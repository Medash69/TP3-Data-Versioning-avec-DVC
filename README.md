# TP3 : Data Versioning avec DVC

## Objectif
Ce TP a pour but de :

- Versionner le dataset `iris.csv` avec DVC.
- Utiliser MinIO comme remote S3 local pour stocker les blobs.
- Assurer la reproductibilité des données sur n’importe quelle machine.



## Commandes DVC utilisées

| Action | Commande |
|--------|----------|
| Initialiser le dépôt DVC | `dvc init` |
| Suivre le fichier CSV avec DVC | `dvc add data/raw/iris.csv` |
| Versionner les pointeurs DVC (.dvc files) dans Git | `git add .` / `git commit -m "Track iris.csv with DVC"` |
| Définir le remote S3 local | `dvc remote add -d storage s3://mlops-dvc` |
| Pointer vers MinIO local | `dvc remote modify storage endpointurl http://localhost:9000` |
| Désactiver SSL pour MinIO local | `dvc remote modify storage use_ssl false` |
| Définir la clé d’accès MinIO | `dvc remote modify storage access_key_id minio` |
| Définir le secret MinIO | `dvc remote modify storage secret_access_key minio12345` |
| Envoyer les blobs DVC vers MinIO | `dvc push` |
| Récupérer les données depuis le remote | `dvc pull` |
| Vérifier l’état local | `dvc status` |
| Vérifier la synchronisation avec le remote | `dvc status --cloud` |

> Pour ce TP, le pipeline `train` a été supprimé car le script `train.py` n’est pas fourni.

---

## Reproductibilité

- Les fichiers `.dvc` permettent de récupérer le dataset sur n’importe quelle machine avec :

```bash
dvc pull

