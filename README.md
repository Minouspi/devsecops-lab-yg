## Devsecops Lab

![Security](https://github.com/Minouspi/devsecops-lab-yg/workflows/DevSecOps%20Pipeline/badge.svg)

---

## Objectif

Ce projet a pour objectif de mettre en place un pipeline DevSecOps complet permettant de détecter et corriger automatiquement des vulnérabilités dans une application Node.js.

Le pipeline intègre plusieurs outils de sécurité dans GitHub Actions.

---

## Stack technique

- Node.js (Express)
- Docker
- GitHub Actions
- Semgrep (SAST)
- npm audit (SCA)
- Gitleaks (Secrets scanning)
- Trivy (Container scanning)
- OWASP ZAP (DAST)

---

## Vulnérabilités détectées (avant)

Après exécution du pipeline, plusieurs vulnérabilités ont été identifiées :

| Outil      | Résultat | Vulnérabilités trouvées |
|------------|----------|------------------------|
| Semgrep    | Failed   | Secrets hardcodés, manque de validation des entrées |
| npm audit  | Failed   | Dépendances obsolètes avec CVE |
| Gitleaks   | Failed   | Secrets détectés dans le code |
| Trivy      | Failed   | Vulnérabilités dans l’image Docker |

---

## Détails des vulnérabilités

### SAST (Semgrep)
- Absence de validation des entrées utilisateur
- Risque d’injection (exécution de commandes)
- Mauvaises pratiques de sécurité

### SCA (npm audit)
- Présence de dépendances vulnérables
- Risques liés à des bibliothèques obsolètes

### Secrets scanning (Gitleaks)
- Détection de secrets dans le code source
- Risque de fuite d’informations sensibles

### Container scanning (Trivy)
- Vulnérabilités dans l’image Docker
- Présence de CVE critiques et élevées

---

## Corrections appliquées (après)

| Vulnérabilité | Correction |
|--------------|-----------|
| Command Injection | Suppression de exec() et validation des entrées |
| Dépendances vulnérables | Mise à jour des packages |
| Image Docker vulnérable | Utilisation d’une image Node LTS sécurisée |
| Secrets exposés | Utilisation de variables d’environnement et GitHub Secrets |

---

## Métriques

### Avant corrections :
- Critical : 1
- High : 2
- Medium : 1
- Low : 0

### Après corrections :
- Critical : 0
- High : 0
- Medium : 0
- Low : 0

---

## Pipeline DevSecOps

Le pipeline comprend les étapes suivantes :

1. Build de l’image Docker
2. Analyse SAST avec Semgrep
3. Analyse SCA avec npm audit
4. Détection de secrets avec Gitleaks
5. Scan de l’image Docker avec Trivy
6. Scan dynamique avec OWASP ZAP
7. Génération d’un rapport JSON

---

## Analyse

Les vulnérabilités détectées montrent que :

- Le code applicatif peut être exploité via des entrées non sécurisées
- Les dépendances représentent un risque important
- Les secrets ne doivent jamais être exposés dans le code
- Les images Docker doivent être régulièrement mises à jour

---

## Leçons apprises

- Toujours valider les entrées utilisateur
- Ne jamais utiliser exec() avec des données non contrôlées
- Maintenir les dépendances à jour
- Ne pas stocker de secrets dans le code
- Intégrer la sécurité dès le pipeline CI/CD

---

## Améliorations possibles

- Ajouter des tests automatisés
- Intégrer Dependabot ou Snyk
- Ajouter des scans en continu
- Déployer avec une sécurité renforcée (Kubernetes, RBAC, etc.)

---

## Auteur

Projet réalisé dans le cadre d’un lab DevSecOps
