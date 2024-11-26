
# Magento 2 Store

## Setup Store

- Create folders mariadb_data, magento_data and elasticsearch_data

- Update file permisions:

    ```
    sudo chmod -R 777 elasticsearch_data magento_data mariadb_data
    ```

## Setup plugin

- Run docker composer up

- Run dc exec -it magento bash

- Go to bitnami/magento/

- Install the plugin:
    ```
    composer require apurata/financing:"0.4.*"
    ```

- Get credentials from https://commercedeveloper.adobe.com/account/keys

- Clone the repo in the folder bitnami/magento/vendor/apurata

    ```
    git clone https://github.com/apurata/magento2-acuotaz-payment-gateway financing
    ```

- Update folder owner

    ```
    sudo chown myuser:root -R vendor/apurata
    ```

- Update apurata host url, go to Apurata/Financing/Helper/ConfigData.php

    ```
    // Use apurata webserver docker container name
    const APURATA_DOMAIN = 'http://tornado-server:8000';
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

- Go to http://localhost/admin
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
