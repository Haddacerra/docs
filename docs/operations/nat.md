# NAT Traversal & Network Bridge

The Haddacerra network bridge is designed to provide a low latency, encrypted, and reliable link between the ground control web interface and the CM4 hardware gateway.

Remote deployments may use cellular networks, network address translation (NAT), or carrier-grade NAT (CGNAT). Because direct connectivity cannot be assumed in these environments, the bridge combines WebSocket signaling, Interactive Connectivity Establishment (ICE), STUN/TURN traversal, and encrypted WebRTC DataChannel transport for seamless connectivity.

The system prioritises direct connectivity whenever a viable path can be established, with TURN available as a relay fallback when direct connectivity is unavailable or unsuitable.

## Architecture Overview

The network bridge relies on three primary components working together during session establishment and operation.

**The Ground Client (Browser):** Initiates the flight session, renders telemetry dashboards, processes physical USB controller inputs, and presents the video stream.

**The CM4 Agent:** Runs locally on the hardware gateway, processes incoming control payloads, drives the hardware DAC outputs, collects ADC measurements, and manages local monitoring and peripheral state.

**The Coordination & Relay Infrastructure:** A cloud hosted signaling server handles WebSocket rendezvous and session negotiation, while a dedicated Coturn server provides STUN services and TURN relay connectivity.

Signaling is used to establish the connection. Normal control and telemetry traffic is carried over the established WebRTC DataChannel rather than through the signaling server.

## 1. Signaling and Session Handshake

Before direct or relayed data can flow between the ground client and the CM4 agent, the endpoints must exchange connection information and establish the WebRTC session.

**WebSocket rendezvous:** When the user initiates a link, the browser and CM4 agent establish persistent WebSocket connections to the centralized signaling service.

**SDP Offer/Answer Exchange:** The browser generates a Session Description Protocol (SDP) offer describing the session and DataChannel capabilities. The offer is forwarded to the CM4 agent through the signaling service. The CM4 agent generates the corresponding SDP answer and returns it through signaling.

**Trickle ICE:** ICE candidates are exchanged as they become available, allowing connectivity checks and session establishment to proceed without waiting for all candidates to be gathered first.

The signaling service coordinates session establishment; it does not carry the normal control and telemetry DataChannel traffic.

## 2. Interactive Connectivity Establishment (ICE) & NAT Traversal

Once session negotiation begins, the browser and CM4 agent gather network candidates and use ICE connectivity checks to determine which communication paths are viable.

ICE can use several candidate types:

**Host Candidates:** Local network addresses available on the endpoint. These may provide a direct path when the endpoints can communicate over the same network or another reachable network route.

**Server-Reflexive Candidates (STUN):** Addresses and port mappings observed by a STUN server. These can help establish direct connectivity through NAT when the resulting mappings are reachable by the other endpoint.

**Relay Candidates (TURN):** Addresses allocated through a TURN server. These provide a relayed path when direct connectivity cannot be established or when the connection policy requires a relay.

ICE evaluates viable candidate pairs and selects a working path according to candidate priorities, connectivity checks, and the configured connection policy. These candidate types are not three mandatory sequential stages. A TURN candidate may be gathered while direct connectivity is also being tested; gathering a relay candidate does not mean that the relay is carrying traffic.

### Direct Connectivity and TURN Fallback

Haddacerra prioritises direct connectivity whenever a suitable direct path can be established. This avoids unnecessary relay hops and helps minimise control latency.

Being behind CGNAT does not automatically require a TURN relay. Depending on the carrier's NAT behaviour, port mappings, and firewall restrictions, ICE may still establish a direct peer-to-peer path.

When a suitable direct path is unavailable or unsuitable, ICE can select a TURN relay candidate. In this case, control and telemetry packets are forwarded through the configured Coturn server. When ICE selects a direct candidate pair, the DataChannel traffic bypasses the TURN relay.

This approach combines low-latency direct connectivity where possible with relay support for more restrictive network environments.

TURN improves connectivity options but cannot guarantee connectivity under every possible network condition. Successful relay operation depends on server availability, network reachability, valid credentials, and compatible network policies.

## 3. Secure Coturn Relay Integration

To prevent unauthorized relay usage and abuse of cloud resources, the Coturn relay uses time-limited credentials generated through the configured shared-secret authentication mechanism.

Rather than embedding a permanent TURN password in the client, the system provisions temporary credentials for session establishment. HMAC-SHA1 is used by the configured credential mechanism to derive the authentication password from the shared secret and credential username. Coturn validates the supplied credentials when the client requests a relay allocation.

These credentials authenticate access to the relay service; they do not themselves encrypt the control payload. DataChannel encryption is provided separately by DTLS.

When TURN is selected, Coturn forwards the encrypted traffic between the WebRTC peers. It does not need to decrypt the application data to relay the packets.

## 4. Encrypted Transport & DataChannel Stack

After session establishment, operational control commands, feedback, and telemetry are carried over a dedicated WebRTC DataChannel using SCTP over DTLS over UDP.

**Datagram Transport Layer Security (DTLS):** DTLS provides encryption and integrity protection for DataChannel traffic between the browser and CM4 agent. When a TURN relay is used, the DataChannel remains encrypted between the peers while Coturn forwards the packets.

**Stream Control Transmission Protocol (SCTP):** SCTP operates over DTLS and provides DataChannel message transport. The control channel is configured for unordered delivery with retransmissions disabled, favouring timely control updates over guaranteed delivery of every individual message.

This configuration avoids waiting for ordered delivery or retransmission of lost control messages. However, messages may still be delayed or lost, and the configuration does not eliminate network congestion or guarantee a fixed end-to-end latency. Actual responsiveness depends on network conditions, endpoint processing, and the behaviour of the complete control and feedback path.
