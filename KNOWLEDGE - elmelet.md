Project Knowledge Base: Secure External Service Access Infrastructure
Overview
Project Purpose
Design and implement a secure network infrastructure that enables external access to Docker services running on internal Linux servers while maintaining network segmentation and security. The project focuses on exposing a Docker service running on port 3001 to external networks via DDNS, while providing VPN access for remote administration.
Current State

Network Infrastructure: Multi-router setup with ISP gateway, enterprise router (TL-ER6020), and internal router (Archer C6)
Server Configuration: Dual-homed Ubuntu Pro server with interfaces on both network segments
Service Target: Docker containerized service on port 3001 requiring external accessibility
Access Requirements: Both direct external access and secure VPN-based administration

High-Level Vision
Create a production-ready, secure network architecture that balances accessibility with security, enabling external service consumption while maintaining strict network segmentation and administrative control.
Key Decisions & Rationale
Network Topology Decision: Segmented Architecture
Decision: Implement isolated network segment (192.168.100.x) via TL-ER6020 for externally accessible services, separate from main internal network (10.0.0.x).
Rationale:

Minimizes attack surface by isolating public-facing services
Provides dual firewall protection (ISP router + TL-ER6020)
Enables independent security policies for different network segments
Allows controlled inter-network communication via dual-homed server

Router Selection: TL-ER6020 as DMZ Gateway
Decision: Use TL-ER6020 enterprise router as the gateway for externally accessible services rather than direct port forwarding from ISP router.
Rationale:

Enterprise-grade security features (VPN, advanced firewall, attack defense)
Built-in DDNS support for dynamic IP management
Comprehensive NAT and port forwarding capabilities
Better logging and monitoring features than consumer routers

DDNS Strategy: No-IP Service
Decision: Implement Dynamic DNS using No-IP service integrated with TL-ER6020.
Rationale:

Automatic IP address tracking for dynamic ISP connections
Free tier available for proof-of-concept
Native integration with TL-ER6020 router
Eliminates need for manual IP address management

Dual Access Pattern: Direct + VPN
Decision: Provide both direct external access (port 3001) and VPN-based administrative access.
Rationale:

Direct access optimizes performance for service consumers
VPN access provides secure administrative channel
Separates operational traffic from management traffic
Enables different security policies for different access types

Strategic Directions Explored
Option A: VPN-Only Access
Summary: Route all external access through VPN tunnel
Pros: Maximum security, encrypted all traffic, centralized access control
Cons: Performance overhead, complexity for end users, single point of failure
Decision: Rejected in favor of dual approach
Option B: Reverse Proxy with SSL Termination
Summary: Use Nginx reverse proxy with Let's Encrypt certificates
Pros: SSL encryption, advanced routing, caching capabilities
Cons: Additional complexity, certificate management overhead
Decision: Marked as future enhancement
Option C: Cloudflare Tunnel
Summary: Use Cloudflare's tunnel service to avoid port forwarding
Pros: No port forwarding needed, built-in DDoS protection, automatic SSL
Cons: Dependency on third-party service, potential latency
Decision: Documented as alternative approach
Technical Requirements & Architecture
Network Architecture
Internet → HG8147X6-10 (ISP) → TL-ER6020 → Ubuntu Server (Docker Service)
                            ↘ Archer C6 → Internal Network + TP Switch
IP Address Schema

ISP Network: 192.168.0.x/24

ISP Router: 192.168.0.100
TL-ER6020 WAN: 192.168.0.102
Archer C6 WAN: 192.168.0.101


DMZ Network: 192.168.100.x/24

TL-ER6020 LAN: 192.168.100.1
Ubuntu Server eno2: 192.168.100.50


Internal Network: 10.0.0.x/24

Archer C6 LAN: 10.0.0.1
Ubuntu Server eno1: 10.0.0.11



Server Configuration
Dual-Homed Ubuntu Pro Server:
yamlnetwork:
  version: 2
  ethernets:
    eno1:
      addresses: [10.0.0.11/24]
      routes: [to: default, via: 10.0.0.1]
    eno2:
      addresses: [192.168.100.50/24]
      routes: [to: default, via: 192.168.100.1]
Service Requirements

Docker Service: Port 3001 binding
External Access: http://[domain].ddns.net:3001
Security: Firewall rules, fail2ban, rate limiting
Monitoring: Health checks, automated restarts, alerting

Port Forwarding Chain

ISP Router: 3001 → 192.168.0.102:3001
TL-ER6020: 3001 → 192.168.100.50:3001
Ubuntu Server: Docker container on port 3001

