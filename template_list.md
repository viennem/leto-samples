# Liste des templates ACID

Voici des exemples de templates qui pourraient servir pour l'équipe **ACID**.

Les templates sont rangés selon **trois catégories** :

1. **Templates de projet :** qui peuvent servir de base pour créer un nouveau projet.
2. **Templates de modèle :** qui peuvent servir de base pour créer un nouveau modèle (pipeline ou infra).
3. **Templates de composants :** qui peuvent être ajoutés dans un modèle existant (pipeline ou infra).

## 1. Templates de projet

### Projet Terraform+Ansible+Jenkins

1. Jenkins+Terraform+Ansible
2. Jenkins+Kubernetes+Docker
3. GitHubActions+Terraform+Ansible
4. GitHubActions+Kubernetes+Docker

5. Jenkins+Ansible
6. Jenkins+Terraform
7. GitHubActions+Ansible
8. GitHubActions+Terraform

9. Jenkins
10. GitHubActions

Les templates de projet ne permettent de créer qu'un seul microservice (pour éviter d'avoir un grand nombre de templates avec toutes les combinaisons possibles).
Si on souhaite avoir plusieurs microservices, il faut les ajouter après la création du projet en ajoutant des modèles dans la vue d'index du projet.
Il faudra voir si on pourrait améliorer cela plus tard, par exemple :

* Pouvoir sélectionner plusieurs templates de projet et les combiner
    * Cette approche a ses limites, car dans le cas d'un projet Terraform on peut vouloir un pipeline de CI par microservice, et un seul pipeline de CD et une seule infra Terraform globale.
* Avoir un système de templates dynamiques, avec par exemple un système de variables et de templating qui permettraient d'indiquer le nombre de microservices désiré.

De plus, il n'est pas possible de sélectionner le langage de notre application pour le build dans le pipeline de CI dans cette liste de templates de projets, car on aurait encore un fois un trop grand nombre de combinaisons possibles. Cela signifie que le pipeline de CI ne pourra pas être pré-configuré avec les commandes pour builder l'application dans le langage spécifique.

### Projet Kubernetes+Docker+Jenkins

1. Projet Kubernetes+Docker+Jenkins - **Java**
2. Projet Kubernetes+Docker+Jenkins - **JavaScript**
    - Exemple: https://github.com/viennem/demo-k8s
3. Projet Kubernetes+Docker+Jenkins - **Python**
4. Projet Kubernetes+Docker+Jenkins - **.NET**

## 2. Templates de modèle

### Pipelines

#### CI (Jenkins)

1. **"Java CI"** : Pipeline de CI pour builder une application Java.
2. **"JavaScript CI - NPM"** : Pipeline de CI pour builder une application JavaScript avec NPM.
3. **"JavaScript CI - Yarn"** : Pipeline de CI pour builder une application JavaScript Yarn.
4. **"Python CI"** : Pipeline de CI pour builder une application Python.
5. **".NET CI"** : Pipeline de CI pour builder une application .NET.

SonarQube serait utilisé par défaut dans chacun de ces templates de CI.
Si on ne veux pas l'utiliser, il suffirait de supprimer le composant Sonar dans la vue modèle, après avoir instancié le template.

#### CD (Jenkins)

1. **"Terraform CD"** : Pipeline de CD pour déployer sur Terraform.
2. **"Kubernetes CD"** : Pipeline de CD pour déployer sur Kubernetes.
3. **"Kubernetes CD + Vault integration"** : Pipeline de CD pour déployer sur Kubernetes en injectant des secrets Vault.
4. **Kuberneted CD + Helm** : Pipeline de CD pour déployer sur Kubernetes avec Helm.
5. **Kuberneted CD + Helm + Vault integration** : Pipeline de CD pour déployer sur Kubernetes avec Helm, en injectant des secrets Vault.

### Infrastructure

#### Terraform

- Single AZ
- Multi AZ (actif actif)
- Multi AZ (actif passif)
- Multi-region
- BDD Postgres
- BDD Oracle
- Message queue

#### Kubernetes

## 3. Templates de composants

### Pipelines

#### CI (Jenkins)

Composants de CI :

