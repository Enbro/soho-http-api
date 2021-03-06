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
Authorization: Bearer dc0b2997196273d62d344fc5d7dd679d
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "sandie.dickens@ruel.io",
    "external_attrs": {
      "source": "obg",
      "data": {
        "customer": "123456",
        "order": "654321"
      }
    },
    "terms_and_conditions": true,
    "privacy_policy": true,
    "profile": {
      "first_name": "Danny",
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-28",
      "city": "South Clarethachester",
      "street": "28585 Schmeler Trail",
      "building": "731",
      "building_addon": "Suite 539",
      "postal_code": "56021-8617",
      "language": "en"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must not exist in the system. |
| customer[external_attrs]  | Data of an external system which can be stored as json to the customer. Example: `{ source: 'obg', data: { customer: '123456', order: '654321' } }` |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
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
  "id": 36,
  "email": "sandie.dickens@ruel.io",
  "created_at": "2020-04-28T12:43:22.998Z",
  "updated_at": "2020-04-28T12:43:23.033Z",
  "organisation": {
    "id": 34,
    "name": "Huels, Carroll and Grant",
    "domain": "jerde-faylockman-26",
    "created_at": "2020-04-28T12:43:22.953Z"
  },
  "profile": {
    "id": 33,
    "customer_id": 36,
    "title": "mr",
    "first_name": "Danny",
    "last_name": "Ocean",
    "birth_date": "2000-04-28",
    "phone": "+3256980144",
    "city": "South Clarethachester",
    "street": "28585 Schmeler Trail",
    "building": "731",
    "building_addon": "Suite 539",
    "postal_code": "56021-8617",
    "language": "en",
    "created_at": "2020-04-28T12:43:23.000Z",
    "updated_at": "2020-04-28T12:43:23.000Z"
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
Authorization: Bearer 333d2c6cec784e301366b7ea8c00db4a
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "hettie_roob@wildermankshlerin.biz",
    "external_attrs": {
      "source": "obg",
      "data": {
        "customer": "123456",
        "order": "654321"
      }
    },
    "terms_and_conditions": true,
    "privacy_policy": true,
    "profile": {
      "first_name": null,
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-28",
      "city": "East Billy",
      "street": "213 Tianna Route",
      "building": "15328",
      "building_addon": "Suite 707",
      "postal_code": "58645-1268",
      "language": "fr"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must not exist in the system. |
| customer[external_attrs]  | Data of an external system which can be stored as json to the customer. Example: `{ source: 'obg', data: { customer: '123456', order: '654321' } }` |
| customer[terms_and_conditions] *required* | Type: *boolean*. Flag that terms and conditions is accepted |
| customer[privacy_policy] *required* | Type: *boolean*. Flag that the privacy policy is accepted |
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
Authorization: Bearer 6924470508711e95ab7feb89e9c9f28e
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
      "id": 22,
      "email": "alexander.murray@runolfonhartmann.org",
      "created_at": "2020-04-28T12:43:22.670Z",
      "updated_at": "2020-04-28T12:43:22.670Z",
      "organisation": {
        "id": 25,
        "name": "Auer Group",
        "domain": "denesikbraun-torphychristiansen-20",
        "created_at": "2020-04-28T12:43:22.666Z"
      },
      "profile": {
        "id": 19,
        "customer_id": 22,
        "title": "mr",
        "first_name": "Delmer",
        "last_name": "Maggio",
        "birth_date": "1970-06-07",
        "phone": "+3225551212",
        "city": "Lacyview",
        "street": "Jamaal Lodge",
        "building": "71385",
        "building_addon": "Apt. 571",
        "postal_code": "85466-1412",
        "language": "nl",
        "created_at": "2020-04-28T12:43:22.680Z",
        "updated_at": "2020-04-28T12:43:22.680Z"
      }
    },
    {
      "id": 24,
      "email": "pa@schaden.net",
      "created_at": "2020-04-28T12:43:22.699Z",
      "updated_at": "2020-04-28T12:43:22.699Z",
      "organisation": {
        "id": 25,
        "name": "Auer Group",
        "domain": "denesikbraun-torphychristiansen-20",
        "created_at": "2020-04-28T12:43:22.666Z"
      },
      "profile": {
        "id": 21,
        "customer_id": 24,
        "title": "mr",
        "first_name": "Lacy",
        "last_name": "Skiles",
        "birth_date": "1988-11-23",
        "phone": "+3225551212",
        "city": "Mohamedville",
        "street": "Dickinson Cliffs",
        "building": "47178",
        "building_addon": "Suite 472",
        "postal_code": "41080-0286",
        "language": "fr",
        "created_at": "2020-04-28T12:43:22.704Z",
        "updated_at": "2020-04-28T12:43:22.704Z"
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
GET /api/v1/customers/13
Content-Type: application/json
Authorization: Bearer b155d483bb5c267cc6b6bdde55f3e824
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
  "id": 13,
  "email": "erick.grady@luettgen.io",
  "created_at": "2020-04-28T12:43:22.460Z",
  "updated_at": "2020-04-28T12:43:22.460Z",
  "organisation": {
    "id": 16,
    "name": "Brekke-Watsica",
    "domain": "shieldsdurgan-bernhard-14",
    "created_at": "2020-04-28T12:43:22.455Z"
  },
  "profile": {
    "id": 10,
    "customer_id": 13,
    "title": "mr",
    "first_name": "Darren",
    "last_name": "Walter",
    "birth_date": "1992-03-29",
    "phone": "+3225551212",
    "city": "North Leon",
    "street": "Betsy Cove",
    "building": "511",
    "building_addon": "Suite 824",
    "postal_code": "03874-3056",
    "language": "nl",
    "created_at": "2020-04-28T12:43:22.464Z",
    "updated_at": "2020-04-28T12:43:22.464Z"
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
GET /api/v1/customers/17
Content-Type: application/json
Authorization: Bearer b64f37fbf9c6980fbdc2d42f0c1c628a
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
POST /api/v1/customers/7/eans
Content-Type: application/json
Authorization: Bearer c8f9478ebf690db9c5f6675facb926e4
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 7,
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
    "contract_end_date": "2020-10-28",
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
| ean[number] *required* | EAN number |
| ean[product] *required* | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason] *required* | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason of adding of a new EAN to the profile. Must be a value from the enum. |
| ean[supplier_id] *required* | ID of the supplier for the EAN connection |
| ean[building] *required* | The address for the EAN connection - building |
| ean[building_addon]  | The address of the EAN connection - building addon |
| ean[street] *required* | The address for the EAN connection - street |
| ean[city] *required* | The address of the EAN connection - city |
| ean[postal_code] *required* | The address of the EAN connection - postal_code |
| ean[consumptions] *required* | The consumptions for the EAN connection |
| ean[consumptions][name] *required* | Name of the tariff |
| ean[consumptions][volume] *required* | A consumption volume by the tariff |
| ean[consumptions][price] *required* | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN (Meter check period). Available values: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only when solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee] *required* | Fixed fee a year charged per EAN connection |
| ean[tariff_group] *required* | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
| ean[wkk]  | Ean wkk |
| ean[gsc]  | Ean gsc |



### Response

```plaintext
Content-Type: application/json; charset=utf-8
201 Created
```


```json
{
  "id": 7,
  "customer_id": 7,
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
  "contract_end_date": "2020-10-28",
  "fixed_fee": "1.0",
  "tariff_group": "mono",
  "recording_period": "february",
  "wkk": "0.00341",
  "gsc": "0.0214",
  "created_at": "2020-04-28T12:43:22.245Z",
  "supplier": {
    "id": 7,
    "name": "Boyer, Predovic and Lowe 7"
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
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the EAN was added to the profile. |
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
| solar_panels | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only when solar panels flag is true |
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
POST /api/v1/customers/8/eans
Content-Type: application/json
Authorization: Bearer fedf1d67c405649062e045316c66b2b9
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
    "contract_end_date": "2020-10-28",
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
| ean[number] *required* | EAN number |
| ean[product] *required* | Enum: ["gas", "electricity"]. The EAN record's product. Must be a value from the enum |
| ean[reason] *required* | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason of adding of a new EAN to the profile. Must be a value from the enum. |
| ean[supplier_id] *required* | ID of the supplier for the EAN connection |
| ean[building] *required* | The address for the EAN connection - building |
| ean[building_addon]  | The address of the EAN connection - building addon |
| ean[street] *required* | The address for the EAN connection - street |
| ean[city] *required* | The address of the EAN connection - city |
| ean[postal_code] *required* | The address of the EAN connection - postal_code |
| ean[consumptions] *required* | The consumptions for the EAN connection |
| ean[consumptions][name] *required* | Name of the tariff |
| ean[consumptions][volume] *required* | A consumption volume by the tariff |
| ean[consumptions][price] *required* | A price for the tariff |
| ean[recording_period]  | Recording period of the EAN (Meter check period). Available values: ["automatic", "monthly", "january", "february", "march", "april", "may", "june", "july", "august", "september", "october", "november", "december"] |
| ean[solar_panels]  | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only when solar panels flag is true |
| ean[contract_end_date]  | The date when the contract for the EAN connection ends |
| ean[fixed_fee] *required* | Fixed fee a year charged per EAN connection |
| ean[tariff_group] *required* | Values: ["mono", "dual", "monoExclusive", "dualExclusive"]. Tariff group for the EAN connection |
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
GET /api/v1/customers/5/eans
Content-Type: application/json
Authorization: Bearer 1d3a87d5f577104876b54175babfa616
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
    "id": 4,
    "customer_id": 5,
    "number": "547352164405856980",
    "product": "electricity",
    "reason": "reopened",
    "building": "8838",
    "building_addon": "Apt. 685",
    "street": "Willms Field",
    "city": "Prosaccoville",
    "state": "ready",
    "postal_code": "25781",
    "solar_panels": true,
    "inverter_max_power": 1464,
    "fixed_fee": "44.0",
    "tariff_group": "dualExclusive",
    "recording_period": "automatic",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-28T12:43:22.160Z",
    "supplier": {
      "id": 6,
      "name": "Mosciski-Fritsch 6"
    }
  },
  {
    "id": 5,
    "customer_id": 5,
    "number": "546958776477544262",
    "product": "electricity",
    "reason": "new",
    "building": "4008",
    "building_addon": "Suite 143",
    "street": "Rutherford Lock",
    "city": "Marianashire",
    "state": "ready",
    "postal_code": "00099",
    "solar_panels": false,
    "inverter_max_power": 1300,
    "fixed_fee": "50.0",
    "tariff_group": "mono",
    "recording_period": "january",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-28T12:43:22.166Z",
    "supplier": {
      "id": 6,
      "name": "Mosciski-Fritsch 6"
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
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the EAN was added to the profile. |
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
| solar_panels | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only when solar panels flag is true |
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
POST /api/v1/customers/1/eans/bulk
Content-Type: application/json
Authorization: Bearer 4053d6a02a5c14fe6fa5f36f2bc13d55
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
        "contract_end_date": "2020-10-28",
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
    "customer_id": 1,
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
    "contract_end_date": "2020-10-28",
    "fixed_fee": "1.0",
    "tariff_group": "mono",
    "recording_period": "february",
    "wkk": "0.00341",
    "gsc": "0.0214",
    "created_at": "2020-04-28T12:43:21.843Z",
    "supplier": {
      "id": 1,
      "name": "Hamill LLC 1"
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
| reason | Values: ["normal", "new", "reopened", "dropped", "moved"]. The reason why the EAN was added to the profile. |
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
| solar_panels | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels. |
| inverter_max_power | Inverter Max Power. Only when solar panels flag is true |
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
POST /api/v1/customers/4/eans/bulk
Content-Type: application/json
Authorization: Bearer f4f43bc758a12f1fbd3bb13d721c4df3
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
        "supplier_id": 4,
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
        "contract_end_date": "2020-10-28",
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


