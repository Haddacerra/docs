##  Network Bridge & NAT Traversal
The Haddacerra network bridge architecture is engineered to provide a ultra-low-latency, highly secure, and reliable communication link between the ground control web interface and the mobile hardware gateway (Compute Module 4) running on the vehicle.

Because remote operations frequently take place over cellular networks and carrier-grade NAT (CGNAT), traditional direct IP routing is impossible. To solve this, the bridge combines WebSocket signaling, Interactive Connectivity Establishment (ICE), STUN/TURN traversal protocols, and end-to-end transport layer security.

## Architecture Overview

The network bridge relies on three primary components cooperating during a session establishment:

The Ground Client (Browser): Initiates the flight session, renders telemetry dashboards, processes physical USB controller inputs, and streams video.

The CM4 Agent: Running locally on the hardware gateway, it monitors onboard sensors, translates control payloads directly into hardware DAC/ADC voltages, and manages local peripheral state.

The Coordination & Relay Infrastructure: A cloud-hosted signaling server (handling WebSocket rendezvous) paired with a dedicated Coturn server (handling STUN/TURN routing).

## 1. Signaling and Session Handshake
Before any direct or relayed data can flow between the ground client and the vehicle, both entities must discover each other and agree on cryptographic parameters.

WebSocket rendezvous: When the user initiates a link, both the client and the CM4 agent connect to a centralized coordination server via persistent WebSocket connections.

SDP Offer/Answer Exchange: The browser generates a Session Description Protocol (SDP) offer detailing its media and data channel capabilities, sending it through the signaling server to the CM4 agent. The CM4 processes the offer, creates a matching local description (answer), and transmits it back.

Trickle ICE: Rather than waiting for complete network path discovery before finalizing the handshake, network candidates are exchanged dynamically ("trickled") as they are gathered, significantly reducing connection establishment time.

## 2. Interactive Connectivity Establishment (ICE) & NAT Traversal
Once signaling is complete, the browser and the CM4 execute ICE to determine the optimal communication path. ICE evaluates three tiers of candidates sequentially:

Host Candidates: Local network addresses used if both devices happen to reside on the same local subnet.

Server-Reflexive Candidates (STUN): Discovered by querying a STUN server to reveal the public IP addresses and port mappings assigned by standard home or office routers.

Relay Candidates (TURN): Used as a mandatory fallback when strict firewalls, symmetric NATs, or carrier-grade NAT (CGNAT) prevent direct peer-to-peer UDP hole punching.

In cellular deployments where the CM4 is assigned a private carrier IP behind CGNAT, the system automatically coordinates through the cloud TURN relay to guarantee reliable connectivity regardless of network topology.

## 3. Secure Coturn Relay Integration
To prevent unauthorized bandwidth consumption and abuse of cloud resources, the Coturn relay server enforces strict authentication using time-limited, dynamically generated credentials.

Instead of relying on static plain-text passwords that risk exposure, the system generates ephemeral HMAC-SHA1 cryptographic signatures for every session. The coordination server and the vehicle agent compute these secure tokens dynamically using a shared secret. The Coturn server validates the token on connection, allocates a secure relay channel, and routes binary data packets transparently between the peers.

## 4. Encrypted Transport & DataChannel Stack
All operational control commands, feedback loops, and telemetry data bypass traditional HTTP overhead, traveling instead over a dedicated WebRTC DataChannel.

Transport Layer Security (DTLS): All data moving across the network bridge—whether traversing a direct local link or passing through the cloud Coturn relay—is encrypted by default using Datagram Transport Layer Security (DTLS) backed by robust cryptographic ciphers. Eavesdropping or packet tampering on public cellular networks is structurally prevented.

Multiplexed Low-Latency Framing (SCTP): Operating on top of DTLS and UDP, the Stream Control Transmission Protocol (SCTP) manages data delivery. The control channel is configured for un-ordered, non-retransmitted delivery (or minimal retransmissions), ensuring that stale command frames are immediately dropped rather than queued. This eliminates buffer bloat and guarantees that flight control inputs maintain absolute real-time responsiveness.
