# Remote Connectivity, Signalling and NAT Traversal

## Overview

Haddacerra uses an AWS-hosted infrastructure to establish a UDP communication path between the CM4-based gateway and the remote PC. The connection carries real-time control inputs and telemetry while accommodating the network restrictions commonly encountered on mobile and residential internet connections.

The gateway may operate behind carrier-grade network address translation (CGNAT), where it does not have a publicly reachable IP address of its own. The remote PC may also be behind a NAT or restrictive firewall. A conventional direct UDP connection cannot be assumed to work in these environments.

Haddacerra addresses this problem through connection signalling, NAT traversal and relay infrastructure.

## Signalling and Connection Establishment

An AWS-hosted signalling service coordinates the initial connection between the gateway and the remote PC. It exchanges the connection information required for the endpoints to discover one another and attempt to establish a working communication path.

Signalling is separate from the control-data stream: it helps establish the session, while the UDP connection carries the operational control inputs and telemetry.

## ICE and STUN

Where ICE is implemented by the endpoint software, Interactive Connectivity Establishment (ICE) is used to evaluate potential network paths between the gateway and remote PC.

STUN assists an endpoint in discovering the public-facing IP address and port assigned by its NAT device. This information can help the endpoints identify candidate paths for direct UDP communication.

The endpoints exchange connection candidates through the signalling service and perform connectivity checks to determine which candidate pairs can communicate successfully. This allows the software to select a usable path rather than relying on a fixed assumption about network addressing.

## TURN Relay Fallback

Direct UDP connectivity is not possible in every network environment. Carrier-grade NAT, restrictive firewall rules and particular NAT behaviours can prevent a usable direct path from being established.

When a direct connection cannot be established and the connection procedure supports relay fallback, a TURN server provides an alternative path. The endpoints send their traffic to the relay, which forwards packets between them.

This allows communication to work in many environments where direct endpoint-to-endpoint UDP traffic would otherwise fail. Relay use can add network latency and consumes bandwidth on the relay infrastructure, so the selected route may affect overall control-link performance.

## Control and Telemetry Path

Once a working path has been established, the UDP communication channel carries real-time control inputs from the remote PC to the gateway and returns telemetry to the remote interface.

The connectivity infrastructure is responsible for establishing and supporting the network path. The gateway's control logic and hardware switching architecture remain responsible for handling the received inputs and managing the local signal path.

Network availability does not override the gateway's control-mode logic or replace its configured timeout and hardware-failsafe behaviour. If connectivity is lost, the gateway's defined timeout and safety mechanisms determine how control returns to the appropriate state.

## Network Limitations

Connectivity depends on the behaviour of the participating networks, NAT devices and firewalls. The use of signalling, ICE and TURN improves the ability to establish a connection across difficult network topologies, including many mobile networks using CGNAT, but cannot guarantee connectivity through every possible firewall or network policy.

Latency, jitter, packet loss and route selection also depend on the underlying network and whether traffic travels directly between endpoints or through a relay.
