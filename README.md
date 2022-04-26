# Sellor-front

## Projet : Logiciel Adaptatif 

## Build Setup

```bash
# installer dependences
$ npm install

# serveur lancé sur localhost:3000
$ npm run dev

# build pour la production et lancer le serveur
$ npm run build
$ npm run start

# générer le projet static 
$ npm run generate
```

## Fonctionnalités du Front-end

Interface permettant de commander différents produits. 

### `Authentification`
Une Authentification est mise en place permettant de s'inscrire, se connecter et de se connecter.
La connection est obligatoire pour pouvoir commander les produits.

### `Produits`
Récupération des différents produits présent dans la base de données.  
Le choix de la quantité est possible dans la limite des stocks disponibles. 

### `Panier`
Quand le choix des produits est effectués, la commande peut être finaliser dans le panier avec le récapitulatif de vos achats avec leurs quantités. 

### `Compte`
Une page compte est disponible pour modifier les paramètres du compte. 
