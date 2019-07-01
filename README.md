1. Generate the certificates (only needed once):

````docker-compose -f create-certs.yml up --force-recreate````

1. Start two Elasticsearch nodes configured for SSL/TLS::

````docker-compose up -d````

1. Generate random passwords for all users

````
docker exec es01 /bin/bash -c "bin/elasticsearch-setup-passwords \
auto --batch \
-Expack.security.http.ssl.certificate=certificates/es01/es01.crt \
-Expack.security.http.ssl.certificate_authorities=certificates/ca/ca.crt \
-Expack.security.http.ssl.key=certificates/es01/es01.key \
--url https://localhost:9200"
````

1. Update password in `.env`
````
ELASTIC_PASSWORD=GUgIOYAk8McaULLZr87x
KIBANA_PASSWORD=baIxb637b55YHdWG73kr
````
