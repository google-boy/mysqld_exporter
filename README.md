# Mysqld-Exporter Installation script

## Clone the repo

```
git clone https://github.com/google-boy/mysqld_exporter.git
```

## Run the installation script

```
cd mysqld_exporter
sudo ./mysqld_exporter.sh
```

## Create mysql user for the exporter

```
sudo mysql
```

```
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'Exporter_1280' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'localhost';
```

## Modify exporter configuration `my.cnf`

```
sudo vim /etc/mysqld_exporter/my.cnf
```

With the credentials you created above, for example

```
[client]
user=exporter
password=Exporter_1280
host=localhost
port=3306
```

Restart the exporter

```
sudo systemctl restart mysqld-exporter
```

## Add the IP or URL of the host to prometheus configuration

```
....
job_name: mysqld_exporter
static_configs:
    - targets:
        - ip:9104

....
```

