# PHP-FPM

## Running Stack
* Direct Connection to the Internet since NGINX & PHP-FPM will install cURL
* Install [Docker Compose](https://docs.docker.com/compose/install/)
* Need to addto your **/etc/hosts** the record 127.0.0.1 **php-fpm.example.org**

## NGINX

### Version
* NGINX 1.15.10

### Dockerfile
* Container installs curl (HealthCheck)

### Configuration

#### TLS
* Port 80 FWDing to port 443
* DH Enable (2048 bits)

```
openssl dhparam -out dhparam2048.pem 2048
```

* Create a Self Sign Cert since I do not have a DNS to put the wordpress.example.org

```
openssl genrsa -out rootCA.key 4096
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt
openssl genrsa -out wordpress.example.org.key 2048
openssl req -new -key php-fpm.example.org.key -out php-fpm.example.org.csr
openssl x509 -req -in php-fpm.example.org.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out php-fpm.example.org.pem -days 500 -sha256
```

* HSTS Enable
* OCSP Stapling Enable

## PHP-FPM 

### Version
* PHP-FPM 7.1

### Pools
* Choose 'ondemand' since it does not leave processes lingering
* Spawns processes as they are needed 
* Listen Directive: Choosen TCP since on an AWS config it would allowd Autoscaling
* TCP listen directive have a higher overhead than unix socket but not that much

### Usage
* Go to php-fpm.example.org and you will load index.php example code 
