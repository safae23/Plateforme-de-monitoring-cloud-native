# Plateforme-de-monitoring-cloud-native
## Description du projet

Ce projet vise la **conception et l’implémentation d’une plateforme de monitoring cloud-native** basée sur **Kubernetes**, **Prometheus**, **Grafana** et **Alertmanager**.
L’objectif est de disposer d’une **solution open-source** capable de :

* Collecter les métriques système et applicatives,
* Visualiser ces données en temps réel via des dashboards interactifs,
* Détecter automatiquement les anomalies à l’aide d’un système d’alertes,
---

## Architecture technique

L’architecture repose sur un cluster **K3d (Kubernetes léger)** exécuté dans **Docker**, et intègre plusieurs composants :

* **Prometheus** : collecte et stocke les métriques.
* **Grafana** : visualisation des données en dashboards interactifs.
* **Alertmanager** : gestion et routage des alertes.
* **Node Exporter** : expose les métriques des nœuds système.
* **Helm** : facilite le déploiement de la stack kube-prometheus-stack.

*Les données sont collectées, analysées et visualisées en temps réel via Grafana.*

---

## Déploiement

### 1. Pré-requis

* Docker Desktop
* K3d
* Helm
* Kubectl
* VS Code 

### 2. Installation du cluster

```bash
k3d cluster create mon-cluster --servers 1 --agents 3
```

### 3. Déploiement de la stack de monitoring

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack -f prometheus-values.yaml
```

### 4. Accès aux interfaces

* **Prometheus** → [http://localhost:9090](http://localhost:9090)
* **Grafana** → [http://localhost:3000](http://localhost:3000)
* **Alertmanager** → [http://localhost:9093](http://localhost:9093)

---

## Application microservices intégrée

Une **mini application microservices** a été développée pour tester la plateforme :

| Service         | Description                                                     | Technologie |
| --------------- | --------------------------------------------------------------- | ----------- |
| `api-gateway`   | Interface web de saisie et redirection vers les microservices   | Flask       |
| `service-age`   | Calcule l’âge d’un utilisateur à partir de sa date de naissance | Flask       |
| `service-poids` | Calcule le poids idéal selon la taille                          | Flask       |

---

## Tests réalisés

* **Tests unitaires** : validation des microservices via `pytest`.
* **Tests d’intégration** : vérification de la communication interservices (HTTP).
* **Tests de performance** : simulation de charge avec **k6**.
* **Monitoring en continu** : vérification temps réel via Grafana + alertes mail via Alertmanager.

---

## Cas d’usage envisagés

* **Industrie 4.0** : supervision de capteurs et maintenance prédictive.
* **Smart Cities** : suivi de services connectés (mobilité, énergie...).
* **E-commerce & Fintech** : surveillance des API et détection d’anomalies.
* **Santé** : supervision d’applications sensibles (dossiers médicaux...).

---

## Technologies utilisées

| Domaine          | Outils                                           |
| ---------------- | ------------------------------------------------ |
| Conteneurisation | Docker, K3d                                      |
| Orchestration    | Kubernetes                                       |
| Monitoring       | Prometheus, Grafana, Alertmanager, Node Exporter |
| Déploiement      | Helm                                             |
| Développement    | Python (Flask), VS Code                          |
| Tests            | Pytest, K6                                       |

---

## Leçons apprises

* Importance du **monitoring dans les environnements conteneurisés**.
* Maîtrise de l’écosystème **Prometheus / Grafana / Alertmanager**.
* Compréhension des **bonnes pratiques DevOps** (supervision, alerting).
* Mise en œuvre d’une **infrastructure cloud-native modulaire et scalable**.

---
## Résultats et perspectives

Le projet a permis de :

* Déployer une **stack de monitoring fonctionnelle** et extensible,
* Mettre en place un **système d’alerte automatique par e-mail**,
* Construire des **dashboards dynamiques** pour le suivi temps réel,
