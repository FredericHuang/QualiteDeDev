# Qualité de développement

Le but de ce cours est de faire des tests d'intégration au fur et à mesure que des nouveaux composants sont intégrés dans une apllication 
tout en vérifiant que les tests précédents continuent de passer sans relever d'erreur. 
On appelle cela des tests de non regression.

# TD 1 (première séance)

Etude du framework de test inclus dans les projets Spring boot : https://github.com/charroux/springbootest

Etude du framework de test Mockito: https://github.com/charroux/mockito

# TP 1 (première séance)

## Présentation de l'application

L'application à développer contient : 

- une base de données.
- un service Web

L'application est programmée en Java avec le framework Spring Boot (pour faciliter l'accès à la base de données ainsi 
que le développement du service web).

Le but de l'application est de faire des statistiques sur des voitures.

## Récupération du projet
```
git clone https://github.com/charroux/qualiteDeDeveloppement
```
## Clonage du projet dans un dépôt git qui vous appartient

Durant les TP vous allez travailler en binôme. Créez un dépôt de code public mais vide dans Github (sans Readme, ni gitignore),
puis recopier ce projet dans votre dépôt git en prodédant comme suit :
```
rm -rf .git
git init
git add *
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/[adresse .git de votre projet]
git push -u origin main
```
Si le push échoue à cause d'un problème d'authentification, il faut créer un "token" sur le site de Github et ensuite faire le push.

## Edition du projet

### Avec Intellij

Lancer Intellij et ouvrir tout simplement le projet.

### Avec Eclipse 

Attention, c'est la version JEE developpeur qu'il faut utiliser.

Importer le projet en choisissant "import gradle project".

## Configuration de l'application

A l'IUT, le traffic réseau passe par un proxy. Il faut donc décommenter le fichier de configuration : 

https://github.com/charroux/qualiteDeDeveloppement/blob/main/gradle.properties

## Création des packages 

Créer 3 sous-packages au package com.example.demo:
- data   
- service 
- web

Data va contenir les classes dont les instances vont être sauvegardées dans la base de données, service les traitements des données et web le Web service.  
## Codage des classes de données, accès à la base de données

### Codage d'une classe Voiture

Créer une classe appelée Voiture dans le package data du projet. Cette classe doit contenir :
 - une marque
 - un prix
 - un identifiant appelé id de type int (qui va servir de clef primaire à la table Voiture dans la base de doonées)

### Tests unitaires de la classe Voiture
Le dossier src/test/java contient déjà l'ébauche de la classe de test de la voiture. 
Cette classe de test est appelée VoitureTest. Ajoutez à cette classe autant de méthodes que vous jugez utile pour 
tester la classe Voiture. Vérifiez que les méthodes de la classe Voiture retournent les résultats attendus en utilisant la classe Assert du framework Spring dont voici la documentation :

https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/Assert.html

Vous pouvez exécuter les tests via un clic droit sur le programme de test ou en ligne de commande en faisant :

Sous Linux :
```
./gradlew build
```

### Accès à la base de données
La base de données est HSQLDB. Elle s'exécute "En mémoire" pour ne pas avoir à démarrer un serveur de base de données tant qu'on est en mode développement.
En conséquence, les données sont perdues dès que l'application s'arrête.

Pour permettre d'accéder par programmation à la base de données vous devez simplement créer uns interface dans le même package que la classe Voiture : 

``` Java
package com.example.demo.data;

import org.springframework.data.repository.CrudRepository;

public interface VoitureRepository extends CrudRepository<Voiture, Integer> {
}
```

### Tests de l'accès à la base de données
Le dossier src/test/java (package data) contient aussi l'ébauche du programme de test de la base de données (BaseDeDonneesTests.java).
Ajoutez à cette classe autant de méthodes que vous jugez utile pour
tester l'accès à la base de données. Testez que la base de données contient bien les bons éléments en utilsant le framework Mockito dont voici l'aide :

https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html

# TP 2 (deuxième séance) : codage de la classe de service qui intègre la base de données
A suivre...
