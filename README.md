# 🟧 Magento 2 

Fresh magento2 project setup. Head into `application` folder in your host/root through term.  

### 1. Install fresh Magento2 version 
```bash
composer create-project --repository=https://repo.magento.com/ magento/project-community-edition ./
```

### 2. Run command below 

Run on root/host inside application folder: 

```bash
php bin/magento setup:install \
--base-url=http://magento2.test \
--db-host=127.0.0.1 \
--db-name=database \
--db-user=user \
--db-password=password \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@example.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=Europe/Copenhagen \
--use-rewrites=1 \
--elasticsearch-host=localhost:9200 \
--elasticsearch-port=9200
```
--- 

### Or run in docker container
```bash
php bin/magento setup:install \
--base-url=http://magento2.test \
--db-host=db:3306 \
--db-name=database \
--db-user=user \
--db-password=password \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@example.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=Europe/Copenhagen \
--use-rewrites=1 \
--elasticsearch-host=elastic-search \
--elasticsearch-port=9200
```

---


Admin url is being generated once installation is done.

### 3. Disable two factor and compile files
```bash
php bin/magento mo:di Magento_TwoFactorAuth
```
```bash
php bin/magento setup:di:compile
```
### 4. Enable developer mode (For debug)
```bash
php bin/magento deploy:mode:set developer
```
```bash
php bin/magento setup:config:set developer
```

### Fix file permissions 
Set the proper permission for the whole Magento 2 installation directory by using below command 

```bash
find . -type d -exec chmod 700 {} \; && find . -type f -exec chmod 600 {} \;
```

<strong>Info:</strong>
<em>In some cases, you can not use 770 or 660 permissions (Fast-CGI systems, for example). Instead, you can use 755 and 644 respectively.</em>

---

### Permissions in docker container 
- `chmod 777 -R var`
- `chmod 777 -R generated`
- `chmod 777 -R app/etc`
- `rm -rf var/cache/* var/page_cache/* var/generation/*`

After that run `php bin/magento setup:di:compile`

[Link guide](https://magento.stackexchange.com/a/251709/91296)

---

## Enable error log 

enable ```display_errors``` from file ```app/bootstrap.php``` around line 11 remove ```#``` 

[Link - Stackexchange](https://magento.stackexchange.com/a/94569/91296)

---

## 🐳 Docker

To start containers use `docker-sync-stack start` — this will start docker-sync process as well as the server

### Docker-sync

COMMAND | START SYNC | CLEAN SYNC | STOP SYNC | LIST SYNCS |
--- | --- | --- | --- | --- |
```docker-sync``` | ```start``` | ```clean``` | ```stop``` | ```list```

[Full guide](https://docker-sync.readthedocs.io/en/latest/troubleshooting/sync-stopping.html)

---

### Docker containers 
COMMAND | DOCKER START | DOCKER DOWN | DIG INTO CONTAINER |
--- | --- | --- | --- | 
```docker-compose``` | ```up -d``` | ```down``` | ```docker exec -it [CONTAINER-ID] bash```

### Enter a docker container
```bash
docker exec -it [CONTAINER-ID] bash
```

### Re-build docker containers
Remove all containers, networks not used by at least one container, dangling images, dangling build cache 
```bash
docker-compose up -d --build --force-recreate
```

### Delete all volumes
```bash
docker volume rm $(docker volume ls -q)
```
### Delete all images
```bash
docker system prune -a
```
```bash
docker system prune --volumes
```

---

## 🤖 Magento commands
Run below command unless alias is different.
```bash
php bin/magento
```

### Admin
| Command                                  | Info
--- | --- |
| ```admin:user:create ```                 | <em>Creates an administrator</em>

### App
| Command                                  | Info 
--- | --- |
| ```app:config:import```                  | Import data from shared configuration files to appropriate data storage

### i18n
| Command                                  | Info | 
--- | --- |
| ```i18n:collect-phrases```               | Discovers phrases in the codebase
| ```i18n:pack```                          | Saves language package

### Info
| Command                                        | Info | 
--- | --- |
| ```info:adminuri```                            | <em>Displays the Magento Admin URI</em>
| ```info:backups:list```                        | <em>Prints list of available backup files</em>
| ```info:currency:list```                       | <em>Displays the list of available currencies</em>
| ```info:dependencies:show-framework```         | <em>Shows number of dependencies on Magento framework</em>
| ```info:dependencies:show-modules```           | <em>Shows number of dependencies between modules</em>
| ```info:dependencies:show-modules-circular```  | <em>Shows number of circular dependencies between modules</em>
| ```info:language:list```                       | <em>Displays the list of available language locales</em>
| ```info:timezone:list```                       | <em>Displays the list of available timezones</em>


### Maintenance
| Command                                  | Info |
--- | --- |
| ```maintenance:allow-ips```              | <em>Sets maintenance mode exempt IPs</em>
| ```maintenance:disable```                | <em>Disables maintenance mode</em>
| ```maintenance:enable```                 | <em>Enables maintenance mode</em>
| ```maintenance:status ```                | <em>Displays maintenance mode status</em>


### Module
| Command                                  | Info |
--- | --- |
| ```module:config:status```               | <em>Checks the modules configuration in the 'app/etc/config.php' file and reports if they are up to date or not</em>
| ```module:disable```                     | <em>Disables specified modules</em>
| ```module:enable```                      | <em>Enables specified modules</em>
| ```module:status```                      | <em>Displays status of modules</em>
| ```module:uninstall```                   | <em>Uninstalls modules installed by composer</em>

### Sampledata
| Command                                  | Info |
--- | --- |
| ```sampledata:deploy```                  | <em>Deploy sample data modules for composer-based Magento installations</em>
| ```sampledata:remove```                  | <em>Remove all sample data packages from composer.json</em>

### Setup
| Command                                  | Info
--- | --- |
| ```setup:backup```                       | <em>Takes backup of Magento Application code base, media and database</em>
| ```setup:config:set```                   | <em>Creates or modifies the deployment configuration</em>
| ```setup:db-data:upgrade```              | <em>Installs and upgrades data in the DB</em>
| ```setup:db-schema:upgrade```            | <em>Installs and upgrades the DB schema</em>
| ```setup:db:status```                    | <em>Checks if DB schema or data requires upgrade</em>
| ```setup:di:compile```                   | <em>Generates DI configuration and all missing classes that can be auto-generated</em>
| ```setup:install```                      | <em>Installs the Magento application</em>
| ```setup:performance:generate-fixtures```| <em>Generates fixtures</em>
| ```setup:rollback```                     | <em>Rolls back Magento Application codebase, media and database</em>
| ```setup:static-content:deploy```        | <em>Deploys static view files</em>
| ```setup:store-config:set```             | <em>Installs the store configuration. Deprecated since 2.2.0. Use config:set instead</em>
| ```setup:uninstall```                    | <em>Uninstalls the Magento application</em>
| ```setup:upgrade```                      | <em>Upgrades the Magento application, DB data, and schema</em>
