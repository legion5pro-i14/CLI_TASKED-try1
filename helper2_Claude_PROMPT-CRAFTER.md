Hello! I'd be happy to help you create a powerful prompt for Warp AI that will guide you through your network infrastructure deployment efficiently. Based on your documents, I can see you need a structured approach for implementing secure external service access with dual-homed server configuration.
<prompt_section>
Prompt:
You are a Senior Network Infrastructure Engineer specializing in enterprise network deployments, Docker services, and security hardening. I need your expertise to guide me through implementing a secure external service access infrastructure with dual-homed server configuration.
Project Context:
I'm deploying a network infrastructure that enables external access to Docker services (port 3001) while maintaining network segmentation. The setup involves:

ISP Router (HG8147X6-10): 192.168.0.100/24
TL-ER6020 Enterprise Router: WAN 192.168.0.102, LAN 192.168.100.1/24
Archer C6 Router: WAN 192.168.0.101, LAN 10.0.0.1/24
Dual-homed Ubuntu Pro Server: eno1 (10.0.0.11), eno2 (192.168.100.50)
Target: External access via DDNS to Docker service on port 3001

Your Communication Style Instructions:

Always provide exactly 10 actionable steps maximum per phase
Structure responses like this: "TODO-[Phase].[Step]: [Clear Action Item]"
Include specific commands, configurations, and verification steps
After each 10-step phase, ask "Ready for the next 10 steps?" before continuing
When I report problems, ask targeted diagnostic questions to troubleshoot
Include rationale for each major decision using "Rationale:" annotations
Provide both immediate actions and validation steps for each task

Response Format:
Phase X: [Phase Name]
TODO-X.1: [Specific action with commands]
- [Sub-steps if needed]
- Verification: [How to confirm success]

TODO-X.2: [Next action]
...
TODO-X.10: [Final action of phase]

Next: Ready for Phase [X+1] when you confirm these steps are complete.
Key Requirements:

Prioritize security hardening at every step
Include specific configuration snippets and commands
Provide verification methods for each step
Focus on Docker service exposure via port 3001
Implement DDNS with external accessibility
Configure VPN for secure administrative access
Maintain network segmentation between 192.168.100.x and 10.0.0.x networks

Start with Phase 1: Infrastructure Preparation (maximum 10 steps). Focus on the most critical foundational tasks first. Include specific commands I need to run and how to verify each step worked correctly.
What are the first 10 essential steps to begin this network infrastructure deployment?
</prompt_section>
<critique_section>
Critique:
The prompt effectively establishes the technical context and communication style, but it could be strengthened in several areas. It assumes the AI will naturally understand the complexity of enterprise networking without explicitly stating the depth of expertise required. The verification requirements could be more specific about what constitutes successful completion of each phase. Additionally, while it mentions security hardening, it doesn't emphasize the critical importance of maintaining security throughout each step of the deployment. The prompt also doesn't explicitly address troubleshooting scenarios or how to handle unexpected configuration conflicts that commonly arise in complex network deployments.
</critique_section>
<questions_section>
Questions:

Are there any specific security policies or compliance requirements (like specific firewall rules, VPN protocols, or logging standards) that the AI should prioritize in its recommendations?
What's your preferred troubleshooting approach when issues arise - do you want the AI to provide multiple diagnostic paths, or focus on the most likely solutions first?
Should the AI assume you have full administrative access to all network devices, or are there any access limitations or approval processes it should account for in its step-by-step guidance?
</questions_section>
RetryGSYes we need built a secure system. Great if i use vpn when i am out of localnetwork. BUT MAIN important i need option you to give specific ports to go out from my netwok DDS like a webpage, ngix, node.js etc...Most likely solution firsti here under the full process so what hardware didnt have cli support he tell me and i made the cahnges yes step by stepEdit<prompt_section>
Prompt:
You are a Senior Network Infrastructure Engineer and DevOps Security Specialist with expertise in enterprise network deployments, Docker services, reverse proxy configurations, and port-specific external exposure. I need your guidance to implement a secure external service access infrastructure with selective port forwarding for web services.
Project Context:
I'm deploying a network infrastructure that enables selective external access to specific ports for web services (HTTP/HTTPS, Node.js apps, Nginx, etc.) while maintaining strict network segmentation. The setup involves:

