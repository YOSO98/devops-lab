# devops-lab

## Présentation du projet

**devops-lab** est un projet de démonstration DevOps visant à mettre en place, déployer et automatiser une application web **Nginx** en utilisant plusieurs outils clés de l’écosystème DevOps.

Le projet couvre :
- le déploiement avec **Docker**
- l’orchestration avec **Kubernetes (Minikube)**
- l’automatisation avec **Ansible**
- les bases du **monitoring avec Prometheus**

---

## Objectif

Mettre en œuvre une stack web simple, reproductible et automatisée dans un environnement Linux (Debian / WSL), en suivant une démarche DevOps complète.

---

## Architecture (Docker)


Client → Nginx (conteneur Docker) → Port 8080


---

## Technologies utilisées

- Linux (Debian – WSL)
- Docker
- Docker Compose
- Kubernetes (Minikube)
- Ansible
- Prometheus
- Nginx

---

## Déploiement Docker (Stack Web)

### Étape 1 – Cloner le repository

```bash
git clone https://github.com/YOSO98/devops-lab.git
cd devops-lab



Étape 2 – Lancer la stack Docker
docker compose up -d

Étape 3 – Vérifier l’état des conteneurs
docker ps

Étape 4 – Tester le service
curl http://localhost:8080


Ou dans un navigateur :

http://localhost:8080

Résultat attendu

Page d’accueil Nginx affichée

Service accessible depuis la machine hôte

Déploiement Kubernetes avec Minikube
Objectif

Déployer Nginx sur un cluster Kubernetes local afin de maîtriser les concepts fondamentaux de Kubernetes.

Étape 1 – Démarrer Minikube
minikube start --driver=docker

Étape 2 – Déployer Nginx
kubectl apply -f k8s/nginx.yaml

Étape 3 – Vérifier les ressources
kubectl get pods
kubectl get svc

Étape 4 – Accéder au service
kubectl port-forward svc/nginx-service 8081:80


Navigateur :

http://localhost:8081

Résultat attendu

Pod en état Running

Service accessible via port-forward

Automatisation avec Ansible
Objectif

Installer et configurer automatiquement Nginx sur Linux sans aucune intervention manuelle.

Arborescence utilisée
ansible/
├── inventory/
│   └── hosts.ini
└── playbooks/
    └── install_nginx.yml

Étape 1 – Inventaire Ansible

Fichier : ansible/inventory/hosts.ini

[local]
localhost ansible_connection=local

Étape 2 – Playbook Ansible

Fichier : ansible/playbooks/install_nginx.yml

---
- name: Installer et configurer Nginx avec Ansible
  hosts: local
  become: true

  tasks:
    - name: Mettre à jour le cache APT
      apt:
        update_cache: yes

    - name: Installer Nginx
      apt:
        name: nginx
        state: present

    - name: Démarrer et activer Nginx
      service:
        name: nginx
        state: started
        enabled: true

Étape 3 – Configuration sudo sans mot de passe
sudo visudo


Ajouter à la fin du fichier :

debian ALL=(ALL) NOPASSWD: ALL


⚠️ Configuration réservée à un environnement de laboratoire.

Étape 4 – Exécuter le playbook
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/install_nginx.yml

Étape 5 – Vérification
curl http://localhost

Monitoring avec Prometheus
Objectif

Superviser les services via un système de monitoring simple.

Arborescence monitoring
monitoring/
├── docker-compose.monitoring.yml
└── prometheus/
    └── prometheus.yml

Étape 1 – Lancer Prometheus
docker compose -f monitoring/docker-compose.monitoring.yml up -d

Étape 2 – Vérifier les conteneurs
docker ps

Étape 3 – Accéder à Prometheus

Navigateur :

http://localhost:9090

Étape 4 – Vérifier les targets

Dans l’interface Prometheus :

Status → Targets


Les services doivent être en état UP.

Compétences démontrées

Docker et Docker Compose

Kubernetes (Deployment, Service)

Ansible (inventaire, playbooks, automatisation)

Linux et gestion des privilèges

Monitoring avec Prometheus

Démarche DevOps complète

Conclusion

Ce projet constitue un portfolio DevOps structuré, automatisé et reproductible, démontrant des compétences concrètes applicables en environnement professionnel.
