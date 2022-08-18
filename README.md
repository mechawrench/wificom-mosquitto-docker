# wificom-mosquitto-docker

## Description
This docker-compose file is used to deploy the wificom-mosquitto service.

## Features
- Letsencrypt for SSL certificates
- Mosquitto MQTT broker
- Mosquitto go-auth for authentication and authorization

## Ports (Need to be opened)
- Mosquitto: 1883(Non-SSL), 8883(SSL)
- Letsencrypt: 80, 443

## Instructions
1. Install docker and docker-compose (out of scope to put tutorial here)
1. Ensure you've stood up the WiFiCom webapp and have the admin login
1. Edit config/conf.d/go-auth.conf, replace the following uppercase values with your own
    - auth_opt_mysql_host IP_ADDRESS_OF_WIFICOM_LARAVEL_APP
    - auth_opt_mysql_port 3306
    - auth_opt_mysql_dbname YOUR_DB_NAME
    - auth_opt_mysql_user YOUR_DB_USER
    - auth_opt_mysql_password YOUR_DB_USER_PASSWORD
1. Launch docker-compose and ensure the services are running
    1. ```docker-compose up -d```
    1. ```docker-compose ps```
        - You should see the service as not restarting repeatedly here
    1. Check logs for any errors, in particular with the MYSQL connection
        - ```docker-compose logs -f```
1. Use an external MQTT client to test the connection is good
    1. Register an account and wificom on WiFiCom.dev
    1. Navigate to your newly created wificom and copy the mqtt_password
    1. Launch the MQTT client and connect to the wificom MQTT broker
        - Settings: Username = name when signing up, password = MQTT_PASSWORD in secrets.py for admin user, Port 8883, SSL/TLS ON, Host (your WiFiCom webapp)