Security Implementation Strategy
Defense in Depth Layers

Perimeter: ISP router basic firewall
Network: TL-ER6020 enterprise firewall with attack defense
Host: Ubuntu UFW firewall + fail2ban
Application: Docker container security + rate limiting

Access Control Policies

Direct Service Access: Limited to specific ports (3001)
Administrative Access: VPN-only for SSH and management
Inter-Network: Controlled routing between network segments
Monitoring: Comprehensive logging across all layers

VPN Configuration Options
Primary: PPTP VPN on TL-ER6020

Simple configuration and client support
Adequate for administrative access
IP pool: 192.168.101.2-10

Alternative: WireGuard on Ubuntu server

Modern encryption and performance
Cross-platform client support
Future migration path

Implementation Phases
Phase 1: Infrastructure Setup

Router configuration and network segmentation
Server dual-homing configuration
Basic connectivity testing

Phase 2: Service Exposure

Docker service configuration
Port forwarding implementation
DDNS setup and testing

Phase 3: Security Hardening

Firewall rule implementation
VPN server configuration
Monitoring and alerting setup

Phase 4: Validation & Documentation

End-to-end testing from external networks
Performance and security validation
Documentation and runbook creation

Monitoring & Maintenance Strategy
Health Monitoring
bash#!/bin/bash
# Service health check template
SERVICE_URL="http://localhost:3001"
if ! curl -f $SERVICE_URL > /dev/null 2>&1; then
    docker restart [service-name]
    echo "$(date): Service restarted" >> /var/log/service-monitor.log
fi
DDNS Monitoring

Regular external accessibility checks
IP change detection and notification
Automated DNS propagation verification

Security Monitoring

Failed authentication attempt tracking
Unusual traffic pattern detection
Port scan and intrusion attempt logging

Prompt Engineering Practices
The Conductor's Mindset Applied
Throughout this project, the AI assistant demonstrated:

Vision Holding: Maintained focus on secure external access while balancing usability
Intent Communication: Translated technical requirements into clear implementation steps
Quality Guardian: Emphasized security best practices and comprehensive testing
Context Provision: Included rationale for each recommendation and alternative approaches
Iterative Refinement: Adapted recommendations based on revealed network constraints

Effective Prompt Patterns Used

Constraint Revelation: Gradually revealed network topology details to get contextual advice
Multiple Language Context: Started in English, switched to Hungarian for comfort, returned to English for documentation
Structured Output Requests: Requested specific formats (TODO lists, configuration files) for actionable results

AI Interaction Best Practices Demonstrated

Incremental Disclosure: Revealed system details progressively to avoid overwhelming initial responses
Cultural Context: Used native language when complex concepts needed clarification
Validation Requests: Asked for confirmation of understanding before proceeding with recommendations
Alternative Seeking: Explicitly requested multiple approaches to enable informed decision-making

Open Questions & Next Steps
Technical Decisions Required

 SSL/TLS implementation strategy (Let's Encrypt vs. self-signed vs. none)
 Service discovery mechanism for multiple Docker services
 Log aggregation and centralized monitoring solution
 Backup and disaster recovery procedures

Future Enhancements

 Container orchestration (Docker Compose/Swarm)
 Load balancing for high availability
 Automated certificate management
 Enhanced security scanning and vulnerability management

Performance Considerations

 Bandwidth optimization for external access
 CDN implementation for static assets
 Database connectivity patterns for dual-homed server
 Connection pooling and resource management

Configuration Templates
TL-ER6020 Virtual Server Rule
Name: DockerService3001
External Port: 3001
Internal IP: 192.168.100.50
Internal Port: 3001
Protocol: TCP
Status: Activate
Ubuntu UFW Configuration
bashsudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow 3001/tcp
sudo ufw enable
Docker Service Template
bashdocker run -d \
  --name myservice \
  --restart unless-stopped \
  -p 3001:3001 \
  [image-name]
References & Resources
Network Security Best Practices

NIST Cybersecurity Framework
OWASP Top 10 for web applications
CIS Controls for network security

Documentation Sources

TL-ER6020 User Guide (provided in chat)
Ubuntu Netplan documentation
Docker networking best practices

Testing Tools

nmap for port scanning validation
curl for service accessibility testing
fail2ban for intrusion prevention
netstat/ss for connection monitoring


Last Updated: Based on chat history through network topology finalization and implementation planning phase.
Next Review: After Phase 1 implementation completion for lessons learned integration.