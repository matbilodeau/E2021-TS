# Installation

L'application peut être déployée de deux façons:


1. **À partir d'images pré-construites**


Des images publiques seront utilisées pour déployer l'application.

2. **À partir du code source**


Vous construirez vous-même les images et les publierez vers un repository. Ces images seront utilisées pour déployer l'application.


## Préparation

   - Un cluster GKE doit être configuré pour recevoir le déploiement.
   ```sh
   gcloud container clusters create boutique --enable-autoupgrade \
       --enable-autoscaling --min-nodes=3 --max-nodes=10 --num-nodes=5 --zone=us-east1-b
   ```

### Option 1: À partir d'images pré-construites
Assurez-vous que le service GCP suivant est bien activé.

`gcloud services enable container.googleapis.com`

À partir d'une copie locale de ce repository, exécutez `kubectl apply -f ./release/kubernetes-manifests.yaml` pour déployer l'application.


### Option 2: À partir du code source
Assurez-vous que les services GCP suivants sont bien activés.

```sh
gcloud services enable container.googleapis.com
gcloud services enable cloudprofiler.googleapis.com
gcloud services enable containerregistry.googleapis.com
gcloud auth configure-docker -q
```
À partir d'une copie locale de ce repository, exécutez `skaffold run --default-repo=gcr.io/[PROJECT_ID]` en utilisant votre ID de projet GCP.

[skaffold]( https://skaffold.dev/docs/install/) est un utilitaire qui permet de construire et publier les images de container puis de déployer l'application. Assurez-vous qu'il est bien installé.

**Alternative:** Il est également possible de construire les images via [Google Cloud Build](https://cloud.google.com/build?hl=fr).
    Utilisez la commande suivante `skaffold run -p gcb --default-repo=gcr.io/[PROJECT_ID]` après [avoir activé l'API](https://console.cloud.google.com/flows/enableapi?apiid=cloudbuild.googleapis.com).

### Nettoyage

Si l'application a été déployée avec l'option 1, exécutez  `kubectl delete -f ./release/kubernetes-manifests.yaml` pour supprimer le déploiement.

Si l'application a été déployée avec l'option 2, exécutez  `skaffold delete` pour supprimer le déploiement. Vous pouvez également supprimer les images hébergées sur GCR et le _Storage Bucket_ créé par skaffold.

Pour supprimer le cluster GKE, exécutez `gcloud container clusters delete boutique  --zone=us-east1-b`
