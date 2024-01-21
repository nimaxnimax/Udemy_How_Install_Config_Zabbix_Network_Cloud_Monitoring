
![Alt text](image.png)

Udemy Course >> How Install Config Zabbix 6 Network Cloud Monitoring Part 1

**********

Complete Crash Course >> Server Network Administration Cloud Monitoring for Free Zabbix 6 for Monitoring Cloud Router Switch Windows Linux VPS P1 (Azure Cloud Test Lab and Local VMware & Virtual-Box Test Lab)

**********

Tips/Tricks/Notes/Commands URL Link:

https://github.com/nimaxnimax/Udemy_How_Install_Config_Zabbix_Network_Cloud_Monitoring/tree/main/Part_1

Instructor & Courses:

https://www.udemy.com/user/adrian-fischer-infotech/

**********

![Alt text](image-1.png)

Lab Requirements:

Option 1 - Cloud
- Azure >> https://azure.microsoft.com/en-us/get-started/azure-portal
- AWS >> https://aws.amazon.com/
- GCP >> https://cloud.google.com/free
- Digitalocean >> https://www.digitalocean.com/

Option 2 - PC Virtualization Options - Installation/Download URL Links (Windows/Linux/Mac):
- VMware Player >> https://www.vmware.com/uk/products/workstation-player/workstation-player-evaluation.html
- Virtual-Box >> https://www.virtualbox.org/wiki/Downloads
- Vagrant >> https://developer.hashicorp.com/vagrant/install
- Ubuntu Download Link >> https://releases.ubuntu.com/jammy/

**********

About Zabbix

Zabbix is an open-source network monitoring and management software designed to monitor the performance and availability of various network services, servers, and other network devices. It provides a centralized platform for monitoring the health and performance of IT infrastructure components in real-time. Here are some key aspects of Zabbix and its advantages:

1. **Monitoring Capabilities:**
   - **Host Monitoring:** Zabbix can monitor various types of network hosts, such as servers, routers, switches, and more.
   - **Service Monitoring:** It can monitor services running on hosts, such as HTTP, FTP, SMTP, and others.
   - **Performance Monitoring:** Zabbix collects and analyzes performance data, allowing administrators to identify bottlenecks and optimize system performance.

2. **Alerting and Notification:**
   - Zabbix can trigger alerts based on predefined thresholds or conditions. This helps in proactive issue identification and resolution.
   - Notification mechanisms include email, SMS, and custom scripts, ensuring that the right people are informed promptly.

3. **Flexible Data Collection:**
   - Zabbix supports various data collection methods, including agent-based monitoring, SNMP (Simple Network Management Protocol), IPMI (Intelligent Platform Management Interface), JMX (Java Management Extensions), and more.
   - This flexibility allows monitoring a wide range of devices and services.

4. **Web-based Interface:**
   - Zabbix provides a web-based interface for configuration, monitoring, and reporting. It is user-friendly and allows easy navigation through different monitoring aspects.

5. **Graphical Representation:**
   - The software offers customizable dashboards and graphical representations of monitored data, making it easier for administrators to analyze trends and patterns.

6. **Scalability:**
   - Zabbix is scalable and can handle large and complex IT environments. It supports distributed monitoring setups and can scale horizontally to accommodate growing infrastructure.

7. **Automation and Scripting:**
   - Zabbix supports automation through the use of scripts and custom actions. This allows administrators to automate routine tasks and responses to specific events.

8. **Community and Support:**
   - Being open-source, Zabbix has an active community of users and developers. Users can benefit from community forums, documentation, and additional plugins or extensions.

9. **Cost-Effective:**
   - As an open-source solution, Zabbix is cost-effective compared to many commercial monitoring tools. It provides robust monitoring capabilities without the need for expensive licensing fees.

10. **Customizable:**
    - Zabbix is highly customizable, allowing users to tailor monitoring configurations to their specific needs. This flexibility is valuable in diverse IT environments.

Zabbix is a powerful and versatile monitoring solution that helps organizations maintain the stability and performance of their IT infrastructure while offering cost-effective alternatives to proprietary monitoring tools.

**********

More Technical Information about Zabbix

Zabbix uses several port numbers for communication between its components and for monitoring various services. Here are some of the important port numbers associated with Zabbix:

1. **Web Interface (HTTP/HTTPS):**
   - Default HTTP port: 80
   - Default HTTPS port: 443

2. **Zabbix Server:**
   - Zabbix server by default uses the following ports:
     - SNMP Trapper: 162/UDP
     - Zabbix Server (communication with Zabbix Web Frontend and Zabbix Proxy): 10051/TCP

3. **Zabbix Proxy:**
   - Zabbix Proxy (communication with Zabbix Server): 10051/TCP

