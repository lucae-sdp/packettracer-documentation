# CCNA Study Roadmap

My study track for the **Cisco CCNA 200-301**, built around Cisco Packet Tracer.
Each module pairs theory with a lab that I build myself and document in its own
folder.

## How each module works

1. **Theory**: study the topics listed for the module.
2. **Lab**: build the suggested lab in Packet Tracer from scratch.
3. **Document**: write the lab's `README.md` (what I did, why, what I learned),
   with a screenshot and the `.pkt` file, committed using Conventional Commits.
4. **Review**: answer the module's checkpoint questions without notes. If I can't,
   I go back to the theory before moving on.

## Sources

- **Jeremy's IT Lab**: free full CCNA course on YouTube, with Packet Tracer labs.
  Main theory source.
- **Gabriel Torres, "Arquitetura de Redes" (Udemy)**: deeper fundamentals, in
  Portuguese. Use alongside modules 1 and 2.
- **NetworkChuck**: introductions and motivation, not the main source.
- **Cisco exam topics (200-301 v1.1)**: the official blueprint. The domain weights
  below come from it.

## Exam domains

| Domain                          | Weight | Modules |
|---------------------------------|--------|---------|
| 1. Network Fundamentals         | 20%    | 1, 2    |
| 2. Network Access               | 20%    | 3, 4    |
| 3. IP Connectivity              | 25%    | 5, 6    |
| 4. IP Services                  | 10%    | 7       |
| 5. Security Fundamentals        | 15%    | 8       |
| 6. Automation and Programmability | 10%  | 9       |

---

## Module 1: Fundamentals

**Theory**
- OSI and TCP/IP models, encapsulation (what each layer adds to a frame/packet)
- Network devices: hub, switch, router, AP, firewall
- Cabling: copper (straight vs crossover, Auto-MDIX), fiber, connectors
- Ethernet frames, MAC addresses, how a switch learns MACs
- ARP and why a PC needs it before sending an IP packet
- Cisco IOS basics: user/privileged/config modes, `show running-config`,
  saving the config

**Labs**
- [x] `hello-world`: two PCs pinging each other
- [x] `fase1/testing-lab`: first exploration lab
- [ ] Switch MAC table: three PCs on one switch; watch `show mac address-table`
      fill up while pinging, then clear it and watch again
- [ ] ARP in simulation mode: follow an ARP request/reply step by step
- [ ] Basic switch config: hostname, enable secret, console/VTY passwords, banner

**Checkpoint**
- Why does the first ping often lose a packet?
- What does a switch do with a frame for a MAC it doesn't know yet?

## Module 2: IPv4 Addressing and Subnetting

**Theory**
- IPv4 address structure, binary conversion, private ranges (RFC 1918)
- Subnet masks, CIDR, network/broadcast addresses, usable hosts
- Subnetting and VLSM
- IPv6 basics: address types, abbreviation, SLAAC
- Default gateway: when a host uses it and when it doesn't

**Labs**
- [ ] Two subnets, one router: two LANs talking through a router's interfaces
- [ ] VLSM design: given host counts, design and implement the addressing plan
- [ ] Wrong mask on purpose: break one PC's mask and explain the result

**Checkpoint**
- Subnet 192.168.10.0/24 into networks for 60, 28, 12 and 2 hosts.
- Why does a wrong mask sometimes work in one direction only?

## Module 3: Switching and VLANs

**Theory**
- VLANs and why they exist (broadcast domains, segmentation)
- Access vs trunk ports, 802.1Q tagging, native VLAN
- Inter-VLAN routing: router-on-a-stick and Layer 3 switch (SVIs)
- CDP and LLDP

**Labs**
- [ ] VLANs on one switch: two VLANs, confirm they can't talk
- [ ] Trunk between two switches: same VLANs across both
- [ ] Router-on-a-stick: subinterfaces route between the VLANs
- [ ] Layer 3 switch: replace the router with SVIs

**Checkpoint**
- What happens if the native VLAN differs on each side of a trunk?

## Module 4: STP and EtherChannel

**Theory**
- Layer 2 loops and broadcast storms
- STP/RSTP: root bridge election, port roles and states, PortFast, BPDU Guard
- EtherChannel: LACP vs PAgP, load balancing

**Labs**
- [ ] Triangle of switches: find the root bridge and the blocked port, then
      change the root on purpose
- [ ] EtherChannel with LACP between two switches

**Checkpoint**
- Why is the root bridge chosen by default often a bad choice?

## Module 5: Routing Fundamentals

**Theory**
- Routing table: connected, static, dynamic routes; longest prefix match
- Administrative distance and metric
- Static routes, default route, floating static route

**Labs**
- [ ] Three routers with static routes end to end
- [ ] Default route toward an "ISP" router
- [ ] Floating static route as a backup link

**Checkpoint**
- Given a routing table, which route does a packet to a given address use, and why?

## Module 6: OSPF

**Theory**
- Link-state routing, OSPF neighbors and adjacencies, DR/BDR
- Single-area OSPFv2 configuration, router ID, cost
- First-hop redundancy (HSRP) concepts

**Labs**
- [ ] Single-area OSPF with three routers; read `show ip ospf neighbor`
- [ ] Change interface cost and watch the path change
- [ ] Redistribute a default route into OSPF

**Checkpoint**
- Why might two routers on the same link never become OSPF neighbors?

## Module 7: IP Services

**Theory**
- DHCP (DORA) and DHCP relay
- DNS
- NAT/PAT
- NTP, Syslog, SNMP concepts
- QoS concepts

**Labs**
- [ ] Router as DHCP server, then DHCP relay to a server in another subnet
- [ ] PAT: a LAN reaching an "internet" router through one public address
- [ ] Syslog and NTP server on the network

**Checkpoint**
- Why does DHCP need a relay to cross a router?

## Module 8: Security Fundamentals

**Theory**
- Threats, vulnerabilities, common attacks
- Standard and extended ACLs
- Port security, DHCP snooping, Dynamic ARP Inspection
- SSH instead of Telnet, AAA concepts
- Wireless security: WPA2/WPA3

**Labs**
- [ ] Standard and extended ACLs: block one host from a server, allow the rest
- [ ] Port security with sticky MACs; trigger a violation
- [ ] SSH-only management on a router

**Checkpoint**
- Where should a standard ACL be placed, and why there?

## Module 9: Wireless, Automation and Programmability

**Theory**
- Wireless: 802.11 standards, autonomous APs vs WLC
- SDN concepts: control plane vs data plane, controllers
- REST APIs, JSON, configuration management tools (Ansible concepts)

**Labs**
- [ ] WLAN with a wireless controller in Packet Tracer
- [ ] Python script that parses `show` output (in `code-exercises`)

**Checkpoint**
- What problem does a controller solve that CLI-per-device doesn't?

---

## Python track (parallel)

Kept in the [`code-exercises`](https://github.com/lucae-sdp/code-exercises) repo,
in its own folder. Light pace, always tied to networking:

1. Python basics: variables, types, conditionals, loops, functions
2. Strings and files: read a saved `show ip interface brief` and print its table
3. Subnet calculator (by hand first, then compare with the `ipaddress` module)
4. JSON and dictionaries: model a network inventory
5. Netmiko and APIs: only after Module 9 theory
