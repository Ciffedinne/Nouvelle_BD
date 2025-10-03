# Guide d'installation sur les machines personnelles

Les méthodes d'installations recommandées utilisent docker.

## MongoDB

### Installer MongoDB par docker 
1. Télécharger Docker Desktop et l'installer: https://docs.docker.com/desktop/
2. Lancer Docker Desktop (cela lance le deamon docker en service de fond - background service)
3. Ouvrir le terminal
4. Taper cette commande dans le terminal
```
docker run --name mongodb -d -p 27017:27017 mongodb/mongodb-community-server:latest
```
Cela télécharge l'image docker de mongdb et crée un container au nom de `mongodb`. Le serveur mongodb écoutera le port 27017
5. Vérifier les containers docker en cours d'exécution en tapant la commande suivante dans le terminal
```
docker ps
```
6. Vérifier les containers dockers disponibles en tapant la commande suivante dans le terminal
```
docker ps -a
```
`-a` signifie `all`
7. Si le container `mongodb` n'est pas en cours d'exécution, vous pouvez le lancer en tapant dans le terminal
```
docker start mongodb
```
8. Vous pouvez arrêter le container en tapant dans le terminal
```
docker stop mongodb
```
9. Si vous souhaitez supprimer le container, tapez dans le terminal
```
docker stop mongodb && docker rm mongodb
```
10. Installez l'interface graphique de MongoDB, nommée Mongo Compass : https://www.mongodb.com/products/tools/compass 

### Utiliser MongoDB via docker

#### Par terminal Mongo Shell (mongosh)
Comme la commande `mongosh`est diponible que dans le container nous pouvons la lancer comme ceci :
```
docker exec -it mongodb mongosh
```
Ce qui signgifie `exec`(executer) `-it` (interactive terminal) `mongodb` (le nom du container pour lancer le terminal interactif) `mongosh` (dans ce terminal interactif je lance la commande `mongosh`)

#### Par client Python (pymongo)
1. installez pymongo
```
pip install pymongo
```
Si vous êtes sous Unix, il est possible que deviez ajouter ceci :
```
pip install pymongo --break-system-packages
```
2. connectez-vous à votre serveur mongodb par son port (27017 donc)
```
import pymongo
myclient = pymongo.MongoClient("mongodb://localhost:27017/")
```

Et voilà ! Vous êtes prêt(e) !

Utilisez les documentations suivantes :
- doc mongodb (par `mongosh`) : https://www.mongodb.com/docs/mongodb-shell/
- doc mongodb (module Python) : https://www.mongodb.com/docs/languages/python/pymongo-driver/current/

## Redis

### Installer Redis par Docker

Redis, et en l'occurence Redis Stack est un ensemble de composants dont l'installation recommandée est par docker.

1. Télécharger Docker Desktop et l'installer: https://docs.docker.com/desktop/
2. Lancer Docker Desktop (cela lance le deamon docker en service de fond - background service)
3. Ouvrir le terminal
4. Taper cette commande dans le terminal
```
docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest
```
Cela télécharge l'image docker de redis stack et crée un container au nom de `redis-stack`. Le serveur redis écoutera le port 6379, tandis que son interface graphique, nommée Redis Insights sera disponible sur le port 8001.
5. Vérifier les containers docker en cours d'exécution en tapant la commande suivante dans le terminal
```
docker ps
```
6. Vérifier les containers dockers disponibles en tapant la commande suivante dans le terminal
```
docker ps -a
```
`-a` signifie `all`
7. Si le container `redis-stack` n'est pas en cours d'exécution, vous pouvez le lancer en tapant dans le terminal
```
docker start redis-stack
```
8. Vous pouvez arrêter le container en tapant dans le terminal
```
docker stop redis-stack
```
9. Si vous souhaitez supprimer le container, tapez dans le terminal
```
docker stop redis-stack && docker rm redis-stack
```

### Utiliser Redis via docker

#### Par terminal Redis Command Line Interface (redis-cli)
Comme la commande `redis-cli` est diponible que dans le container nous pouvons la lancer comme ceci :
```
docker exec -it redis-stack redis-cli
```
Ce qui signgifie `exec`(executer) `-it` (interactive terminal) `redis-stack` (le nom du container pour lancer le terminal interactif) `redis-cli` (dans ce terminal interactif je lance la commande `redis-cli`)

#### Par client Python (redis)
1. installez 
```
pip install redis
```
Si vous êtes sous Unix, il est possible que deviez ajouter ceci :
```
pip install redis --break-system-packages
```
2. connectez-vous à votre serveur mongodb par son port (27017 donc)
```
import redis
r = redis.Redis(host='localhost', port=6379)
```

Et voilà ! Vous êtes prêt(e) !

Utilisez les documentations suivantes :
- doc redis (par `redis-cli`) : https://redis.io/docs/latest/develop/tools/cli/
- doc redis (module Python) : https://redis.io/docs/latest/develop/clients/redis-py/

De manière optionnelle, sachez qu'il y a une extension pour redis dans VSCode : https://redis.io/docs/latest/develop/tools/redis-for-vscode/

