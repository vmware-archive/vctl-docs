# Deprecated

As of Fusion 11.5.5 and TP20H2, this document is no longer maintained. We expect all containers to work, and where something does not wokr as expected we would encourage users to [file an issue](https://github.com/VMwareFusion/nautilus/issues/new).

# Tested Images

What follows here is a maintained list of containers that we have tested and any caveats that need consideration when running that image.


| **Images**  | **'vctl' Sample Commands** | **Notes** |
| ------------- | ------------- | ------------- |
| adoptopenjdk | vctl run container -t --image docker.io/library/adoptopenjdk:latest myopenjdk |  |
| aerospike | vctl run container myaerospike -p 3000:3000 -p 3001:3001 -p 3002:3002 -p 3003:3003 --image docker.io/library/aerospike:latest -t -v $PWD/aerospike:/opt/aerospike/etc -- /entrypoint.sh asd --foreground --config-file /opt/aerospike/etc/aerospike.conf | Put aerospike.conf under $PWD/aerospike folder |
| alpine | vctl run container -t --image docker.io/library/alpine:latest myalpine |  |
| alt | vctl run container -t --image docker.io/library/alt:latest myalt |  |
| amazoncorretto | vctl run container -t --image docker.io/library/amazoncorretto:latest myamazoncorretto |  |
| amazonlinux | vctl run container mycentos --image docker.io/library/amazonlinux:latest -t |  |
| bash | vctl run container -t --image docker.io/library/bash:latest mybash |  |
| buildpack-deps | vctl run container mybuildpack-deps --image docker.io/library/buildpack-deps:latest -t |  |
| centos | vctl run container mycentos --image docker.io/library/centos:latest -t |  |
| chronograf | vctl run container -d -p 8888:8888 --image docker.io/library/chronograf:latest mychronograf |  |
| clojure | vctl run container -t  --image docker.io/library/clojure:latest myclojure |  |
| composer | vctl run container -t -v $PWD:/app --image=docker.io/library/composer:latest |  |
| consul | vctl run container -t --image docker.io/library/consul:latest myconsul |  |
| convertigo | vctl run container -d -p 28080:28080 --image docker.io/library/convertigo:latest myconvertigo |  |
| couchbase | vctl run container -t --image  docker.io/library/couchbase:latest mycouchbase |  |
| couchdb | vctl run container -t --image  docker.io/library/couchdb:latest mycouchdb |  |
| crate | vctl run container --image docker.io/library/crate:latest -p 4200:4200 -v $PWD:/data mycrate |  |
| crux | vctl run container  -t --image docker.io/library/crux:latest mycrux |  |
| debian | vctl run container -t  --image docker.io/library/debian:latest mydebian |  |
| drupal | vctl run container -t -p 20013:80 --image=docker.io/library/drupal:latest mydrupal |  |
| eclipse-mosquitto | vctl run container -t -p 1883:1883 -p 9001:9001 --image docker.io/library/eclipse-mosquitto:latest myeclipse-mosquitto |  |
| elasticsearch | vctl run container myelastic -p 9200:9200 -p 9300:9300 --env "discovery.type=single-node" --image docker.elastic.co/elasticsearch/elasticsearch:7.5.1 | Set VM memory to be 2048M for container |
| elixir | vctl run container -t  --image docker.io/library/elixir:latest myelixir |  |
| erlang | vctl run container -t --image docker.io/library/erlang:latest myerlang |  |
| euleros | vctl run container -t --image docker.io/library/euleros:latest myeuleros |  |
| express-gateway | vctl run container -i docker.io/library/express-gateway:latest -p 8080:8080 -p 9876:9876 -v $PWD:/var/lib/eg myexpress |  |
| flink | vctl run container flink_jobmanager --image docker.io/library/flink:latest -p 8081:8081 -p 6123:6123 --env "JOB_MANAGER_RPC_ADDRESS=[Host ip address]" -t -- /docker-entrypoint.sh jobmanager<br>vctl run container flink_taskmanager --image docker.io/library/flink:latest -p 6121:6121 -p 6122:6122 --env "JOB_MANAGER_RPC_ADDRESS=[Host ip address]" -t -- /docker-entrypoint.sh taskmanager |  |
| fluentd | vctl run container -i docker.io/library/fluentd:latest -p 24224:24224/udp -p 24224:24224 myfluent |  |
| gcc | vctl run container mygcc -i docker.io/library/gcc:latest -t bash |  |
| ghost | vctl run container -t --image docker.io/library/ghost:latest myghost |  |
| gradle | vctl run container -i docker.io/library/gradle:latest -v $PWD:/home/gradle/project --cwd /home/gradle/project  mygradle -- gradle -q hello | build.gradle with hello task is created under $PWD  |
| groovy | vctl run container mygroovy --image docker.io/library/groovy:latest -v $PWD:/home/groovy -- groovy hello_word.groovy | Put "hello_word.groovy" under $PWD directory |
| haproxy | vctl run container -i docker.io/library/haproxy:latest myhaproxy -t bash |  |
| haskell | vctl run container -i docker.io/library/haskell:latest myhaskell |  |
| hello-world  | vctl pull image docker.io/library/hello-world:latest<br>vctl run container -i docker.io/library/hello-world:latest myhello|  |
| httpd | vctl run container -i docker.io/library/httpd:latest -v $PWD:/usr/local/apache2/htdocs/ -p 8080:80 myhttpd |  |
| hylang | vctl run container -t --image=docker.io/library/hylang:latest myhylang |  |
| ibmjava | vctl run container -t --image=docker.io/library/ibmjava:latest myibm |  |
| influxdb | vctl run container -p 8086:8086 -v $PWD:/var/lib/influxdb -t --image=docker.io/library/influxdb:latest myinfluxdb |  |
| irssi | vctl run container -t -e TERM -v $PWD/.irssi:/home/user/.irssi --image=docker.io/library/irssi:latest myirssi |  |
| jetty | vctl run container -d -p 20011:8080 -p 20012:8443 --image=docker.io/library/jetty:latest myjetty |  |
| jobber | vctl run container --image docker.io/library/jobber:latest -v $PWD:/root/.jobber myjobber | Put .jobber under $PWD directory |
| joomla | vctl run container mysql-1 --image docker.io/mysql/mysql-server:5.7 -p 3306:3306 --env="MYSQL_USER=MYDBUSER"  --env="MYSQL_PASSWORD=MYPASSWD"  --env="MYSQL_ROOT_PASSWORD=MYPASSWD"  --env="MYSQL_DATABASE=MYDB" -d<br>vctl run container myjoomla --image docker.io/library/joomla:latest --env="JOOMLA_DB_HOST=MYSQLHOST:PORT" --env="JOOMLA_DB_USER=MYDBUSER" --env="JOOMLA_DB_PASSWORD=MYPASSWD" --env="JOOMLA_DB_NAME=MYDB" -p 8080:80 -v $PWD:/var/www/html -t|  |
| jruby | vctl run container -i docker.io/library/jruby:latest -t myruby -- jruby --help |  |
| julia | vctl run container -i docker.io/library/julia:latest -t -v $PWD:/usr/myapp julia julia test.jl |  |
| lightstreamer | vctl run container -d -p 20010:8080 --image=docker.io/library/lightstreamer:latest mylight |  |
| mageia | vctl run container -i docker.io/library/mageia:latest -t mymameia |  |
| mariadb | vctl run container mymariadb --image docker.io/library/mariadb:latest -p 3306:3306 --env "MYSQL_ROOT_PASSWORD=MYPASSWD" -t " |  |
| maven | vctl run container -i docker.io/library/maven:latest -t mymaven -- bash |  |
| mediawiki | vctl run container -d -p 20009:80 --image=docker.io/library/mediawiki:latest mymediawiki |  |
| memcached | vctl run container -d --image=docker.io/library/memcached:latest mymemcached |  |
| mongo-express | vctl run container --image docker.io/library/mongo-express:latest -e ME_CONFIG_MONGODB_SERVER=[mongo container IP] my-mongo-express |  |
| mysql | vctl run container --image docker.io/library/mysql:latest mysql-1 -e MYSQL_ROOT_PASSWORD=MYPASSWD |  |
| nats | vctl run container -i docker.io/library/nats:latest -d -p 8222:8222 mynats |  |
| nginx | vctl pull image docker.io/library/nginx:latest<br>vctl run container -d -p 8080:80 --image docker.io/library/nginx:latest mynginx |  |
| nuxeo | vctl run container -d -p 8080:8080 --image docker.io/library/nuxeo:latest mynuxeo |  |
| openjdk | vctl run container -i docker.io/library/openjdk:latest -t myopenjdk |  |
| orientdb | vctl run container -i docker.io/library/orientdb:latest -p 2424:2424 -p 2480:2480 -e ORIENTDB_ROOT_PASSWORD=rootpwd myorientdb |  |
| percona | vctl run container --image docker.io/library/percona:latest mypercona --env MYSQL_ROOT_PASSWORD=secret |  |
| photon | vctl run container -t --image docker.io/library/photon:latest myphoton |  |
| plone | vctl run container -i docker.io/library/plone:latest -p 8080:8080 myplone |  |
| pypy | vctl run container -i docker.io/library/pypy:latest -t mypypy |  |
| rabbitmq | vctl run container --hostname my-rabbit -i docker.io/library/rabbitmq:latest myrabbit |  |
| rakudo-star | vctl run container --image docker.io/library/rakudo-star:latest myrakudo-star -v $PWD:/script perl /script/simple.pl |  |
| redis | vctl run container myredis --image docker.io/library/redis:latest -t |  |
| ruby | vctl run container -i docker.io/library/ruby:latest -t myruby |  |
| solr | vctl run container -i docker.io/library/solr:latest -p 8983:8983 -t mysolr |  |
| teamspeak | vctl run container myteamspeak -p 9987:9987/udp -p 10011:10011 -p 30033:30033 --env TS3SERVER_LICENSE=accept --image docker.io/library/teamspeak:latest |  |
| tomcat | vctl pull image docker.io/library/tomcat:latest<br>vctl run container mytomcat -p 8888:8080 --image docker.io/library/tomcat:latest |  |
| tomee | vctl run container  --image docker.io/library/tomee:latest mytomee |  |
| ubuntu | vctl run container  --image docker.io/library/ubuntu:latest myubuntu -t |  |
| vault | vctl run container -i docker.io/library/vault:latest -p 9989:8200 myvault |  |
