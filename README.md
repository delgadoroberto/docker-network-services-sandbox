# docker-network-services-sandbox

A complete, isolated laboratory environment designed to simulate and study core network infrastructure services (DNS and DHCP). This project is heavily inspired by the foundational concepts covered in the **Cisco Networking Basics** curriculum, maping abstract Layer 3, Layer 4, and Layer 7 mechanisms into tangible containers.

## Technical Architecture

The architecture mimics a standard local area network (LAN) environment with a designated gateway, static service points, and a dynamic allocation pool.

*   **Network Domain:** `sandbox.lan`
*   **Subnet:** `192.168.56.0/24`
*   **Gateway (Simulated):** `192.168.56.1`
*   **Core Server (DNS/DHCP):** `192.168.56.10`
*   **DHCP Allocatable Range:** `192.168.56.50` to `192.168.56.150`

```mermaid
graph TD
    Client[LAN Client Device] -->|1. DHCP Request / Broadcast| Server[Core Network Sandbox Container]
    Server -->|2. DHCP Lease IP/DNS/Gateway| Client
    Client -->|3. DNS Query: router.sandbox.lan| Server
    Server -->|4. Local Resolution: 192.168.56.1| Client
    Client -->|5. External Query: google.com| Server
    Server -->|6. Forward to Upstream| PublicDNS[1.1.1.1 / Cisco Umbrella]
