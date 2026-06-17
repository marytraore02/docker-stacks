Ollama Stack
===============

But
----
Ce dossier contient un exemple réutilisable pour démarrer le service Ollama et son UI `open-webui` dans un environnement Docker Compose.

Services
--------
- `ollama` : serveur Ollama exposé sur le port `11434`.
- `open-webui` : interface web qui se connecte à Ollama (exposée sur `3001` dans l'exemple).

Ports exposés
-------------
- Ollama API : `11434`
- Open Web UI : `3001` (mappe le port 8080 interne)

Prérequis
---------
- Docker et Docker Compose (plugin `docker compose`) installés.
- Un réseau Docker partagé nommé `shared_network_local` si vous utilisez la configuration réseau externe (voir `docker network ls`).

Exécution (exemple sans monter de dossier local)
----------------------------------------------
Ce dépôt fournit `docker-compose.example.yml` qui utilise un volume nommé pour stocker les données. Pour démarrer :

```bash
docker compose -f stacks/ollama/docker-compose.example.yml up -d
```

Si vous préférez utiliser le montage local d'origine (répertoire `ollama-data/`), copiez `docker-compose.example.yml` en `docker-compose.yml` et modifiez la section `volumes` du service `ollama` en `- ./ollama-data:/root/.ollama`.

ATTENTION
---------
ATTENTION A NE PAS MODIFIER LES CODES INTERNES DES DIFFERENTS FICHER CONFIG POUR LE FONCTIONNEMENT DES SERVICES DOKCER

Bonnes pratiques avant de pusher
--------------------------------
- Ne commitez jamais les dossiers de données locaux (ex. `ollama-data/`). Ajoutez-les à `.gitignore` au niveau du dépôt racine.
- Si vous utilisez un réseau externe (`shared_network_local`), documentez la commande pour le créer : `docker network create shared_network_local`.

Fichiers fournis
----------------
- `docker-compose.example.yml` : compose nettoyé et prêt à être utilisé (sans montages host sensibles).

Support
-------
Ouvrez une issue si vous voulez que j'ajoute un script `start-stack.sh`/`stop-stack.sh` ou un `.env.example` pour ce stack.
