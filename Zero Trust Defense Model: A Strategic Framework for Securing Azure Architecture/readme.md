# Vue d'ensemble du projet : Familiarisation avec l'architecture de sécurité Zero-Trust (SC-100)

Ce projet personnel vise à approfondir la compréhension et la mise en œuvre de l'architecture de sécurité en utilisant le modèle Zero-Trust pour la certification Azure Cybersecurity Architect Expert (SC-100). J'ai conçu une architecture basée sur une approche d'injection triple, où les concepts de sécurité sont modulaire, répartis en couches, et injectés de manière stratégique dans l'architecture. Cette méthode apporte à la fois flexibilité et une vue d'ensemble solide, tout en pouvant être approfondie davantage.

## Modèle de défense Zero Trust : Un cadre stratégique pour sécuriser l'architecture Azure

### Injection d'architecture triple

1. **Couche d'identité et d'accès (I.A.L)**

    **Objectif** : Vérification d'identité, contrôle d'accès et application de mesures strictes d'authentification/autorisation.  
    **Concepts clés** :
    - **Authentification Zero Trust** : MFA, EntraID et SSO
    - **Contrôle d'accès basé sur les rôles (RBAC)** et accès Just-in-Time
    - **Accès conditionnel** : Basé sur l'utilisateur, le périphérique et la localisation
    - **Gestion des identités privilégiées (PIM)** : Gestion des autorisations élevées

2. **Couche de segmentation du réseau et des données (N.D.S.L)**

    **Objectif** : Isolation du réseau, segmentation et communication sécurisée dans Azure.  
    **Concepts clés** :
    - **Micro-segmentation** : Réseau virtuel (VNet), NSGs
    - **Points de terminaison privés** : Restriction de l'accès à certains services
    - **Pare-feu Azure** & **Pare-feu d'application Web (WAF)** : Inspection du trafic réseau
    - **Cryptage des données** : Azure Key Vault, cryptage au repos et en transit

3. **Couche de surveillance, détection des menaces et réponse (M.T.D.R.L)**

    **Objectif** : Surveillance continue, détection des menaces et mise en place de mécanismes de réponse automatisés.  
    **Concepts clés** :
    - **Azure Sentinel** : Journalisation centralisée et détection des menaces
    - **Microsoft Defender for Identity** : Détection des activités anormales
    - **Réponse automatisée** : Utilisation de playbooks et de flux de travail d'incidents
    - **Azure Defender for Cloud** : Alertes de sécurité et gestion de la posture

## Fonctionnement de l'injection d'architecture triple

Chaque couche de l'injection d'architecture triple est conçue pour renforcer l'approche Zero Trust dans Azure. Ensemble, elles forment un mécanisme de défense solide, conçu pour protéger l'environnement contre les menaces émergentes.

### Couche d'identité et d'accès (I.A.L)

Cette couche fondamentale joue un rôle de gardien, garantissant que seuls les utilisateurs ou services authentifiés et autorisés peuvent accéder aux ressources. Elle impose une vérification rigoureuse de l'identité et assure un accès minimal aux ressources critiques.

### Couche de segmentation du réseau et des données (N.D.S.L)

Une fois l'accès validé, cette couche s'assure d'une segmentation correcte du trafic réseau et de la protection des données. Elle empêche les mouvements latéraux au sein de l'environnement et sécurise les données sensibles, tant en transit qu'au repos.

### Couche de surveillance, détection des menaces et réponse (M.T.D.R.L)

Cette couche permet une détection des menaces en temps réel et une surveillance continue. Même si un attaquant parvient à contourner les autres couches, ce composant agit comme un système d'alerte précoce, permettant des réponses automatisées et rapides pour limiter les risques.

## Intégration des principes Zero Trust

Le modèle Zero Trust est intégré dans l'injection d'architecture triple, garantissant qu'aucune confiance implicite n'est accordée, même pour le trafic interne. Cette approche repose sur :

- **Vérification** : Chaque demande d'utilisateur/service est authentifiée, l'accès étant accordé selon le principe du moindre privilège.
- **Segmentation** : Les ressources sont isolées, avec des règles d'accès strictes pour limiter les déplacements latéraux.
- **Surveillance continue** : Les ressources sont constamment validées pour garantir leur intégrité et leur sécurité.

## Conclusion

En intégrant l'injection d'architecture triple dans le modèle de défense Zero Trust, ce cadre offre une approche en couches complète pour sécuriser les environnements Azure. L'accent mis sur le contrôle d'identité et d'accès, la segmentation du réseau et la surveillance continue assure une protection robuste contre les menaces cybernétiques croissantes dans le cloud.
