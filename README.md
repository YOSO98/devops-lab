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
