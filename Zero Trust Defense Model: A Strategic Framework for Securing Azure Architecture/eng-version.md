# Project Overview: Familiarization with the Zero-Trust Security Architecture (SC-100)

This is a personal project aimed at better understanding and implementing security architecture using the Zero-Trust model for the Azure Cybersecurity Architect Expert certification (SC-100). I’ve designed an architecture based on a triple injection approach, where common security concepts are modularized into layers and strategically injected into the architecture. This approach provides flexibility and a solid overview, though it can be further developed with more depth.

## Zero Trust Defense Model: A Strategic Framework to Secure Azure Architecture

### Triple Architecture Injection

1. **Identity and Access Layer (I.A.L)**

    **Goal**: Identity verification, access control, and strict authentication/authorization measures.  
    **Key Concepts**:
    - **Zero Trust Authentication**: MFA, EntraID, and SSO
    - **Role-Based Access Control (RBAC)** and Just-in-Time access
    - **Conditional Access**: Based on user, device, and location
    - **Privileged Identity Management (PIM)**: Managing elevated permissions

2. **Network and Data Segmentation Layer (N.D.S.L)**

    **Goal**: Network isolation, segmentation, and secure communication within Azure.  
    **Key Concepts**:
    - **Micro-Segmentation**: Virtual Network (VNet), NSGs
    - **Private Endpoints**: Restricting access to certain services
    - **Azure Firewall** & **Web Application Firewall (WAF)**: Network traffic inspection
    - **Data Encryption**: Azure Key Vault, encryption at rest and in transit

3. **Threat Monitoring, Detection, and Response Layer (T.M.D.R.L)**

    **Goal**: Continuous monitoring, threat detection, and automated response mechanisms.  
    **Key Concepts**:
    - **Azure Sentinel**: Centralized logging and threat detection
    - **Microsoft Defender for Identity**: Detecting abnormal activities
    - **Automated Response**: Using playbooks and incident workflows
    - **Azure Defender for Cloud**: Security alerts and posture management

## How the Triple Architecture Injection Works

Each layer of the triple architecture injection is designed to support the Zero Trust security approach within Azure. Together, they form a robust defense mechanism to protect the environment against emerging threats.

### Identity and Access Layer (I.A.L)

This foundational layer serves as a gatekeeper, ensuring that only authenticated and authorized users or services can access resources. It enforces strict identity verification and minimal access to critical resources.

### Network and Data Segmentation Layer (N.D.S.L)

Once access is granted, this layer ensures proper segmentation of network traffic and protection of data. It prevents lateral movement within the environment and protects sensitive data both in transit and at rest.

### Threat Monitoring, Detection, and Response Layer (T.M.D.R.L)

This layer provides real-time threat detection and continuous monitoring. Even if an attacker bypasses other layers, this component acts as an early warning system, allowing for fast automated responses to mitigate risks.

## Integrating Zero Trust Principles

The Zero Trust model is integrated into the triple architecture injection, ensuring no implicit trust is granted, even for internal traffic. This approach emphasizes:

- **Verification**: Every user/service request is authenticated, with access granted based on the principle of least privilege.
- **Segmentation**: Resources are isolated, with strict access rules to limit lateral movement.
- **Continuous Monitoring**: Resources are continuously validated to ensure their integrity and security.

## Conclusion

By utilizing triple architecture injection within the Zero Trust defense model, this framework provides a layered and comprehensive approach to securing Azure environments. Emphasizing identity and access control, network segmentation, and continuous monitoring ensures robust protection against evolving cyber threats in the cloud.