4. **Zabbix Agent:**
   - Zabbix Agent (active mode): 10050/TCP
   - Zabbix Agent (passive mode): 10050/TCP or UDP

5. **SNMP (Simple Network Management Protocol):**
   - SNMP Port: 161/UDP

6. **Java Management Extensions (JMX):**
   - Default JMX Port: 10052/TCP

7. **Database Connection (if using a separate database server):**
   - Default MySQL Port (if using MySQL as the database): 3306/TCP
   - Default PostgreSQL Port (if using PostgreSQL as the database): 5432/TCP

8. **IPMI (Intelligent Platform Management Interface) for Hardware Monitoring:**
   - IPMI Port: 623/UDP

Note: The default port numbers mentioned above are based on standard installations, and they can be changed during the configuration process if needed. It's important to ensure that firewalls and network configurations allow communication on these ports between the relevant Zabbix components (Server, Proxy, Agents) and the monitored devices. Always refer to the official Zabbix documentation for the most up-to-date and accurate information on port configurations.

**********

How to Install Zabbix 6.0 Ubuntu 22.04 or 20.04

Install Zabbix server, frontend, and agent
```bash
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu$(lsb_release -rs)_all.deb
sudo dpkg -i zabbix-release_6.0-4+ubuntu$(lsb_release -rs)_all.deb
sudo apt update -y
sudo apt -y install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

Configure database - In this installation, I will use password rootDBpass as root password and zabbixDBpass as Zabbix password for DB. Consider changing your password for security reasons. Install MariaDB 10.6 - In your terminal, use the following command to install MariaDB 10.6.
```bash
sudo apt install software-properties-common -y
curl -LsS -O https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
sudo bash mariadb_repo_setup --mariadb-server-version=10.6
sudo apt update
sudo apt -y install mariadb-common mariadb-server-10.6 mariadb-client-10.6
```

Once the installation is complete, start the MariaDB service and enable it to start on boot using the following commands:
```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

Reset root password for database - Secure MySQL/MariaDB by changing the default password for MySQL root:
```bash
sudo mysql_secure_installation
```

Create database
```bash
sudo mysql -uroot -p'rootDBpass' -e "create database zabbix character set utf8mb4 collate utf8mb4_bin;"
sudo mysql -uroot -p'rootDBpass' -e "create user 'zabbix'@'localhost' identified by 'zabbixDBpass';"
sudo mysql -uroot -p'rootDBpass' -e "grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbixDBpass';"
```

Import initial schema and data. - Import database shema for Zabbix server (could last up to 5 minutes):
```bash
sudo zcat /usr/share/zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p'zabbixDBpass' zabbix
```

Enter database password in Zabbix configuration file - Open zabbix_server.conf file with command:
```bash
sudo vi /etc/zabbix/zabbix_server.conf
```

and add database password in this format anywhere in file:
```bash
DBPassword=zabbixDBpass
```

Configure firewall - If you have a UFW firewall installed on Ubuntu, use these commands to open TCP ports: 10050 (agent), 10051 (server), and 80 (frontend):
```bash
sudo ufw allow 10050/tcp
sudo ufw allow 10051/tcp
sudo ufw allow 80/tcp
sudo ufw reload
```

Start Zabbix server and agent processes
```bash
sudo systemctl restart zabbix-server zabbix-agent 
sudo systemctl enable zabbix-server zabbix-agent
```

Configure PHP for Zabbix frontend - Edit file /etc/zabbix/apache.conf:
```bash
sudo vi /etc/zabbix/apache.conf
```

Uncomment 2 lines in apache.conf that starts with “# php_value date.timezone Europe/Riga” by removing symbol # and set the right timezone for your country, for example:
```bash
php_value date.timezone Europe/Amsterdam
```

Restart Apache web server and make it start at system boot
```bash
sudo systemctl restart apache2
sudo systemctl enable apache2
```

Configure web frontend - Connect to your newly installed Zabbix frontend using URL “http://server_ip_or_dns_name/zabbix” to initiate the Zabbix installation wizard. Basically, in this wizard you only need to enter a password for Zabbix DB user and just click “Next step” for everything else. In this guide, I have used a zabbixDBpass as a database password, but if you set something else, be sure to enter the correct password when prompted by the wizard.

Login to frontend using Zabbix default login credentials - Use Zabbix default admin username “Admin” and password “zabbix” (without quotes) to login to Zabbix frontend at URL “http://server_ip_or_dns_name/zabbix” via your browser.

Optimizing Zabbix Server (optional) - Don’t bother with this optimization if you are monitoring a small number of devices, but if you are planning to monitor a large number of devices then continue with this step. Open “zabbix_server.conf” file with command:
```bash
sudo vi /etc/zabbix/zabbix_server.conf
```

