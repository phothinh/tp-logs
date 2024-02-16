# Activité 3 - Manipulation de logs

## Mot de passe Graphana

```
Henrilepetit
```

## 1. Qu’est ce que Loki ?

Loki est un système d'agrégation de journaux (logs) conçu pour être hautement évolutif et rentable. Il est optimisé pour les infrastructures conteneurisées et utilise un modèle de stockage inspiré de Prometheus.

## 2. Quelles sont les différentes composantes de la stack Loki fournie ?

- Read
- Write
- Promtail
- Minio
- Gateway
- Flog

## 3. À quoi servent chacune des composantes ? 

- Read :
    - Fournit une interface pour récupérer les journaux stockés dans Loki
- Write :
    - Reçoit et stocke les journaux provenant de différentes sources
- Promtail :
    - Collecte les journaux locaux, les formate et les envoie à Loki
- Minio
    - Stocke les données de journaux de Loki de manière persistante. Loki utilise Minio comme backend de stockage.
- Gateway
    - Fournit une interface unifiée pour interroger les services Read et Write de Loki. Redirige les requêtes vers le service approprié en fonction du chemin de l'URL
- Flog
    - Produit des journaux simulés pour tester le fonctionnement du système d'agrégation de journaux

## 4. Qu’est-ce que Minio ? 

Minio est un serveur de stockage d'objets open source qui a été conçu pour être compatible avec l'API Amazon S3 (Simple Storage Service). Il offre un moyen de stocker et de récupérer des données non structurées, telles que des fichiers, des images, des vidéos ou d'autres types de données binaires, via une interface HTTP RESTful.

## 5. Réalisez un schéma (à mettre dans le dossier partie1 du repo) du flux de données entre le moment où un log est écrit dans docker jusqu’au moment où il est visible dans grafana.

![image](https://github.com/phothinh/tp-logs/assets/66186125/e5d596f6-ecc5-4c6a-9101-8d6f0844d80d)

## 6. À quoi sert le service gateway ?

Le service gateway fonctionne comme une interface unifiée pour les services read et write de Loki, simplifiant ainsi l'accès aux fonctionnalités de Loki.

## 7. L’application a une structure de logs plutôt constante, quels champs sont contenus dans les logs ? Quelle données représentent-il?

1. **`evt`:** Le type d'événement qui s'est produit. Il représente l'action spécifique effectuée dans l'application
2. **`level`:** Niveau de gravité du log
3. **`msg`:** Un message décrivant l'événement ou l'action qui s'est produit
4. **`time`:** Horodatage indiquant quand l'événement s'est produit
5. **`uuid`:** Identifiant unique associé à chaque événement. Il est utilisé pour suivre de manière unique chaque occurrence d'événement
6. **`name`:** Nom associé à certains événements, comme le nom du produit dans le cas de "product.remove" ou "product.add".
7. **`product`:** Identifiant unique du produit associé à certains événements, comme "product.remove" ou "product.add".
8. **`stocks`:** La quantité de stocks associée à un produit dans certains événements, indiquant probablement la disponibilité du produit.
9. **`device`:** Information sur le dispositif ou le navigateur, tel que "chrome-101", associé à certains événements tels que "login.failure".

## 8. Qu’est-ce qui doit être configuré du coté de la stack loki pour récolter les logs ? 

- Avoir les fichiers de configuration de Promtail et de Loki
- Les volumes nécessaires sont montés
- Loki, Promtail, Minio sont bien configurés et en cours d’execution

## 9. Dans l’onglet “explorer”, quelle requête permet d’avoir :
### le volume de logs par couleur

```
count_over_time({job="promtail", color=~".+"}[5m])
```

### Filtrer les resultats pour un utilisateur

```
{job="promtail", color=~".+"} |~ "user=<nom_utilisateur>"
```

## 11. Qu’est-ce qu’elasticsearch ? 

Elasticsearch est un moteur de recherche et d'analyse de données distribué.

## 12. À quoi sert elasticsearch ? 

Elasticsearch est utilisé pour indexer, rechercher et analyser des données à grande échelle, offrant des fonctionnalités de recherche avancées et des capacités d'analyse.

## 13. Qu’est ce que Kibana ? Sur quel port accéder à Kibana ?

Kibana est une interface utilisateur permettant de visualiser et d'explorer les données stockées dans Elasticsearch. On accède à Kibana généralement via le port 5601.

## 14. Qu’est-ce qu’un index Elasticsearch ? 

Un index Elasticsearch est une collection de documents qui partagent une structure similaire et sont stockés de manière optimisée pour la recherche et l'analyse.

## 15. Qu’est-ce que Lucene ? Quel est son rapport avec Elasticsearch ? 

Lucene est une bibliothèque de recherche open source. Elasticsearch utilise Lucene en tant que moteur de recherche sous-jacent, fournissant des fonctionnalités de recherche avancées et une indexation efficace des données.

## 16. Qu’est-ce que Filebeat ?

Filebeat est un agent léger développé par Elastic, conçu pour envoyer des logs d'événements à Elasticsearch ou à Logstash à partir de fichiers, de répertoires ou de modules spécifiques.

## 17. Quels autres “beats” existent ?

- **Metricbeat :** Pour collecter et envoyer des métriques du système et des services.
- **Packetbeat :** Pour analyser le trafic réseau et extraire des informations sur les protocoles.
- **Winlogbeat :** Pour collecter des logs d'événements Windows.
- **Heartbeat :** Pour surveiller la disponibilité des services en effectuant des vérifications de la connectivité.
- **Auditbeat :** Pour collecter des données d'audit du système d'exploitation.
- **Functionbeat :** Pour déclencher des événements basés sur des fonctions serverless.

