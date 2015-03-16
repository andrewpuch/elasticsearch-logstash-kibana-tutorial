Amazon Linux AMI 2014.09.2

Elasticsearch 1.4.4
===================

Commands
--------
sudo su
yum update -y
cd /root
wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.4.4.noarch.rpm
yum install elasticsearch-1.4.4.noarch.rpm -y
rm -f elasticsearch-1.4.4.noarch.rpm
cd /usr/share/elasticsearch/
./bin/plugin -install mobz/elasticsearch-head
./bin/plugin -install lukas-vlcek/bigdesk
./bin/plugin install elasticsearch/elasticsearch-cloud-aws/2.4.1
cd /etc/elasticsearch
nano elasticsearch.yml

Config
------
cluster.name: awstutorialseries
cloud.aws.access_key: ACCESS_KEY_HERE
cloud.aws.secret_key: SECRET_KEY_HERE
cloud.aws.region: us-east-1
discovery.type: ec2
discovery.ec2.tag.Name: "AWS Tutorial Series - Elasticsearch"
http.cors.enabled: true
http.cors.allow-origin: "*"

Commands
--------
service elasticsearch start 


Logstash 1.4.2
==============

Commands
--------
sudo su
yum update -y
cd /root
wget https://download.elasticsearch.org/logstash/logstash/packages/centos/logstash-1.4.2-1_2c0f5a1.noarch.rpm
yum install logstash-1.4.2-1_2c0f5a1.noarch.rpm -y
rm -f logstash-1.4.2-1_2c0f5a1.noarch.rpm
nano /etc/logstash/conf.d/logstash.conf

Config
------
input { file { path => "/tmp/logstash.txt" } } output { elasticsearch { host => "ELASTICSEARCH_URL_HERE" protocol => "http" } }

Commands
--------
service logstash start


Kibana 4.0.1
============

Commands
--------
sudo su
yum update -y
cd /root
wget https://download.elasticsearch.org/kibana/kibana/kibana-4.0.1-linux-x64.tar.gz
tar xzf kibana-4.0.1-linux-x64.tar.gz
rm -f kibana-4.0.1-linux-x64.tar.gz
cd kibana-4.0.1-linux-x64
nano config/kibana.yml 

Config
------
elasticsearch_url: "ELASTICSEARCH_URL_HERE"

Commands
--------
nohup ./bin/kibana &

Navigate In Browser
-------------------
http://KIBANA_URL:5601/