Add this configuration anywhere in file:
```bash
StartPollers=100
StartPollersUnreachable=50
StartPingers=50
StartTrappers=10
StartDiscoverers=15
StartPreprocessors=15
StartHTTPPollers=5
StartAlerters=5
StartTimers=2
StartEscalators=2
CacheSize=128M
HistoryCacheSize=64M
HistoryIndexCacheSize=32M
TrendCacheSize=32M
ValueCacheSize=256M
```

This is not a perfect configuration, keep in mind that you can optimize it even more. Let’s say if you don’t use ICMP checks then set the “StartPingers” parameter to 1 or if you don’t use active agents then set “StartTrappers” to 1 and so on. You can find out more about the parameters supported in a Zabbix server configuration file in the official documentation.

https://www.zabbix.com/documentation/4.0/manual/appendix/config/zabbix_proxy

If you try to start the Zabbix server you may receive an error “[Z3001] connection to database 'Zabbix' failed: [1040] Too many connections” in the log “/var/log/zabbix/zabbix_server.log” because we are using more Zabbix server processes than MySQL can handle. We need to increase the maximum permitted number of simultaneous client connections and optimize MySQL – so move to the next step.

Optimizing MySQL / MariaDB database (optional) - Create custom MySQL configuration file - Create file “10_my_tweaks.cnf":
```bash
sudo vi /etc/mysql/mariadb.conf.d/10_my_tweaks.cnf
```

And paste this configuration:
```bash
[mysqld]
max_connections                = 404
innodb_buffer_pool_size        = 800M
innodb-log-file-size           = 128M
innodb-log-buffer-size         = 128M
innodb-file-per-table          = 1
innodb_buffer_pool_instances   = 8
innodb_old_blocks_time         = 1000
innodb_stats_on_metadata       = off
innodb-flush-method            = O_DIRECT
innodb-log-files-in-group      = 2
innodb-flush-log-at-trx-commit = 2
tmp-table-size                 = 96M
max-heap-table-size            = 96M
open_files_limit               = 65535
max_connect_errors             = 1000000
connect_timeout                = 60
wait_timeout                   = 28800
```

And set the correct file permission:
```bash
sudo chown mysql:mysql /etc/mysql/mariadb.conf.d/10_my_tweaks.cnf
sudo chmod 644 /etc/mysql/mariadb.conf.d/10_my_tweaks.cnf
```

Configuration parameter max_connections must be larger than the total number of all Zabbix proxy processes plus 150. You can use the command below to automatically check the number of Zabbix processes and add 150 to that number:
```bash
sudo egrep "^Start.+=[0-9]" /etc/zabbix/zabbix_server.conf | awk -F "=" '{s+=$2} END {print s+150}'
```

The second most important parameter is innodb_buffer_pool_size, which determines how much memory can MySQL get for caching InnoDB tables and index data. You should set that parameter to 70% of system memory if only database is installed on server. I didn’t have any problems with memory, but if your Zabbix proxy crashes because of lack of memory, reduce “innodb_buffer_pool_size” and restart MySQL server.

Restart Zabbix Server and MySQL service - Stop and start the services in the same order as below:
```bash
sudo systemctl stop zabbix-server
sudo systemctl stop mysql
sudo systemctl start mysql
sudo systemctl start zabbix-server
```

Upgrade between minor versions:
```bash
sudo apt install -y --only-upgrade 'zabbix*'
sudo systemctl restart zabbix-server
```

**********

Swap Configuration on Ubuntu 20 or 22 - Linux Command >>
```bash
sudo apt update -y && sudo apt upgrade -y
sudo fallocate -l 4G /swapfile
ls -anp /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

**********

VB and Vagrant Installation on Ubuntu 22 - Linux Command >>
```bash
sudo apt update -y && sudo apt upgrade -y
wget https://www.virtualbox.org/download/oracle_vbox_2016.asc
cat oracle_vbox_2016.asc | gpg --dearmor | sudo tee /usr/share/keyrings/virtualbox.gpg > /dev/null 2>&1
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/virtualbox.gpg] https://download.virtualbox.org/virtualbox/debian jammy contrib' | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
sudo apt update && sudo apt install virtualbox-7.0 -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant -y
```

```bash
sudo vi Vagrantfile
```

```bash
Vagrant.configure("2") do |config|
    config.vm.define "ubuntu1" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu1"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
end
```

```bash
Vagrant.configure("2") do |config|
    config.vm.define "ubuntu1" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu1"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
    config.vm.define "ubuntu2" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu2"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
    config.vm.define "ubuntu3" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu3"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
end
```

```bash
cat Vagrantfile
```

```bash
vagrant help
vagrant global-status
vagrant up
vagrant ssh [ID]
vagrant destroy [ID]
```

