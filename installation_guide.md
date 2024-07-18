# Elasticsearch Metricbeat Kibana Installation Guide for AlmaLinux 8.6

## Prerequisites
- A server running AlmaLinux 8.6
- Root or sudo user privileges
- Network access to the server

## Step 1: Update the System
Start by updating the system to ensure all packages are up to date:

```sh
sudo dnf update -y


## Step 2: Install Java
Elasticsearch requires Java. Install OpenJDK 11:

```sh
sudo dnf install java-11-openjdk-devel -y
```
Verify the installation:
```sh
java -version
```

## Step 3: Install Elasticsearch
**Import the GPG Key**

Import the Elasticsearch GPG key:
```sh
sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

**Create the Elasticsearch Repository**

Create a repository file for Elasticsearch:
```sh
sudo nano /etc/yum.repos.d/elasticsearch.repo
```

Add the following content to the file:
```plaintext
[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
Save and close the file.

**Install Elasticsearch**

Install Elasticsearch:
```sh
sudo dnf install elasticsearch -y
```

**Enable and Start Elasticsearch**

Enable Elasticsearch to start on boot and start the service:
```sh
sudo systemctl enable elasticsearch
sudo systemctl start elasticsearch
```

**Verify Elasticsearch Status**

Check the status of the Elasticsearch service:
```sh
sudo systemctl status elasticsearch
```

## Step 4: Install Kibana
**Create the Kibana Repository**

Create a repository file for Kibana:
```sh
sudo nano /etc/yum.repos.d/kibana.repo
```

Add the following content to the file:
```plaintext
[kibana-7.x]
name=Kibana repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
Save and close the file.

**Install Kibana**

Install Kibana:
```sh
sudo dnf install kibana -y
```

**Enable and Start Kibana**
Enable Kibana to start on boot and start the service:
```sh
sudo systemctl enable kibana
sudo systemctl start kibana
```

**Verify Kibana Status**
Check the status of the Kibana service:
```sh
sudo systemctl status kibana
```

## Step 5: Install Metricbeat
**Create the Metricbeat Repository**

Create a repository file for Metricbeat:
```sh
sudo nano /etc/yum.repos.d/metricbeat.repo
```

Add the following content to the file:
```plaintext
[elastic-7.x]
name=Elastic repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
Save and close the file.

**Install Metricbeat**
Install Metricbeat:
```sh
sudo dnf install metricbeat -y
```

**Enable and Start Metricbeat**
Enable Metricbeat to start on boot and start the service:
```sh
sudo systemctl enable metricbeat
sudo systemctl start metricbeat
```

**Verify Metricbeat Status**
Check the status of the Metricbeat service:
```sh
sudo systemctl status metricbeat
```
## Step 6: Open Firewall Ports
**Install firewalld (if not installed)**
```sh
sudo dnf install firewalld -y
```
If you have a firewall enabled, you need to allow traffic to the necessary ports:

```sh
sudo firewall-cmd --permanent --add-port=9200/tcp
sudo firewall-cmd --permanent --add-port=5601/tcp
sudo firewall-cmd --reload
```

## Step 7: Configure Elasticsearch, Kibana, and Metricbeat
**Configure Elasticsearch**

Edit the Elasticsearch configuration file:
```sh
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Make any necessary adjustments, such as setting the cluster name and node name. Save and close the file, then restart Elasticsearch:
```sh
sudo systemctl restart elasticsearch
```

**Configure Kibana**
Edit the Kibana configuration file:
```sh
sudo nano /etc/kibana/kibana.yml
```

Set the Elasticsearch URL and any other necessary settings. Save and close the file, then restart Kibana:
```sh
sudo systemctl restart kibana
```

**Configure Metricbeat**
Edit the Metricbeat configuration file:
```sh
sudo nano /etc/metricbeat/metricbeat.yml
```

Configure the Elasticsearch output and any other necessary settings. Save and close the file, then restart Metricbeat:
```sh
sudo systemctl restart metricbeat
```

**Conclusion**
You have successfully installed and configured Elasticsearch, Kibana, and Metricbeat on AlmaLinux 8.6. These steps should help you set up a robust monitoring and analytics platform.

