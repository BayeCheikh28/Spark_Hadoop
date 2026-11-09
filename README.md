# Étude de cas : ventes et livraisons

Exercice d'analyse de données avec PySpark : chargement, nettoyage, jointures,
fenêtrage, agrégations et data visualisation sur un jeu de données de commandes
et de livraisons (ventes en ligne, flotte de véhicules, traces GPS).

## Contenu

- `notebooks/exercice_livraisons.ipynb` : le notebook principal, avec toutes les
  réponses aux questions (sections 1 à 11), déjà exécuté.
- `data/` : jeu de données fourni (non versionné, voir `.gitignore` — volumineux).
- `conf/` : configuration Spark (`spark-defaults.conf`, `log4j2.properties`).
- `docker/` : image Docker Spark + JupyterLab + librairies Python.
- `docker-compose.yml` : orchestration des services (Spark, Jupyter, MongoDB).
- `resultats/` : graphiques et cartes générés par le notebook (non versionnés).

## Lancer l'environnement

```bash
docker compose up -d jupyter mongo
```

JupyterLab est disponible sur http://localhost:8888 (pas de token).

Le notebook utilise une session Spark locale (`local[2]`) pour rester
compatible avec des machines à ressources limitées. Les services
`spark-master` / `spark-worker` / `spark-history` restent disponibles dans
le `docker-compose.yml` si l'on souhaite exécuter sur un vrai cluster Spark
(il suffit alors de changer `.master("local[2]")` en
`.master("spark://spark-master:7077")` dans la première cellule du notebook,
et de lancer `docker compose up -d` sans restriction de services).

## Exécuter le notebook en ligne de commande

```bash
docker exec commandes-jupyter-1 bash -c \
  "cd /work/notebooks && jupyter nbconvert --to notebook --execute --inplace \
   exercice_livraisons.ipynb --ExecutePreprocessor.timeout=600"
```
