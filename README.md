# 🚀 TME CI/CD - Intégration Continue & Déploiement Continu

Ce projet consiste à mettre en place un **pipeline CI/CD** en utilisant **GitHub Actions**, **Docker**, **Docker Hub** et **Kubernetes avec Kind** pour automatiser l'intégration et le déploiement d'une application.

---

## 📌 Déroulement du TP

### 1️⃣ Dépôt Git et gestion du code  
Nous avons commencé par initialiser un dépôt Git pour versionner notre projet et permettre son suivi sur GitHub. Cela nous a permis d'intégrer un **workflow GitHub Actions**, qui est déclenché à chaque mise à jour du code. L'objectif était d'automatiser la construction et le déploiement de notre application.  

### 2️⃣ Construction et publication de l’image Docker  
L'application a été conteneurisée à l'aide de **Docker**. Après avoir rédigé un **Dockerfile**, nous avons construit une image que nous avons ensuite envoyée sur **Docker Hub** pour qu'elle puisse être utilisée dans notre cluster Kubernetes.  
Nous avons rencontré quelques difficultés avec le push de l’image, notamment des problèmes d'authentification et de version des images.  

### 3️⃣ Déploiement Kubernetes avec Kind  
Plutôt que d’utiliser **Minikube**, nous avons opté pour **Kind** afin de gérer notre cluster Kubernetes directement dans des conteneurs Docker.  
Une fois le cluster créé, nous avons déployé notre application à l’aide de fichiers **YAML** définissant le **Deployment** et le **Service** Kubernetes.  
L'un des problèmes majeurs rencontrés concernait l'erreur `ImagePullBackOff`, où Kubernetes ne parvenait pas à récupérer l’image stockée sur Docker Hub. Nous avons dû reconfigurer les permissions et vérifier l’accessibilité du registre Docker.  

### 4️⃣ Début de mise en place d'un Runner GitHub Actions auto-hébergé  
Nous avons ensuite tenté d’intégrer un **Runner GitHub Actions auto-hébergé** pour exécuter nos workflows sur notre propre machine plutôt que sur un serveur GitHub.  
Cependant, nous avons rencontré des erreurs lors du téléchargement du fichier du runner, notamment un problème de **checksum invalide**, ce qui a empêché sa configuration correcte. Ce point reste à finaliser.  

---

## 🚧 Problèmes rencontrés et axes d’amélioration  

- **Problème d'authentification Docker Hub** empêchant le pull de l’image ( Problèmes avec Docker et le push vers Docker Hub).  
- **Erreur ImagePullBackOff** dans Kubernetes nécessitant des vérifications de configuration.  
- **Service LoadBalancer non accessible** sur Kind, nécessitant un autre mode d'exposition.
- **Ordre d'execution des etapes dans le dossier cy.yml**, ce qui empêche le bon déroulement dans actions.  
- **Échec de l'installation du Runner GitHub Actions**, ce qui empêche l’exécution en local.  
- **Github secret** Valeur de kubeconfig devait etre en base64 
- **Erreur de version Kubernetes avec Kind** Nous avons voulu exécuter le pipeline en local via un Runner GitHub Actions auto-hébergé, mais l'installation a échoué.
- **Échec du premier kubectl apply -f deployment.yaml** Le fichier deployment.yaml ne créait pas les ressources correctement.
  
---

Quelques captures

![image](https://github.com/user-attachments/assets/80da0c30-2ff9-4334-938d-9d113341b9f0)

Build et Deployement

![image](https://github.com/user-attachments/assets/4d701272-971a-45b2-b102-7c21b94894fe)

Process du Build

![image](https://github.com/user-attachments/assets/6cc7630c-3aff-40e6-b328-732f0f48d1fc)

Process du Deployment

---
## ✅ Conclusion  

Malgré plusieurs blocages techniques, nous avons réussi à mettre en place un **pipeline CI/CD** opérationnel incluant le **build**, le **push** et le **déploiement** de l'application.  
Les prochaines étapes consisteront à finaliser l’utilisation du **Runner GitHub Actions auto-hébergé**.

📌 **Projet réalisé dans le cadre du TME CI/CD**  
📌 **Auteur : @shyamsubrun**   
📌 **Encadré par alfreddeiva**
