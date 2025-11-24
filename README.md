# TP3 : Data Versioning avec DVC

## Objectif
Versionner le dataset `iris.csv` avec DVC, utiliser MinIO comme remote S3 local et assurer la reproductibilité.

## Structure du projet
mlops-dvc-iris/
├─ data/raw/iris.csv # Dataset suivi par DVC
├─ .dvc/ # Configuration DVC
├─ dvc.yaml # Pipelines DVC (supprimé pour TP3)
└─ README.md


## Commandes DVC utilisées

 | Initialiser le repo DVC |
 `dvc init` 
 | Suivre le fichier CSV avec DVC |
 `dvc add data/raw/iris.csv` 
 | Versionner les pointeurs DVC (.dvc files) dans Git |
 `git add` / `git commit` 
 | Définir le remote S3 local |
 `dvc remote add -d storage s3://mlops-dvc` 
 | Pointer vers MinIO local |
 `dvc remote modify storage endpointurl http://localhost:9000` 
 | Pas de SSL pour MinIO local |
 `dvc remote modify storage use_ssl false` 
 | Clé d’accès MinIO |
 `dvc remote modify storage access_key_id minio` 
 | Secret MinIO |
 `dvc remote modify storage secret_access_key minio12345` 
 | Envoyer les blobs DVC vers MinIO |
 `dvc push` 
 | Récupérer les données depuis le remote |
 `dvc pull` 
 | Vérifier l’état local |
 `dvc status` 
 | Vérifier la synchronisation avec le remote |
 `dvc status --cloud` 

> Pour ce TP, le pipeline `train` a été supprimé car le script `train.py` n’est pas fourni.

## Reproductibilité
- Les fichiers `.dvc` permettent de récupérer le dataset sur n’importe quelle machine avec `dvc pull`.
