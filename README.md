Magento Community Edition - Docker
---
### Up Docker
##### Windows - WSL - Before Docker up
Open your powershell,

```shell
# Loging into docker desktop sub linux
wsl -d docker-desktop

# Then increase max map count to fix issue with Opensearch
sysctl -w vm.max_map_count=262144
```

### Run composer
Log in to your docker container and run following command,

```shell
dcli web
cd app/
composer install
```

### Installation

Install magento using following command

```shell
bin/magento setup:install \
--base-url=http://magento2ce \
--db-host=db \
--db-name=magento \
--db-user=root \
--db-password=root \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_GB \
--currency=DKK \
--timezone=America/Chicago \
--use-rewrites=1 \
--search-engine=opensearch \
--opensearch-host=opensearch-node1 \
--opensearch-port=9200 \
--opensearch-index-prefix=magento2 \
--opensearch-timeout=15

```

### Disable 2FA into your dev env

```shell
php bin/magento module:disable {Magento_AdminAdobeImsTwoFactorAuth,Magento_TwoFactorAuth}
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy -f
php bin/magento indexer:reindex
php bin/magento cache:flush
```
