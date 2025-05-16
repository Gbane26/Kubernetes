# Etherpad Kubernetes Helm Chart
Ce projet déploie une instance Etherpad avec une base de données PostgreSQL, des sauvegardes automatisées et un accès via Ingress, le tout paramétrable via Helm.

Prérequis
Un cluster Kubernetes fonctionnel (Minikube, Kind, ou cloud)

kubectl installé et configuré pour ton cluster

Helm 3 installé sur ta machine

Structure du projet
```text
Kubernetes/
  Chart.yaml
  values.yaml
  templates/
    postgres-secret.yaml
    postgres-statefulset.yaml
    postgres-service.yaml
    etherpad-secret.yaml
    etherpad-pvc.yaml
    etherpad-deployment.yaml
    etherpad-service.yaml
    etherpad-ingress.yaml
    postgres-backup-pvc.yaml
    postgres-backup-cronjob.yaml
    etherpad-backup-pvc.yaml
    etherpad-archive-cronjob.yaml
````
Paramétrage
Tu peux personnaliser les paramètres principaux dans le fichier values.yaml (utilisateurs, mots de passe, nom de la base, taille des volumes, nom d’hôte d’Ingress, etc.).

Installation
Cloner le projet ou copier le dossier Kubernetes/

Se placer dans le dossier parent de Kubernetes/

bash
cd /chemin/vers/ton/projet
Installer le chart avec Helm

bash
helm install mon-etherpad ./Kubernetes
Tu peux personnaliser les valeurs à l’installation avec --set ou en modifiant values.yaml.

Vérifier le déploiement

bash
kubectl get all
kubectl get ingress

Accéder à Etherpad

Récupère le nom d’hôte configuré dans values.yaml (par défaut, etherpad.local).

Si tu utilises Minikube, expose l’Ingress ou ajoute l’IP de Minikube dans ton /etc/hosts :

text
sudo echo "$(minikube ip) etherpad.local" | sudo tee -a /etc/hosts
Ouvre ensuite http://etherpad.local:9001 dans ton navigateur.

Sauvegardes automatisées
Backup PostgreSQL : un dump est réalisé chaque jour à 02h00 dans un volume dédié.

Archive Etherpad : une archive du dossier de données Etherpad est créée chaque jour à 03h00 dans un autre volume.


Ce projet te permet de déployer rapidement un Etherpad prêt à l’emploi, sauvegardé et personnalisable, sur n’importe quel cluster Kubernetes grâce à Helm.