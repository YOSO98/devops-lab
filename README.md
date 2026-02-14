# devops-lab
Lab DevOps : Docker, Docker Compose et déploiement d’une stack web
Objectif  
Ce projet a pour objectif de démontrer la mise en place d’une stack web simple et reproductible à l’aide de Docker Compose, dans un environnement Linux (WSL).

Architecture  
Client → Nginx (conteneur Docker) → Port 8080

Technologies utilisées  
- Linux (Debian – WSL)  
- Docker  
- Docker Compose  
- Nginx  

Déploiement

1. Cloner le repository
git clone https://github.com/YOSO98/devops-lab.git
cd devops-lab

2. Lancer la stack
docker compose up -d

3. Vérifier les conteneurs
docker ps

4. Tester le service
curl http://localhost:8080  
ou  
Navigateur : http://localhost:8080

Résultat attendu  
Affichage de la page d’accueil Nginx confirmant le bon fonctionnement du conteneur et de l’exposition réseau.

Compétences démontrées  
- Utilisation de Docker et Docker Compose  
- Déploiement de services conteneurisés  
- Gestion des ports et du réseau  
- Environnement Linux et bonnes pratiques DevOps

---

Déploiement Kubernetes (minikube)

Objectif  
Déployer une application Nginx sur un cluster Kubernetes local (minikube) afin de démontrer la maîtrise des concepts fondamentaux Kubernetes.

Ressources Kubernetes  
- Deployment : nginx-deployment  
- Service : nginx-service (NodePort)

Déploiement

1. Démarrer le cluster
minikube start --driver=docker

2. Appliquer les manifests
kubectl apply -f k8s/nginx.yaml

3. Vérifier l’état
kubectl get pods
kubectl get svc

4. Accéder au service (méthode fiable)
kubectl port-forward svc/nginx-service 8081:80

Accès à l’application  
http://localhost:8081

Compétences démontrées  
- Kubernetes (Deployment, Service)  
- Orchestration de conteneurs  
- Débogage et exposition de services  
- Utilisation de minikube

---

Automatisation avec Ansible (Tutoriel)

Objectif  
Mettre en place une automatisation complète permettant d’installer et de configurer un serveur web **Nginx** sur Linux à l’aide d’Ansible, sans intervention manuelle.

---

Tutoriel pas à pas

Étape 1 – Préparer l’arborescence Ansible

Créer la structure suivante dans le projet :

ansible/
├── inventory/
│   └── hosts.ini
└── playbooks/
    └── install_nginx.yml

---

Étape 2 – Définir l’inventaire Ansible

L’inventaire permet de définir la machine cible.  
Dans ce projet, la cible est le serveur local (localhost).

Fichier : ansible/inventory/hosts.ini

[local]
localhost ansible_connection=local

---

Étape 3 – Créer le playbook Ansible

Le playbook automatise les actions suivantes :
- Mise à jour du cache APT
- Installation de Nginx
- Démarrage et activation du service Nginx

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

---

Étape 4 – Configurer sudo sans mot de passe (automatisation complète)

Pour permettre une exécution non interactive du playbook, l’utilisateur utilisé par Ansible est configuré pour utiliser sudo sans mot de passe.

Commande :

sudo visudo

Ajouter la ligne suivante à la fin du fichier :

debian ALL=(ALL) NOPASSWD: ALL

Cette configuration est adaptée à un environnement de laboratoire ou de développement.

---

Étape 5 – Exécuter le playbook

Lancer le playbook avec la commande suivante :

ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/install_nginx.yml

Aucune saisie de mot de passe n’est nécessaire.

---

Étape 6 – Vérifier le résultat

Tester le service Nginx :

curl http://localhost

Ou vérifier le statut du service :

systemctl status nginx

---

Résultat attendu

- Nginx est installé automatiquement
- Le service est démarré et activé au démarrage
- La page par défaut Nginx est accessible depuis le serveur local

---

Compétences démontrées

- Ansible (inventaire, playbooks, modules apt et service)
- Automatisation système Linux
- Exécution non interactive
- Gestion des privilèges sudo
