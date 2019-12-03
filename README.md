# tuto-jenkins

Mes notes concernant le [tutoriel docker/jenkins](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/)

Attention, il y aura besoin d'avoir docker d'installé & de plusieurs terminaux.

## 1 / Lancer le docker Jenkins

Lancer le docker avec un nom de machine, puis recup le code dans les fichiers.

Dans le premier terminal (ca tourne sous node si sous windows..)

```
docker run ^
  --rm ^
  -u root ^
  -p 8082:8080 ^
  -v jenkins-data:/var/jenkins_home ^
  -v /var/run/docker.sock:/var/run/docker.sock ^
  -v "%HOMEDRIVE%%HOMEPATH%":/home ^
  --name jenkins-tutorials ^
  jenkinsci/blueocean
```

Attention, il s'agit de la commande de base du tuto MAIS avec un nom 'jenkins-tutorial' de spécifié.

Attention, derrière -p, vous pouvez changer le port si il est déjà occupé, mais cela modifiera l'adresse à aller voir dans le navigateur.

Attention, il faut donner l'autorisation a la fois a windows ET a docker d'accéder au bousin.

## 2 / Site en local

Dans le navigateur : [http://localhost:8082/](http://localhost:8082/)

Un code est demandé afin de finaliser le lancement de jenkins. C'est censé apparaitre dans le bash mais si ça ne s'affiche pas..

## 3 / Accéder à l'image du docker

Ouvrir un 2eme terminal

```
docker exec -it jenkins-tutorials bash
cd var/jenkins_home/secrets/
vi initialAdminPassword
```

Récupérer le mot de passe, et l'injecter dans le formulaire du navigateur.

Finir de remplir le formulaire (mettre "dev" partout en utilisateur/pass)

## 4 / Tester, tout ça

Pas de problème particulier avec le reste du tuto.

Ne pas oublier de git add/commit si en dehors du container (avant de relancer le _pipeline_).

Si modification directe depuis le container (2eme terminal > home/simple-node-js-react-npm-app/src/App.js), il y a un genre de HMR (si le pipeline de test est toujours en cours.
