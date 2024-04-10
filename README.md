
# Magento 2 Store

## Setup plugin
- Run docker compose up

    Go to http://localhost/admin
    ```
    Username: user
    Password: bitnami1
    ```

- Install the plugin:
    ```
    composer require apurata/financing:"0.4.*"
    ```

- Update folder owner

```
sudo chown bitnami:andy -R vendor/apurata
```

- Clone the repo in the folder bitnami/magento/vendor/apurata

```
git clone https://github.com/apurata/magento2-acuotaz-payment-gateway financing
```

## Configure store

- Activate payment method
```
Go to Stores -> Configuration -> Sales -> Payment Methods

Type client_id and token

Save config
```

- Add a product:

```
Go to Products Page -> New products

Fill the required fields, it is important to set th Quantity value

Click save button
```

> Note: The product is not shown in the home section, type it in the search engine

- Update currency:

```
Go to Stores Page -> Settings/Configuration -> Currency Setup

Set Base Currency and Allowed Currencies to PEN

Click Save Config button
```