# 🛠️ devops-lab

Projet DevOps complet démontrant le déploiement, l'orchestration, l'automatisation
et le monitoring d'une application web Nginx dans un environnement Linux.

---

## 📌 Présentation du projet

**devops-lab** est un projet de démonstration DevOps visant à mettre en place
une stack web reproductible et automatisée, en utilisant les principaux outils du métier.

Le projet couvre :

- Le déploiement avec Docker
- L'orchestration avec Kubernetes (Minikube)
- L'automatisation avec Ansible
- Le monitoring avec Prometheus

---

## 🎯 Objectif

Mettre en œuvre une stack web simple, automatisée et observable dans un environnement
Linux (Debian / WSL), en suivant une démarche DevOps de bout en bout.

---

## 🧱 Architecture (Docker)
```
Client → Nginx (conteneur Docker) → Port 8080
```

---

## 🛠️ Technologies utilisées

- Linux (Debian – WSL)
- Docker & Docker Compose
- Kubernetes (Minikube)
- Ansible
- Prometheus
- Nginx

---

## 📂 Structure du projet
```text
devops-lab
├── .github/workflows/       # CI pipeline GitHub Actions
├── ansible/
│   ├── inventory/
│   │   └── hosts.ini
│   └── playbooks/
│       └── install_nginx.yml
├── k8s/
│   └── nginx.yaml
├── monitoring/
│   ├── docker-compose.monitoring.yml
│   └── prometheus/
│       └── prometheus.yml
├── nginx/
├── docker-compose.yml
└── README.md
```

---

## 🚀 Déploiement Docker

**Étape 1 – Cloner le repository**
```bash
git clone https://github.com/YOSO98/devops-lab.git
cd devops-lab
```

**Étape 2 – Lancer la stack**
```bash
docker compose up -d
```

**Étape 3 – Vérifier les conteneurs**
```bash
docker ps
```

**Étape 4 – Tester le service**
```bash
curl http://localhost:8080
```

Ou dans un navigateur : http://localhost:8080

✅ Résultat attendu : page d'accueil Nginx affichée, service accessible depuis la machine hôte.

---

## ☸️ Déploiement Kubernetes (Minikube)

**Étape 1 – Démarrer Minikube**
```bash
minikube start --driver=docker
```

**Étape 2 – Déployer Nginx**
```bash
kubectl apply -f k8s/nginx.yaml
```

**Étape 3 – Vérifier les ressources**
```bash
kubectl get pods
kubectl get svc
```

**Étape 4 – Accéder au service**
```bash
kubectl port-forward svc/nginx-service 8081:80
```

Navigateur : http://localhost:8081

✅ Résultat attendu : pod en état `Running`, service accessible via port-forward.

---

## 🤖 Automatisation avec Ansible

**Étape 1 – Inventaire** (`ansible/inventory/hosts.ini`)
```ini
[local]
localhost ansible_connection=local
```

**Étape 2 – Playbook** (`ansible/playbooks/install_nginx.yml`)
```yaml
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
```

**Étape 3 – Configuration sudo sans mot de passe**
```bash
sudo visudo
```

Ajouter à la fin du fichier :
```
debian ALL=(ALL) NOPASSWD: ALL
```

> ⚠️ Configuration réservée à un environnement de laboratoire / développement.

**Étape 4 – Exécuter le playbook**
```bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/install_nginx.yml
```

**Étape 5 – Vérification**
```bash
curl http://localhost
```

✅ Résultat attendu : Nginx installé automatiquement, service démarré et activé au boot.

---

## 📊 Monitoring avec Prometheus

**Étape 1 – Lancer Prometheus**
```bash
docker compose -f monitoring/docker-compose.monitoring.yml up -d
```

**Étape 2 – Vérifier les conteneurs**
```bash
docker ps
```

**Étape 3 – Accéder à Prometheus**

Navigateur : http://localhost:9090

**Étape 4 – Vérifier les targets**

Dans l'interface Prometheus : `Status → Targets`

✅ Les services doivent apparaître en état `UP`.

---

## 🧠 Compétences démontrées

- Docker & Docker Compose
- Kubernetes (Deployment, Service)
- Ansible (inventaire, playbooks, automatisation)
- Linux et gestion des privilèges
- Monitoring avec Prometheus
- Démarche DevOps complète et reproductible

---

## 🏁 Conclusion

Ce projet constitue un portfolio DevOps structuré, automatisé et professionnel,
démontrant des compétences techniques directement applicables en environnement réel.

---

## 👤 Auteur

**Youssouf Souleyman**  
GitHub : [https://github.com/YOSO98](https://github.com/YOSO98)
