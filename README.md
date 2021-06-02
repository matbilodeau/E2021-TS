# Démonstration microservices

## Contenu
Une application _cloud-native_ composée de microservices qui simule un site web transactionnel.
Le visiteur peut explorer les produits, les ajouter à son panier puis procéder à un "achat".

## Utilisation
**Cette application ne doit être utilisée que pour des fins de démonstration.**

## Pré-requis
Un compte [Google Cloud Platform](https://cloud.google.com/).

## Installation
Un fichier contenant les [instructions](./Installation.md) est disponible.


## Architecture

| Service                                              | Description                                                                                                                       |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [Interface Client](./src/frontend)                   | Interface web de base. Génère un ID de session automatiquement.                                                                   |
| [Panier d'achats](./src/cartservice)                 | Stocke les produits choisis.                                                                                                      |
| [Catalogue](./src/productcatalogservice)             | Fourni la liste des produits disponibles.                                                                                         |
| [Taux de change](./src/currencyservice)              | SIMULATION - Conversion de devises.                                                                                               |
| [Paiement](./src/paymentservice)                     | SIMULATION - Valide un # fourni comme carte de paiement et fourni un ID de transaction si le "paiement" est accepté.              |
| [Expédition](./src/shippingservice)                  | SIMULATION - Calcul un coût d'expedition. Fourni un ID de repérage.                                                               |
| [Confirmation](./src/emailservice)                   | SIMULATION - Transmet un courriel de confirmation de commande.                                                                    |
| [Commis Caissier](./src/checkoutservice)             | Récupère les données du panier afin de préparer le paiement de la commande, l'expédition et le courriel de confirmation.          |
| [Recommandation](./src/recommendationservice)        | Recommandation de produits selon le contenu du panier.                                                                            |
| [Pubilicité](./src/adservice)                        | Fourni une publicité textuelle à afficher au visiteur.                                                                            |


La communication entre les services est assurée par gRPC. La description des buffers de protocole est disponible dans le [dossier `./pb`](./pb).

Un [générateur de charge](./src/loadgenerator) est également offert pour simuler des requêtes.
