
# ZUMI APP

This is a deployment repo for Kalio Sobomabo technical assesment. The application API is located at https://github.com/sobomabo/zumi_api, and the application frontend is located at https://github.com/sobomabo/zumi_app.
## API Reference

#### Get all orders

```http
  GET /api/orders
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `vendor` | `string` | **Required**. Order venbor ID |
| `search` | `string` | **Optional**. Search string |
| `orderNumber` | `string` | **Optional**. Order number |
| `customerName` | `string` | **Optional**. Order customer name |
| `status` | `string` | **Optional**. Order status |
| `page` | `number` | **Optional**. Pagination request page, default is 0 |
| `limit` | `number` | **Optional**. Pagination page limit, default is 6 |

#### Get Order

```http
  GET /api/orders/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of order to fetch |

#### Updatae Order

```http
  POST /api/orders/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of order to update |

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `customerName`      | `string` | **Optional**. Order customer name |
| `customerAddress`      | `string` | **Optional**. Order customer address |
| `deliveryDate`      | `string` | **Optional**. Confirmed ordeer delivery date |
| `status`      | `string` | **Optional**. Order status |
| `cancelReason`      | `string` | **Optional**. Reason for order cancelation |
| `vendor`      | `string` | **Required**. Order venbor ID |

#### Create Order

```http
  POST /api/orders
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `customerName`      | `string` | **Optional**. Order customer name |
| `customerAddress`      | `string` | **Optional**. Order customer address |
| `deliveryDate`      | `string` | **Optional**. Confirmed ordeer delivery date |
| `status`      | `string` | **Optional**. Order status |
| `cancelReason`      | `string` | **Optional**. Reason for order cancelation |
| `vendor`      | `string` | **Required**. Order venbor ID |
| `orderLines`      | `array` | **Required**. List of objects representing order products {sku: string, name: string, quantity: number, price: number} |

#### List Products

```http
  GET /api/products
```

| Parameters | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `sku`      | `string` | **Optional**. Product number |
| `name`      | `string` | **Optional**. Product name |
| `brand`      | `string` | **Optional**. Product brand name |
| `price`      | `string` | **Optional**. Product brand |
| `quantity`      | `string` | **Optional**. Product quantity |
| `vendor`      | `string` | **Required**. Product vendor ID |
| `search`      | `string` | **Required**. Search steing |
| `status`      | `string` | **Required**. Product status |
| `page` | `number` | **Optional**. Pagination request page, default is 0 |
| `limit` | `number` | **Optional**. Pagination page limit, default is 6 |

#### Get Product

```http
  GET /api/products/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to fetch |

#### Update Product

```http
  POST /api/products/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of product to update |

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `name`      | `string` | **Optional**. Product name |
| `brand`      | `string` | **Optional**. Product brand name |
| `price`      | `string` | **Optional**. Product brand |
| `quantity`      | `string` | **Optional**. Product quantity |
| `vendor`      | `string` | **Required**. Vendor ID of product |

#### Create Product

```http
  POST /api/products
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `sku`      | `string` | **Required**. Product number |
| `name`      | `string` | **Required**. Product name |
| `brand`      | `string` | **Required**. Product brand name |
| `price`      | `string` | **Required**. Product brand |
| `quantity`      | `string` | **Required**. Product quantity |
| `vendor`      | `string` | **Required**. Vendor ID of product |

#### Create User

```http
  POST /api/users/
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `firstName`      | `string` | **Required**. First name of the user |
| `lastname`      | `string` | **Required**. Last name of the user |
| `username`      | `string` | **Required**. Username of the user |
| `password`      | `string` | **Required**. password of the user |

#### Login User

```http
  POST /api/orders/login
```

| Body | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `username`      | `string` | **Required**. Username of the user |
| `password`      | `string` | **Required**. password of the user |



## Deployment

The project has be containerized with docker.

To deploy the project please follow the steps below:

```bash
  git clone https://github.com/sobomabo/zumi_deployment.git
```
A **zumi_deployment** directory will be created  with a docker-compose.yml file inside.

Change into the zumi_deployment directory, and run the command below:

```bash
  docker compose up -d
```
The docker compose file will spin up three containers for
- The ZUMI API (backend) - configured to run on port 3001
- The ZUMI App (frontend) - configured to run on port 3000
- A mongodb container for the database - configured to run on port 27017

The network is at IP: http://127.0.0.1

To seed the  database run

```bash
   docker exec -it zumi_api node seedDB.js 
```
A list of users will be logged to the console for testing.

##### Cheers!