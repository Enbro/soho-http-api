---
title: Enbro Soho HTTP API
language_tabs:
  - json: JSON
  - shell: cURL
---

Enbro Soho HTTP API.

The enbro soho system can find new gas and electricity offers for a customer if it has all the necessary data.
Therefore the API allows you to create customers and provide all the necessary data for them,
including data of their EAN records.

According to customer records you can:

- Create new customers for your organisation through the API.
  The created customers are treated by the system the same way
  as the customers who registered using enbro soho registration forms.
- Get a list of the customers that have been created for the organisation.
- Get attributes of a customer by his ID.

When you have an ID of a customer, you can use it to create EAN records for him.

# Customers

    Allows to manage list of customers of the current organisation.
    Current organisation defined based on a provided API token.
    You can provide an API token using `Authorization` request header.

    For example: `Authorization: Bearer 2453797fc41e0cfa5c7a00f5acfd6915`


## CREATE 201 Created

Creates a customer for the current organisation and returns it's attributes

### Request

#### Endpoint

```plaintext
POST /api/v1/customers
Content-Type: application/json
Authorization: Bearer 1f987ee6844a3add62d5f4c5fad7961f
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "rudolph_olson@fay.biz",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "190.241.145.224",
    "profile": {
      "first_name": "Danny",
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-08",
      "city": "Goldnerfort",
      "street": "26206 Cole Crossroad",
      "building": "124",
      "building_addon": "Suite 599",
      "postal_code": "48191",
      "language": "en"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must be not registered before. |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
| customer[registered_from_ip] *required* | Customer registered from ip |
| customer[profile] *required* | Attributes for the profile of a customer |
| customer[profile][first_name] *required* | Customer profile first name |
| customer[profile][last_name] *required* | Customer profile last name |
| customer[profile][title] *required* | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| customer[profile][phone] *required* | Example: "+3256980144". Customer profile phone |
| customer[profile][birth_date] *required* | Example: "2000-04-06". Customer profile birth date |
| customer[profile][city] *required* | Customer profile city |
| customer[profile][street] *required* | Customer profile street |
| customer[profile][building] *required* | Customer profile building |
| customer[profile][building_addon]  | Customer profile building addon |
| customer[profile][postal_code] *required* | Customer profile postal code |
| customer[profile][language]  | Values: ["nl", "fr", "en"]. Default: "nl". Customer profile language |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
{
  "id": 5,
  "email": "rudolph_olson@fay.biz",
  "created_at": "2020-04-08T11:37:15.978Z",
  "updated_at": "2020-04-08T11:37:16.044Z",
  "organisation": {
    "id": 5,
    "name": "Dooley LLC",
    "domain": "torphyaufderhar-hanecrooks-3",
    "created_at": "2020-04-08T11:37:15.906Z"
  },
  "profile": {
    "id": 5,
    "customer_id": 5,
    "title": "mr",
    "first_name": "Danny",
    "last_name": "Ocean",
    "birth_date": "2000-04-08",
    "phone": "+3256980144",
    "city": "Goldnerfort",
    "street": "26206 Cole Crossroad",
    "building": "124",
    "building_addon": "Suite 599",
    "postal_code": "48191",
    "language": "en",
    "created_at": "2020-04-08T11:37:15.981Z",
    "updated_at": "2020-04-08T11:37:15.981Z"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## CREATE 422 Validation Error

          At least one of the specified parameters contains an error.
          Check if all the required parameters have been specified.
          Also the specified email must be unique.
          You can find details about the error in the response.


### Request

#### Endpoint

```plaintext
POST /api/v1/customers
Content-Type: application/json
Authorization: Bearer 40ffd9c0282b540713abb5b50d70ecd9
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "carlie.lakin@hicklefritsch.org",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "100.161.13.144",
    "profile": {
      "first_name": null,
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-08",
      "city": "Lake Eleneshire",
      "street": "302 Louie Walks",
      "building": "9404",
      "building_addon": "Apt. 643",
      "postal_code": "32561-1800",
      "language": "nl"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must be not registered before. |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
| customer[registered_from_ip] *required* | Customer registered from ip |
| customer[profile] *required* | Attributes for the profile of a customer |
| customer[profile][first_name] *required* | Customer profile first name |
| customer[profile][last_name] *required* | Customer profile last name |
| customer[profile][title] *required* | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| customer[profile][phone] *required* | Example: "+3256980144". Customer profile phone |
| customer[profile][birth_date] *required* | Example: "2000-04-06". Customer profile birth date |
| customer[profile][city] *required* | Customer profile city |
| customer[profile][street] *required* | Customer profile street |
| customer[profile][building] *required* | Customer profile building |
| customer[profile][building_addon]  | Customer profile building addon |
| customer[profile][postal_code] *required* | Customer profile postal code |
| customer[profile][language]  | Values: ["nl", "fr", "en"]. Default: "nl". Customer profile language |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "path": "customer.profile.first_name",
      "error": "must_be_filled",
      "message": "must be filled",
      "type": "params"
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| errors | Type: *array*. Items type: *object*. Contains a list of occurred errors |
| path | A full name of an erroneous field |
| error | A string identifier of the error |
| message | An error message |
| type | A type of the error |


## LIST 200 OK

Returns customers of the current organisation.
Current organisation defined based on provided API token.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers?page=1&amp;per=2
Content-Type: application/json
Authorization: Bearer 4310d45f6dc16ff00499d39e5afcfedc
```

`GET /api/v1/customers`

#### Parameters


```json
page: 1
per: 2
```


| Name | Description |
|:-----|:------------|
| page  |  page |
| per  | Limit of records per page. Max value is 25. |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
{
  "current_page": 1,
  "limit_value": 2,
  "next_page": 2,
  "prev_page": null,
  "total_pages": 2,
  "records": [
    {
      "id": 14,
      "email": "clay.rice@skilepencer.org",
      "created_at": "2020-04-08T11:37:16.641Z",
      "updated_at": "2020-04-08T11:37:16.641Z",
      "organisation": {
        "id": 20,
        "name": "Ruecker, Doyle and Hayes",
        "domain": "krajciklarkin-franeckihoeger-13",
        "created_at": "2020-04-08T11:37:16.634Z"
      },
      "profile": {
        "id": 14,
        "customer_id": 14,
        "title": "mr",
        "first_name": "Jed",
        "last_name": "Yundt",
        "birth_date": "1983-04-09",
        "phone": "+3232411132",
        "city": "Deonmouth",
        "street": "Felix Lakes",
        "building": "509",
        "building_addon": "Suite 871",
        "postal_code": "15027",
        "language": "fr",
        "created_at": "2020-04-08T11:37:16.651Z",
        "updated_at": "2020-04-08T11:37:16.651Z"
      }
    },
    {
      "id": 16,
      "email": "reuben@jaskolski.com",
      "created_at": "2020-04-08T11:37:16.686Z",
      "updated_at": "2020-04-08T11:37:16.686Z",
      "organisation": {
        "id": 20,
        "name": "Ruecker, Doyle and Hayes",
        "domain": "krajciklarkin-franeckihoeger-13",
        "created_at": "2020-04-08T11:37:16.634Z"
      },
      "profile": {
        "id": 16,
        "customer_id": 16,
        "title": "mr",
        "first_name": "Charlott",
        "last_name": "O'Keefe",
        "birth_date": "1969-03-08",
        "phone": "+3232411132",
        "city": "Murphyhaven",
        "street": "Swaniawski Vista",
        "building": "257",
        "building_addon": "Apt. 306",
        "postal_code": "65102-7546",
        "language": "fr",
        "created_at": "2020-04-08T11:37:16.696Z",
        "updated_at": "2020-04-08T11:37:16.696Z"
      }
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| current_page | The current page number |
| limit_value | Limit of records on a page |
| next_page | The next page number |
| prev_page | The previous page number |
| total_pages | Total available pages |
| records | The list of found records |
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## SHOW 200 OK

          Returns the attributes of the customer with provided ID.
          The customer must belong to the current organisation.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers/8
Content-Type: application/json
Authorization: Bearer 7ea5b0662a77dcc11e8ea5c0bb426ad4
```

`GET /api/v1/customers/:id`

#### Parameters



| Name | Description |
|:-----|:------------|
| id *required* | Type: *integer*. ID of a customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
{
  "id": 8,
  "email": "marylou_gutkowski@armstrong.net",
  "created_at": "2020-04-08T11:37:16.401Z",
  "updated_at": "2020-04-08T11:37:16.401Z",
  "organisation": {
    "id": 11,
    "name": "Lakin Group",
    "domain": "marks-rowe-7",
    "created_at": "2020-04-08T11:37:16.395Z"
  },
  "profile": {
    "id": 8,
    "customer_id": 8,
    "title": "mr",
    "first_name": "Lise",
    "last_name": "Beier",
    "birth_date": "1975-03-21",
    "phone": "+3232411132",
    "city": "Pacochaburgh",
    "street": "Lanora Brooks",
    "building": "597",
    "building_addon": "Suite 514",
    "postal_code": "60999",
    "language": "nl",
    "created_at": "2020-04-08T11:37:16.407Z",
    "updated_at": "2020-04-08T11:37:16.407Z"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the customer |
| email | Unique email of the customer |
| organisation | Attributes of the organisation to which the customer belongs to |
| organisation[id] | ID of the customer's organisation |
| organisation[name] | Name of the organisation |
| organisation[domain] | Domain of the organisation. Usually it's a subdomain under the parent organisation's domain |
| organisation[created_at] | Date and time when the organisation has been created |
| profile[id] | ID of the customer's profile |
| profile[customer_id] | ID of the customer to whom the profile belongs to |
| profile[title] | Values: ["mr", "mrs"]. Example: "mr". Customer profile title |
| profile[first_name] | The customer's first name |
| profile[last_name] | The customer's last name |
| profile[birth_date] | The customer's birth date |
| profile[phone] | Example: "+32460123456". The phone number (full format - only country code with digits) |
| profile[city] | The customer's address - city |
| profile[street] | The customer's address - street |
| profile[building] | The customer's address - building |
| profile[building_addon] | The customer's address - buildin addon |
| profile[postal_code] | The customer's address - zip code |
| profile[language] | Values: ["nl", "fr", "en"]. Customer profile language |
| profile[created_at] | Date and time when the customer profile has been created |
| profile[updated_at] | Date and time when the customer profile has been updated |


## SHOW 404 Not Found

          A customer with specified ID haven't been found.
          The customer must belong to the current organisation.
          Current organisation defined based on provided API token.


### Request

#### Endpoint

```plaintext
GET /api/v1/customers/14
Content-Type: application/json
Authorization: Bearer 15c34e179870c50ee3c3ae771c8e5a97
```

`GET /api/v1/customers/:id`

#### Parameters



| Name | Description |
|:-----|:------------|
| id *required* | Type: *integer*. ID of a customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
404 Not Found
```


```json
"Not found"
```



# Customers / Eans

    Allows to create an EAN record and get the list of EAN records for a customer.
    While a customer doesn't have any EAN records it's not possible to find an offer for him.

    You must specify an ID of a customer and provide all the necessary data.
    The customer must belong to the current organisation.
    Current organisation defined based on a provided API token.
    You can provide an API token using `Authorization` request header.

    For example: `Authorization: Bearer 2453797fc41e0cfa5c7a00f5acfd6915`


## CREATE 201 Created

Create an EAN record for the specified customer

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/36/eans
Content-Type: application/json
Authorization: Bearer dc045083ea01e01db8308e65c9bcd0a3
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 10,
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "recording_period": "february",
    "solar_panels": "true",
    "inverter_max_power": "315",
    "contract_end_date": "2020-10-08",
    "fixed_fee": "1.00",
    "tariff_group": "mono",
    "wkk": "0.00341",
    "gsc": "0.0214"
  }
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| ean *required* | Attributes for the EAN record |
| ean[number]  | EAN number |
| ean[product]  | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. Must be a value from the enum. |
| ean[supplier_id]  | ID of the supplier for the EAN connection |
| ean[building]  | The address for the EAN connection - building addon |
| ean[building_addon]  | The address of the EAN connection - street |
| ean[street]  | The address for the EAN connection - building |
| ean[city]  | The address of the EAN connection - city |
| ean[postal_code]  | The address of the EAN connection - postal_code |
| ean[consumptions]  | The consumptions for the EAN connection |
| ean[consumptions][name]  | Name of the tariff |
| ean[consumptions][volume]  | A consumption volume by the tariff |
| ean[consumptions][price]  | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN (Meter check period). Available values: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only then solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee]  | Fixed fee a year charged per EAN connection |
| ean[tariff_group]  | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| ean[wkk]  | Ean wkk |
| ean[gsc]  | Ean gsc |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
{
  "id": 6,
  "customer_id": 36,
  "number": "542170967180397340",
  "product": "electricity",
  "reason": "normal",
  "building": "15",
  "building_addon": "A",
  "street": "street name",
  "city": "Kiev",
  "state": "ready",
  "postal_code": "2443",
  "consumptions": [
    {
      "name": "mono",
      "volume": "22.25",
      "price": "0.15"
    }
  ],
  "solar_panels": true,
  "inverter_max_power": 315,
  "contract_end_date": "2020-10-08",
  "fixed_fee": "1.0",
  "tariff_group": "mono",
  "recording_period": "february",
  "wkk": "0.00341",
  "gsc": "0.0214",
  "created_at": "2020-04-08T11:37:17.789Z",
  "supplier": {
    "id": 10,
    "name": "Donnelly-Reichel 10"
  }
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the EAN record |
| customer_id | ID of the customer to whom the EAN record belongs to |
| number | An EAN number of record |
| product | Values: ["gas", "electricity"]. The EAN record's product |
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. |
| state | The current status of the EAN record |
| building | The address of the EAN connection - building |
| building_addon | The address of the EAN connection - building addon |
| street | The address of the EAN connection - street |
| city | The address of the EAN connection - city |
| postal_code | The address of the EAN connection - postal_code |
| consumptions | The consumptions of the EAN connection |
| consumptions | The consumptions of the EAN connection. |
| consumptions[name] | Name of the tariff |
| consumptions[volume] | A consumption volume by the tariff |
| consumptions[price] | A price for the tariff |
| solar_panels | Type: *boolen*. For the *electricity* product only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only then solar panels flag is true |
| contract_end_date | The date when the contract for the EAN connection ends |
| fixed_fee | Fixed fee a year charged per EAN connection |
| tariff_group | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| wkk |  wkk |
| gsc |  gsc |
| created_at | Date and time when the EAN record has been created |
| supplier[id] | ID of the supplier of the EAN connection |
| supplier[name] | Name of the supplier of the EAN connection |


## CREATE 422 Validation Error

          At least one of the specified parameters contains an error.
          Check if all the required parameters have been specified.
          Also the specified EAN number must be unique.
          You can find details about the error in the response.


### Request

#### Endpoint

```plaintext
POST /api/v1/customers/35/eans
Content-Type: application/json
Authorization: Bearer 6afa2947a9265446d023662dd10d27a8
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 8,
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "recording_period": "february",
    "solar_panels": "true",
    "inverter_max_power": "315",
    "contract_end_date": "2020-10-08",
    "fixed_fee": "1.00",
    "tariff_group": "mono",
    "wkk": "0.00341",
    "gsc": "0.0214"
  }
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| ean *required* | Attributes for the EAN record |
| ean[number]  | EAN number |
| ean[product]  | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. Must be a value from the enum. |
| ean[supplier_id]  | ID of the supplier for the EAN connection |
| ean[building]  | The address for the EAN connection - building addon |
| ean[building_addon]  | The address of the EAN connection - street |
| ean[street]  | The address for the EAN connection - building |
| ean[city]  | The address of the EAN connection - city |
| ean[postal_code]  | The address of the EAN connection - postal_code |
| ean[consumptions]  | The consumptions for the EAN connection |
| ean[consumptions][name]  | Name of the tariff |
| ean[consumptions][volume]  | A consumption volume by the tariff |
| ean[consumptions][price]  | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN (Meter check period). Available values: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For *electricity* only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only then solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee]  | Fixed fee a year charged per EAN connection |
| ean[tariff_group]  | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| ean[wkk]  | Ean wkk |
| ean[gsc]  | Ean gsc |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "error": "has_already_been_added_to_customer",
      "message": "has already been added to customer",
      "path": "ean.number",
      "type": "params"
    },
    {
      "error": "has_already_been_taken",
      "message": "has already been taken",
      "path": "ean.number",
      "type": "params"
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| errors | Type: *array*. Items type: *object*. Contains a list of occurred errors |
| path | A full name of an erroneous field |
| error | A string identifier of the error |
| message | An error message |
| type | A type of the error |


## LIST 200 OK

Returns available EAN records for the specified customer

### Request

#### Endpoint

```plaintext
GET /api/v1/customers/37/eans
Content-Type: application/json
Authorization: Bearer a788659c941a6ed05e3e9e9000ddee59
```

`GET /api/v1/customers/:customer_id/eans`

#### Parameters



| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
200 OK
```


```json
[
  {
    "id": 7,
    "customer_id": 37,
    "number": "548515259063953554",
    "product": "electricity",
    "reason": "normal",
    "building": "8413",
    "building_addon": "Suite 520",
    "street": "Gutmann Turnpike",
    "city": "Gutkowskiberg",
    "state": "ready",
    "postal_code": "82161-4900",
    "solar_panels": false,
    "inverter_max_power": 1846,
    "fixed_fee": "21.0",
    "tariff_group": "monoExclusive",
    "recording_period": "january",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-08T11:37:17.884Z",
    "supplier": {
      "id": 11,
      "name": "Harris LLC 11"
    }
  },
  {
    "id": 8,
    "customer_id": 37,
    "number": "546787317406942656",
    "product": "electricity",
    "reason": "normal",
    "building": "27151",
    "building_addon": "Suite 358",
    "street": "Stacy Mall",
    "city": "Randiview",
    "state": "ready",
    "postal_code": "96507",
    "solar_panels": true,
    "inverter_max_power": 964,
    "fixed_fee": "38.0",
    "tariff_group": "dual",
    "recording_period": "january",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-08T11:37:17.890Z",
    "supplier": {
      "id": 11,
      "name": "Harris LLC 11"
    }
  }
]
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the EAN record |
| customer_id | ID of the customer to whom the EAN record belongs to |
| number | An EAN number of record |
| product | Values: ["gas", "electricity"]. The EAN record's product |
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. |
| state | The current status of the EAN record |
| building | The address of the EAN connection - building |
| building_addon | The address of the EAN connection - building addon |
| street | The address of the EAN connection - street |
| city | The address of the EAN connection - city |
| postal_code | The address of the EAN connection - postal_code |
| consumptions | The consumptions of the EAN connection |
| consumptions | The consumptions of the EAN connection. |
| consumptions[name] | Name of the tariff |
| consumptions[volume] | A consumption volume by the tariff |
| consumptions[price] | A price for the tariff |
| solar_panels | Type: *boolen*. For the *electricity* product only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only then solar panels flag is true |
| contract_end_date | The date when the contract for the EAN connection ends |
| fixed_fee | Fixed fee a year charged per EAN connection |
| tariff_group | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| wkk |  wkk |
| gsc |  gsc |
| created_at | Date and time when the EAN record has been created |
| supplier[id] | ID of the supplier of the EAN connection |
| supplier[name] | Name of the supplier of the EAN connection |


# Customers / Eans / Bulk

    Allows to create multiple EAN records for a specified customer.
    While a customer doesn't have any EAN records it's not possible to find an offer for him.

    You must specify an ID of a customer and provide all the necessary data.
    The customer must belong to the current organisation.
    Current organisation defined based on a provided API token.
    You can provide an API token using `Authorization` request header.

    For example: `Authorization: Bearer 2453797fc41e0cfa5c7a00f5acfd6915`


## CREATE 201 Created

Create multiple EAN records at once. The records will belong to the specified customer

### Request

#### Endpoint

```plaintext
POST /api/v1/customers/29/eans/bulk
Content-Type: application/json
Authorization: Bearer 6bae71aa8ee84af90a5a6bc351713b19
```

`POST /api/v1/customers/:customer_id/eans/bulk`

#### Parameters


```json
{
  "eans": [
    {
      "ean": {
        "product": "electricity",
        "number": "542170967180397340",
        "reason": "normal",
        "supplier_id": 1,
        "street": "street name",
        "building": "15",
        "building_addon": "A",
        "postal_code": "2443",
        "city": "Kiev",
        "consumptions": [
          {
            "name": "mono",
            "volume": "22.25",
            "price": "0.15"
          }
        ],
        "fixed_fee": "1.00",
        "solar_panels": "true",
        "recording_period": "february",
        "contract_end_date": "2020-10-08",
        "respect_contract_end_date": true,
        "tariff_group": "mono",
        "gsc": "0.0214",
        "wkk": "0.00341",
        "inverter_max_power": "315"
      }
    }
  ]
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| eans *required* | An array of EAN records with attributes |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
[
  {
    "id": 1,
    "customer_id": 29,
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "building": "15",
    "building_addon": "A",
    "street": "street name",
    "city": "Kiev",
    "state": "ready",
    "postal_code": "2443",
    "consumptions": [
      {
        "name": "mono",
        "volume": "22.25",
        "price": "0.15"
      }
    ],
    "solar_panels": true,
    "inverter_max_power": 315,
    "contract_end_date": "2020-10-08",
    "fixed_fee": "1.0",
    "tariff_group": "mono",
    "recording_period": "february",
    "wkk": "0.00341",
    "gsc": "0.0214",
    "created_at": "2020-04-08T11:37:17.380Z",
    "supplier": {
      "id": 1,
      "name": "Ruecker-Wolff 1"
    }
  }
]
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| id | ID of the EAN record |
| customer_id | ID of the customer to whom the EAN record belongs to |
| number | An EAN number of record |
| product | Values: ["gas", "electricity"]. The EAN record's product |
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the customer is searching for a new offer. |
| state | The current status of the EAN record |
| building | The address of the EAN connection - building |
| building_addon | The address of the EAN connection - building addon |
| street | The address of the EAN connection - street |
| city | The address of the EAN connection - city |
| postal_code | The address of the EAN connection - postal_code |
| consumptions | The consumptions of the EAN connection |
| consumptions | The consumptions of the EAN connection. |
| consumptions[name] | Name of the tariff |
| consumptions[volume] | A consumption volume by the tariff |
| consumptions[price] | A price for the tariff |
| solar_panels | Type: *boolen*. For the *electricity* product only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only then solar panels flag is true |
| contract_end_date | The date when the contract for the EAN connection ends |
| fixed_fee | Fixed fee a year charged per EAN connection |
| tariff_group | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| wkk |  wkk |
| gsc |  gsc |
| created_at | Date and time when the EAN record has been created |
| supplier[id] | ID of the supplier of the EAN connection |
| supplier[name] | Name of the supplier of the EAN connection |


## CREATE 422 Validation Error

          At least one of the specified parameters contains an error.
          Check if all the required parameters have been specified.
          Also the specified EAN numbers must be unique.
          You can find details about the error in the response.


### Request

#### Endpoint

```plaintext
POST /api/v1/customers/30/eans/bulk
Content-Type: application/json
Authorization: Bearer 5413f4427bf394a155e9ed17fee6e034
```

`POST /api/v1/customers/:customer_id/eans/bulk`

#### Parameters


```json
{
  "eans": [
    {
      "ean": {
        "product": "electricity",
        "number": "542170967180397340",
        "reason": "normal",
        "supplier_id": 2,
        "street": "street name",
        "building": "15",
        "building_addon": "A",
        "postal_code": "2443",
        "city": "Kiev",
        "consumptions": [
          {
            "name": "mono",
            "volume": "22.25",
            "price": "0.15"
          }
        ],
        "fixed_fee": "1.00",
        "solar_panels": "true",
        "recording_period": "february",
        "contract_end_date": "2020-10-08",
        "respect_contract_end_date": true,
        "tariff_group": "mono",
        "gsc": "0.0214",
        "wkk": "0.00341",
        "inverter_max_power": "315"
      }
    }
  ]
}
```


| Name | Description |
|:-----|:------------|
| customer_id *required* | ID of the customer |
| eans *required* | An array of EAN records with attributes |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
422 Unprocessable Entity
```


```json
{
  "errors": [
    {
      "error": "has_already_been_added_to_customer",
      "message": "has already been added to customer",
      "path": "ean.number",
      "type": "params",
      "index": 0
    },
    {
      "error": "has_already_been_taken",
      "message": "has already been taken",
      "path": "ean.number",
      "type": "params",
      "index": 0
    }
  ]
}
```



#### Fields

| Name       | Description         |
|:-----------|:--------------------|
| errors | Type: *array*. Items type: *object*. Contains a list of occurred errors |
| path | A full name of an erroneous field |
| error | A string identifier of the error |
| message | An error message |
| type | A type of the error |