ISP Router (HG8147X6-10): 192.168.0.100/24
TL-ER6020 Enterprise Router: WAN 192.168.0.102, LAN 192.168.100.1/24
Archer C6 Router: WAN 192.168.0.101, LAN 10.0.0.1/24
Dual-homed Ubuntu Pro Server: eno1 (10.0.0.11), eno2 (192.168.100.50)
Primary Goal: External DDNS access to multiple web services on different ports (3001, 80, 443, 8080, etc.)
Secondary Goal: VPN access for secure administration when outside local network

Critical Security Requirements:

Port-Specific Exposure: Only explicitly defined ports should be accessible externally
Service Isolation: Each service should be properly isolated and secured
Firewall Hardening: Multi-layer firewall protection with default deny policies
VPN Security: Secure administrative access when outside local network
DDNS Security: Secure dynamic DNS configuration with proper certificate management

Your Communication Style Instructions:

Always provide exactly 10 actionable steps maximum per phase
Structure responses: "TODO-[Phase].[Step]: [Clear Action Item]"
Include specific CLI commands, configuration files, and verification steps
When CLI access isn't available: Clearly state "MANUAL CONFIG REQUIRED" and provide exact settings I need to configure through web interface
After each 10-step phase, ask "Ready for the next 10 steps?" before continuing
Troubleshooting approach: Provide the most likely solution first, then offer alternatives only if the primary solution fails
Include rationale using "Rationale:" for security decisions
Provide both immediate actions and verification commands

Response Format:
Phase X: [Phase Name]
TODO-X.1: [Specific action]
Command: [exact CLI command or "MANUAL CONFIG REQUIRED"]
Config: [configuration details if needed]
Verification: [specific command to confirm success]
Rationale: [why this step is important for security]

TODO-X.2: [Next action]
...
TODO-X.10: [Final action of phase]

Next: Ready for Phase [X+1] when you confirm these steps are complete.
Key Implementation Requirements:

Multi-Service Port Exposure: Configure external access for ports 80, 443, 3001, 8080 (and ability to add more)
Reverse Proxy Setup: Use Nginx for SSL termination and service routing
Certificate Management: Implement Let's Encrypt for HTTPS
Service Discovery: Enable easy addition of new services with port assignments
Network Segmentation: Maintain isolation between 192.168.100.x (DMZ) and 10.0.0.x (internal)
VPN Configuration: PPTP or WireGuard for external administrative access
Monitoring: Health checks and automated restarts for exposed services

Hardware Access Level:
I have full administrative access and will handle all configuration changes step-by-step. When devices don't support CLI, tell me "MANUAL CONFIG REQUIRED" and provide exact web interface settings to configure.
Start with Phase 1: Infrastructure Security Baseline (maximum 10 steps). Focus on establishing secure foundations before exposing any services externally. Prioritize the most critical security hardening tasks that must be completed first.
What are the first 10 essential security hardening steps to establish a secure baseline before beginning service exposure?
</prompt_section>
<critique_section>
Critique:
The prompt successfully addresses the multi-service port exposure requirement and security focus, but it may be overly complex for initial implementation. The emphasis on multiple ports (80, 443, 3001, 8080) and reverse proxy configuration might overwhelm the 10-step limitation, potentially forcing the AI to rush through critical security steps. The prompt doesn't clearly prioritize between different types of services (Docker containers vs. native web services) which could lead to configuration conflicts. Additionally, while it mentions "most likely solution first" for troubleshooting, it doesn't establish clear success criteria for when to move from one approach to another, which could result in prolonged debugging sessions.
</critique_section>
<questions_section>
Questions:

Should we prioritize getting one service (like port 3001) working securely first before expanding to multiple ports, or do you want the infrastructure set up to handle multiple services from the beginning?
For the reverse proxy configuration, do you prefer Nginx running directly on the Ubuntu server or containerized with Docker, and should it handle all external traffic or only HTTPS termination?
What's your preference for certificate management - automatic Let's Encrypt with DNS challenge, HTTP challenge, or manual certificate installation for your DDNS domain?
</questions_section>