
# Magento 2 Store

## Setup Store

- Create folders mariadb_data, magento_data and elasticsearch_data
    ```
    mkdir mariadb_data magento_data elasticsearch_data
    ```
- Update file permisions:

    ```
    sudo chown -R 1001:100 mariadb_data elasticsearch_data
    ```

## Setup plugin

- Run
    ```
    docker composer up
    dc exec -it magento bash
    ```

- Go to bitnami/magento/

- Install the plugin, follow this instructions: https://github.com/apurata/magento2-acuotaz-payment-gateway

- Get credentials from https://commercedeveloper.adobe.com/account/keys

- Exit from container bash

- Go to the folder magento_data/vendor

    ```
    sudo chown -R $USER:root apurata
    cd apurata && sudo rm -rf financing
    git clone git@github.com:apurata/magento2-acuotaz-payment-gateway.git financing
    ```

- Update folder owner

    ```
    sudo chown -R $USER:root -R financing
    ```

- Update apurata host url, go to Apurata/Financing/Helper/ConfigData.php

    ```
    const APURATA_DOMAIN = 'http://172.17.0.1:9000';
    ```

- Update deploy mode:

    ```
    magento deploy:mode:set developer
    ```

- Create the network:

    ```
    docker network create my_shared_network
    ```

- In the docker-compose of webserser add:

    ```
    networks:
    my_shared_network:
        external: true
    ```

- Connect tornado server and mongo to the network:

    ```
    tornado-server:
        [...]
        networks:
        - my_shared_network
    ```

## Configure store

- Go to http://localhost:8080/admin
    ```
    Username: user
    Password: bitnami1
    ```

- Activate payment method
    ```
    Go to Stores -> Configuration -> Sales -> Payment Methods

    Type client_id and token

    Save config
    ```

- Add a product:

    ```
    Go to Catalog -> Products -> Add product

    Fill the required fields, it is important to set the Quantity value

    Click save button
    ```

> Note: The product is not shown in the home section, type it in the search engine

- Update currency:

    ```
    Go to Stores -> Configuration -> General -> Currency Setup

    Set Base Currency and Allowed Currencies to PEN

    Click Save Config button
    ```
