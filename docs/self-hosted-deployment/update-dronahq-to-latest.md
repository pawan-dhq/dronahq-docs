---
sidebar_position: 96
---

# Update DronaHQ version

while updating DronaHQ, users might need downtime. Its a good practice to always notify users about downtimes and newly installed updates. Also create backup of your instance and databbases regularly before update. DronaHQ provide incremental updates for database. it should be performed in sequence. If you wish to downgrade your installation, you do not need to downgrade database.

### 1. Notify users about downtime

Its always helpful to send announcements before performing any activity slightly before you start downtime.

### 2. Create a backup

Create backup of your server instance before upgrading so that you can restore them if needed.

If you are using any cloud service like AWS, GCP, Azure, the cloud provider might have a convinient way to backup and restore state of your instance.

- Backup your MySQL and Mongo database. If you have setup your databases with a managed service like AWS, they provide a managed way to take periodic backup of your databases. You can also take snapshots of your database to restore is faster in case of any failure.

- Also, take backup of your environment variables specific to your installation and store in safe place.

### 3. Choose DronaHQ version

Check [Releases](https://community.dronahq.com/t/dronahq-self-hosted-releases/1177) page to see available DronaHQ updates and its changelogs. always read changelogs between your current version and the version you are upgrading to. It may also include notification and instructions for managing deprecated features.

It is highly recommended for you to frequently check updates and always be on latest version.

### 4. Download database updates for target version.

Following is a interactive shell script, which will help you download the database updates for the upgrade version nyou choose.

```shell
/bin/bash -c "$(curl -fsSL https://license.dronahq.com/self-hosted/master/scripts/get-database-updates.sh)"
```

Above line will download an update file with name `update.sql` in your working directory.

### 5. Apply updates on your database

##### a. Apply updates on containarized database

Run following command to apply updates on  containerized database.

```shell
sudo docker exec dronahq-self-hosted-mysqldb /bin/sh -c "mysql -u root -p<% root password %> < update.sql"
```
##### b. Apply updates on external database

Run following command to apply updates on  exteranal database.

```shell
mysql --host=<% host %> --port=<% port %> --user=<% username %> --password=<% password %> < update.sql
```

### 6. Update DronaHQ version in service file.

##### a. For Docker installation

In `docker-compose.yaml`, change the image tag to indicate the version of DronaHQ to install. The following example specifies the image tag to install version `2.2.8`.

```
image: dronahq/self-hosted:2.2.8
services:
...
  webapp:
    image: dronahq/self-hosted:2.2.8
...
```
##### b. For Kubernetes cluster installation

In `dronahq-webapp.yaml`, change the image tag to indicate the version of DronaHQ to install. The following example specifies the image tag to install version `2.2.8`.

```
...
spec:
  template:
    spec:
      containers:
        - image: dronahq/self-hosted:2.2.8
...
```

### 7. Restart DronaHQ service

Restart is mandatory for new updates to take effect.

##### a. Restart Docker installation

Restart DronaHQ docker container with following command
```
sudo docker-compose up -d webapp
```

##### b. Restart Kubernetes installation

Apply mofified manifest file with followinf command
```
sudo kubectl apply -f dronahq-webapp.yaml
```