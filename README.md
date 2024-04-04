# Zabbix Stack with Grafana
This Docker Compose setup includes the following components:

1. **Zabbix Server:** Monitors and collects data from various devices and systems.
1. **Zabbix Frontend (Nginx):** Provides a web interface for managing Zabbix.
1. **Zabbix Agent:** Installed on monitored devices to collect data and send it to the Zabbix server.
1. **Grafana:** A powerful dashboard and visualization tool.

## Features
1. Select multiple metrics by using Regex.
1. Create interactive and reusable dashboards with template variables.
1. Show events on graphs with Annotations.
1. Display active problems with Triggers panel.

## Installation
- Create initial database

Make sure you have database server up and running.
Run the following on your database host.
```
# mysql -uroot -p
password
mysql> create database zabbix_db character set utf8mb4 collate utf8mb4_bin;
mysql> create user zabbix_user@localhost identified by 'zabix@123';
mysql> grant all privileges on zabbix_db.* to zabbix_user@localhost;
mysql> set global log_bin_trust_function_creators = 1;
mysql> quit;
```
- On Zabbix server host import initial schema and data. You will be prompted to enter your newly created password.

```
# zcat zabbix-sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix_user -p zabbix_db
```
- Disable log_bin_trust_function_creators option after importing database schema.
```
# mysql -uroot -p
password
mysql> set global log_bin_trust_function_creators = 0;
mysql> quit; 
```
# Install and configure Zabbix for your platform
- Run the docker-compose file,
```
# docker compose up -d
```
- Install the Zabbix plugin for Grafana using grafana-cli:
For more installation options, refer to the [official documentation](https://grafana.com/docs/plugins/alexanderzobnin-zabbix-app/latest/installation/).

>>**Note:** Ensure that the .env file is updated with the correct variables before running the docker-compose file.

## Getting Started Grafana
1. Login to Grafana in *localhost:3000*.
1. Configure the Zabbix data source in Grafana.
1. Explore the available metrics and create your dashboards.

## Documentation
For detailed information and usage instructions, visit the [Grafana-Zabbix documentation](https://grafana.com/docs/plugins/alexanderzobnin-zabbix-app/latest/configuration/).
