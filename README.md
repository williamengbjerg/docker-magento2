# 🟧 Magento 2 

Onboarding setup and project setup.

--- 
### Install clean version of Magento2 
```bash
composer create-project --repository=https://repo.magento.com/ magento/project-community-edition ./
```

### Run in PHP container to install magento 2 setup 
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
--elasticsearch-host=elasticsearch \
--elasticsearch-port=9200
```

Admin url is being generated once installation is done.

### Remove two factor 
```bash
php bin/magento mo:di Magento_TwoFactorAuth
```
```bash
php bin/magento setup:di:compile
```

### Enable developer mode
```bash
php bin/magento deploy:mode:set developer
```

### Set developer mode (To get error info)
```bash
php bin/magento setup:config:set developer
```

### Fix file permissions 
```bash
find var vendor pub/static pub/media app/etc -type f -exec chmod g+w {} + && find var vendor pub/static pub/media app/etc -type d -exec chmod g+w {} + && chmod u+x bin/magento
```

1. Set permissions to the files:
```bash
find . -type f -exec chmod 644 {} \;
```
2. Set permissions to the directories
```bash
find . -type d -exec chmod 755 {} \;
```
3. Set permissions to special directories
```bash
find var -type d -exec chmod 755 {} \;
find pub/media -type d -exec chmod 777 {} \;
find pub/static -type d -exec chmod 777 {} \;
```

<strong>Info:</strong>
<em>In some cases, you can not use 770 or 660 permissions (Fast-CGI systems, for example). Instead, you can use 755 and 644 respectively.</em>

---

## Error log 

enable ```display_errors``` from file ```app/bootstrap.php``` around line 11 remove ```#``` 


[Link](https://magento.stackexchange.com/a/94569/91296)
---

## 🐳 Docker

### Docker-sync
Before running docker-compose run docker-sync start via term.

COMMAND | START SYNC | CLEAN SYNC | STOP SYNC | LIST SYNCS |
--- | --- | --- | --- | --- |
```docker-sync``` | ```start``` | ```clean``` | ```stop``` | ```list```

[Full guide](https://docker-sync.readthedocs.io/en/latest/troubleshooting/sync-stopping.html)

---

### Docker containers 
COMMAND | DOCKER START | DOCKER DOWN | DIG INTO CONTAINER |
--- | --- | --- | --- | 
```docker-compose``` | ```up -d``` | ```down``` | ```docker exec -it [CONTAINER-ID] bash```

### Docker containers
Enter any docker containers 
```bash
docker exec -it [CONTAINER-ID] bash
```

### Docker containers
Remove all stopped containers, networks not used by at least one container, dangling images, dangling build cache 
```bash
docker-compose up -d --build --force-recreate
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
