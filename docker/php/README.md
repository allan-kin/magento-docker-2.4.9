# After creating the image run: 

`docker compose exec php bash`

## If you want to set up a brand-new project, then inside the container:

```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.9 .
```

## For Linux: After the installation, outside the container (exit), do: 

```
docker compose exec --user root php sh -lc "cd /var/www/html && find var generated pub/static pub/media app/etc -type f -exec chmod g+w {} + 2>/dev/null || true && find var generated pub/static pub/media app/etc -type d -exec chmod g+ws {} + 2>/dev/null || true && chown -R www-data:www-data var generated pub/static pub/media app/etc"
```

## For Mac

```
sudo chown -R "$USER":staff var generated pub/static pub/media app/etc
chmod -R u+rwX,g+rwX var generated pub/static pub/media app/etc
find var generated pub/static pub/media app/etc -type d -exec chmod g+s {} \;
```

## Running this for the initial setup: 

Enter the docker `docker compose exec php bash`

```
bin/magento setup:install \
  --base-url=http://localhost:8080/ \
  --db-host=db \
  --db-name=magento \
  --db-user=magento \
  --db-password=magento \
  --admin-firstname=Admin \
  --admin-lastname=User \
  --admin-email=admin@magento.com \
  --admin-user=admin \
  --admin-password='Test1234!' \
  --language=en_US \
  --currency=USD \
  --timezone=America/Sao_Paulo \
  --use-rewrites=1 \
  --search-engine=opensearch \
  --opensearch-host=opensearch \
  --opensearch-port=9200 \
  --opensearch-index-prefix=magento2 \
  --opensearch-timeout=15 \
  --backend-frontname=admin
```

## Set up the developer mode:

```
bin/magento deploy:mode:set developer
bin/magento cache:clean
bin/magento indexer:reindex
```

## Before log in in the admin do: 

```
bin/magento config:set twofactorauth/general/force_providers google
bin/magento cache:clean
```