![](https://github.com/viennem/demo-k8s/raw/main/img/ci-bricks.png)

Aucun template de composants de CI nécessaire.

<details><summary><b>[Résolu] Incertitude</b></summary>

As-t-on besoin de templates de CI ? => cela va dépendre du fonctionnement des composants dans le plugin Jenkinator

- Si les composants comme "Build / Test" sont spécifiques (avec un composant différent par language), alors il n'y aura pas besoin de templates de CI.
- Si les composants sont génériques (exemple : un seul composant "Build / Test" générique), alors on aura besoin de templates pour décliner les composants génériques en templates spécifiques par langauge, exemple :
  1. **"Build / Test - Java"** : Composant "Build / Test" pré-configuré avec les commandes pour builder une application Java.
  2. **"Build / Test - JavaScript"** : Composant "Build / Test" pré-configuré avec les commandes pour builder une application JavaScript.
  3. **"Build / Test - Python"** : Composant "Build / Test" pré-configuré avec les commandes pour builder une application Python.
  4. **"Build / Test - .NET"** : Composant "Build / Test" pré-configuré avec les commandes pour builder une application .NET.
  5. Idem pour **"Sonar Analysis"** décliné en languages (Java et JavaScript seulemment) ?
  6. Idem pour **"Automatic Version Retrieval"** décliné en languages  (Java et JavaScript seulemment)  ?

**Réponse :** Les composants seront spécifiques, donc il n'y aura pas besoin de templates,
car cela permettra de simplifier la configuration des attributs des composants au lieu d'avoir des noms d'attributs génériques.

</details>

<details><summary><b>[Résolu] Autres questions en dehors des templates</b></summary>

- Attribut language au niveau du composant pipeline, ou au niveau de chaque composant (Build/Test, Version Retrival, Sonar Analysis) ?
    - Qid des pipelines multi-languages ?

**Réponse :** Pour permettre d'avoir un pipeline flexible (multi-language), le paramètre indiquant le nom du langage de programmation sera dupliqué dans les composants "Version retrieval" et "Sonar Analysis".

</details>

#### CD (Jenkins)

Composants de CD :

![](https://github.com/viennem/demo-k8s/raw/main/img/cd-bricks.png)

Aucun template de composants de CD nécessaire.

### Infrastructure

#### Terraform

1. **"OCS Compute"** : OCS Compute instance et ses dépendances.
   <details><summary>Afficher</summary><img src="./img/compute.png" /></details>
2. **"OCS Compute + Block Storage"** : OCS Compute instance et ses dépendances + block storage attaché.
   <details><summary>Afficher</summary><img src="./img/compute.png" /><br /><b>TODO:</b> composants à ajouter dans les metadata de Terraform</details>
3. **"OCS Compute + File Storage"** : OCS Compute instance et ses dépendances + file storage attaché.
   <details><summary>Afficher</summary><img src="./img/compute.png" /><br /><b>TODO:</b> composants à ajouter dans les metadata de Terraform</details>
4. **"OCS Compute + Block & File Storage"** : Compute instance et ses dépendances + block et file storage attachés.
   <details><summary>Afficher</summary><img src="./img/compute.png" /><br /><b>TODO:</b> composants à ajouter dans les metadata de Terraform</details>
5. ~~"Postgres Cluster" : Cluster postgres et une database.~~
   <details><summary>Afficher</summary><img src="./img/postgres_cluster.svg" /></details>
6. ~~"DNS Alias" : Alias DNS avec zone DNS.~~
   <details><summary>Afficher</summary><img src="./img/dns.png" /></details>
7. **"Security Group"** : Security group avec règles HTTPS+SSH+~~ICMP~~.
   <details><summary>Afficher</summary><img src="./img/secgroup.svg" /></details>
   <b>TODO :</b> créer d'autres templates de security groups avec des règles différentes (exmple : <code>SMTP</code>).
8. **"SLB Load-Balancer"** : Load-balancer et sous-composants.
   <details><summary>Afficher</summary><img src="./img/slb.png" /></details>
9. **"Traffic Manager"** : Traffic manager et deux load-balancers (multi-az ou multi-régions).
   <details><summary>Afficher</summary><img src="./img/traffic_manager.png" /></details>
10. ~~"File Storage" : Consistency Group + Filesystem~~
11. **"Object Storage"** : Access Key + Bucket + Policy + Group.
12. **"RabbitMQ"** : RabbitMQ broker + user + vhost.
13. **"Certificate"** : Certificat pré-configuré avec les champs subject de la SG.
14. **"VCS Compute"** : VCS Compute instance et ses dépendances.
15. **"VCS Compute + Block Storage"** : VCS Compute instance et ses dépendances + block storage.
16. **"VCS Compute + File Storage"** : VCS Compute instance et ses dépendances + file storage.
17. **"VCS Compute + Block & File Storage"** : VCS Compute instance et ses dépendances + block et file storage.

<details><summary>Composants manquants dans le plugin</summary>

- Storage :
    - Block Storage :
        - `compute_volume`, `compute_volume_attachement`
    - File Storage :
        - `files_consistency_group`, `files_filesystem`, `files_nfs_client`
    - Object Storage :
        - `object_storage_access_key`, `object_storage_bucket`, `object_storage_group`, `object_storage_rights_policy`, `object_storage_replication_policy`, `object_storage_bucket_replication`
- PaaS :
    - Rabbitmq :
        - `rabbitmq_broker`, `rabbitmq_user`, `rabbitmq_vhost`
    - Certificates :
        - `pki_certificate_subject`
    - Oracle :
        - `oracle_database`
- Autres :
    - `vcs_server`
    - `compute_server_group`
    - `os_configuration_module`
    - `slb_http_policy`, `slb_certificate`
    - `traffic_manager_healthcheck`
    - Read vault secret
- Pas nécessaire ?
    - Kubernetes workspace
    - Airflow instance
    - Secrets (create secret)
    - MyVault namespace
    - Monitoring
    - Metrology
    - Showback
    - IAM client (create client_id, client_secret)

</details>

Questions :

- "OCS/VCS Compute" : 4 variations -> faut-il garder seulement la variation la plus complète, dans la logique où il est plus facile de supprimer le trop que de rajouter ? (comme pour Kubernetes)
    - Idem pour load-balancer / traffic manager
    - Ajouter un security group dans les 4 variations ?
- Supprimer les templates barrés (Postgres cluster, DNS Alias, File Storage) ?

#### Kubernetes

1. **"Deployment++"** : `Deployment` + `Service` + `Ingress` + `PersistentVolumeClaim` + `ConfigMap` + `Secret` + `HorizontalPodAutoscaler`.
   <details><summary>Afficher</summary><img src="./img/deployment.png" /></details>
2. **"StatefullSet++"** : `StatefullSet` + `Service` + `Ingress` + `PersistentVolumeClaim` + `ConfigMap` + `Secret` + `HorizontalPodAutoscaler`.
   <details><summary>Afficher</summary><img src="./img/statefullset.png" /></details>
3. **"CronJob++"** : `CronJob` + `PersistentVolumeClaim` + `ConfigMap` + `Secret`.
   <details><summary>Afficher</summary><img src="./img/cronjob.png" /></details>
4. **"Deployment++ - DR"** : `Deployment` + `Service` + `Ingress` + `PersistentVolumeClaim` + `ConfigMap` + `Secret` + `HorizontalPodAutoscaler` - configuré avec affinity pour garantir le scheduling des pods sur différents noeuds.
5. **"StatefullSet++ - DR"** : `StatefullSet` + `Service` + `Ingress` + `PersistentVolumeClaim` + `ConfigMap` + `Secret` + `HorizontalPodAutoscaler` - configuré avec affinity pour garantir le scheduling des pods sur différents noeuds.

**Question :** bonne idée de mettre un `HorizontalPodAutoscaler` par défaut ?

**TODO :** Ajouter un composant `Volumes` séparé pour permettre d'ajouter/supprimer facilement une `ConfigMap`, un `Secret`, ou un `PersistentVolumeClaim` à un `Pod`.

- **difficulté d'implémentation :** les volumes sont configurés à plusieurs endroits dans un `Pod` : [volumes](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#volumes) et [containers.volumeMounts](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#volumes-1).
