## How to install elasticsearch on amazon linux 2

**Step 1**: Install Java

```Shell
sudo amazon-linux-extras install java-openjdk11
```
**Make sure JAVA_HOME environment variable is configured**

```Shell
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```
**Step 2**: Install Elasticsearch on Amazon linux 2

Accept the Elasticsearch GPG Key:

```Shell

sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

```

Create a file called elasticsearch.repo in the `/etc/yum.repos.d/` directory, :

```Shell
sudo vi /etc/yum.repos.d/elasticsearch.repo
```
Add ELK repository on Amazon Linux 2

```yaml

[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md

```
Install Elasticsearch:

```Shell
sudo yum install --enablerepo=elasticsearch elasticsearch
```
You can start or stop using this commands:
```Shell
sudo systemctl start elasticsearch
OR
sudo systemctl stop elasticsearch
``` 
Run the command: 
```Shell
sudo /bin/systemctl daemon-reload
```
Ruin the command:
```Shell
sudo /bin/systemctl enable elasticsearch.service
```

To verify that Elasticsearch is running, use curl to send an HTTP request to 
```Curl
curl -X GET "localhost:9200/"
```
**Step 3**: Configure Elasticsearch
```Shell
sudo vi /etc/elasticsearch/elasticsearch.yml
```
Set an ip address to expose this node on network, Here we are opened all the address.
```yaml
network.host: 0.0.0.0
```
After edited the file, restart the service
```Shell
sudo systemctl restart elasticsearch
```
Now the Elasticsearch is ready!!!

# Install and configure Kibana on Amazon Linux 2

Download and install kibana 
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.17.2-x86_64.rpm
```
```Shell
sudo rpm --install kibana-7.17.2-x86_64.rpm
```
Enable the service 
```Shell
sudo systemctl enable kibana
```
Now add the line into this: `sudo vi /etc/kibana/kibana.yml`
```Shell
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://localhost:9200"]
```
Run the command:
```Shell
sudo systemctl restart kibana
```
```Shell
sudo systemctl status kibana
```

Now Kibana is ready!!!

# Setup minimal security for Elasticsearch

Refer this documentaion and configure basic authentication. [Setup minimal securtiy for Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/7.17/security-minimal-setup.html).

Save the generated passwords. You’ll need them to add the built-in user to Kibana.
