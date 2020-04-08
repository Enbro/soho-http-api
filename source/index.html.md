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
Authorization: Bearer 01ecce3cb6732dc6e5e64f66045c113f
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "marcie@raynor.biz",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "127.197.254.149",
    "profile": {
      "first_name": "Danny",
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-08",
      "city": "South Fermin",
      "street": "1288 Marquardt Course",
      "building": "42630",
      "building_addon": "Suite 174",
      "postal_code": "01650-4934",
      "language": "fr"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must not exist in the system. |
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
  "id": 26,
  "email": "marcie@raynor.biz",
  "created_at": "2020-04-08T13:49:04.227Z",
  "updated_at": "2020-04-08T13:49:04.247Z",
  "organisation": {
    "id": 21,
    "name": "Bradtke Inc",
    "domain": "hammesgraham-cummings-16",
    "created_at": "2020-04-08T13:49:04.184Z"
  },
  "profile": {
    "id": 24,
    "customer_id": 26,
    "title": "mr",
    "first_name": "Danny",
    "last_name": "Ocean",
    "birth_date": "2000-04-08",
    "phone": "+3256980144",
    "city": "South Fermin",
    "street": "1288 Marquardt Course",
    "building": "42630",
    "building_addon": "Suite 174",
    "postal_code": "01650-4934",
    "language": "fr",
    "created_at": "2020-04-08T13:49:04.229Z",
    "updated_at": "2020-04-08T13:49:04.229Z"
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
Authorization: Bearer 78cc9766eafe035b75d4f43fd83d0aea
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "jeffry@hammes.co",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "registered_from_ip": "42.130.46.89",
    "profile": {
      "first_name": null,
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-08",
      "city": "Connellyhaven",
      "street": "817 Andre Park",
      "building": "485",
      "building_addon": "Apt. 813",
      "postal_code": "38502-6787",
      "language": "nl"
    }
  }
}
```


| Name | Description |
|:-----|:------------|
| customer[email] *required* | A customer's email. Serves as an unique identifier of a customer. A customer with the same email must not exist in the system. |
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
Authorization: Bearer 451e5b357e0575565b6cf26c9488bec7
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
      "id": 7,
      "email": "mickey.christiansen@sanford.co",
      "created_at": "2020-04-08T13:49:03.812Z",
      "updated_at": "2020-04-08T13:49:03.812Z",
      "organisation": {
        "id": 9,
        "name": "Altenwerth-Funk",
        "domain": "harvey-rippin-8",
        "created_at": "2020-04-08T13:49:03.808Z"
      },
      "profile": {
        "id": 5,
        "customer_id": 7,
        "title": "mr",
        "first_name": "Nia",
        "last_name": "Krajcik",
        "birth_date": "1965-07-26",
        "phone": "+3256980144",
        "city": "Jaskolskiside",
        "street": "Swift Roads",
        "building": "929",
        "building_addon": "Suite 717",
        "postal_code": "15635-6980",
        "language": "nl",
        "created_at": "2020-04-08T13:49:03.816Z",
        "updated_at": "2020-04-08T13:49:03.816Z"
      }
    },
    {
      "id": 9,
      "email": "jalisa@hermancain.org",
      "created_at": "2020-04-08T13:49:03.833Z",
      "updated_at": "2020-04-08T13:49:03.833Z",
      "organisation": {
        "id": 9,
        "name": "Altenwerth-Funk",
        "domain": "harvey-rippin-8",
        "created_at": "2020-04-08T13:49:03.808Z"
      },
      "profile": {
        "id": 7,
        "customer_id": 9,
        "title": "mr",
        "first_name": "Aubrey",
        "last_name": "Haley",
        "birth_date": "1997-07-05",
        "phone": "+3232411132",
        "city": "Farahmouth",
        "street": "Carolyne Crest",
        "building": "9056",
        "building_addon": "Apt. 913",
        "postal_code": "11702-2541",
        "language": "nl",
        "created_at": "2020-04-08T13:49:03.838Z",
        "updated_at": "2020-04-08T13:49:03.838Z"
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
GET /api/v1/customers/29
Content-Type: application/json
Authorization: Bearer af9d6d31bcc04f0c79eae632966fcce6
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
  "id": 29,
  "email": "brittaney@christiansen.info",
  "created_at": "2020-04-08T13:49:04.479Z",
  "updated_at": "2020-04-08T13:49:04.479Z",
  "organisation": {
    "id": 27,
    "name": "Reinger, Conroy and Halvorson",
    "domain": "murphyschmeler-treutel-20",
    "created_at": "2020-04-08T13:49:04.474Z"
  },
  "profile": {
    "id": 27,
    "customer_id": 29,
    "title": "mr",
    "first_name": "Weldon",
    "last_name": "Barrows",
    "birth_date": "1965-05-11",
    "phone": "+3225551212",
    "city": "Cyrusland",
    "street": "Jerrica Street",
    "building": "72532",
    "building_addon": "Suite 357",
    "postal_code": "78001",
    "language": "nl",
    "created_at": "2020-04-08T13:49:04.489Z",
    "updated_at": "2020-04-08T13:49:04.489Z"
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
GET /api/v1/customers/35
Content-Type: application/json
Authorization: Bearer c2c9f2689357d054980da0799600c86c
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
POST /api/v1/customers/1/eans
Content-Type: application/json
Authorization: Bearer b045cd2c477489a90f4149922c4f15f2
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 1,
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
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason of adding of a new EAN to the profile. Must be a value from the enum. |
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
| ean[solar_panels]  | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only when solar panels flag is true |
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
  "contract_end_date": "2020-10-08",
  "fixed_fee": "1.0",
  "tariff_group": "mono",
  "recording_period": "february",
  "wkk": "0.00341",
  "gsc": "0.0214",
  "created_at": "2020-04-08T13:49:03.519Z",
  "supplier": {
    "id": 1,
    "name": "Zulauf, Yost and Considine 1"
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
POST /api/v1/customers/2/eans
Content-Type: application/json
Authorization: Bearer b448b472fbd2314c764839264a6e9c00
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 2,
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
| ean[reason]  | Enum: ["normal", "new", "reopened", "dropped", "moved"]. The reason of adding of a new EAN to the profile. Must be a value from the enum. |
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
| ean[solar_panels]  | Type: *boolen*. For electricity EANs only. A flag that the EAN connection has solar panels.  |
| ean[inverter_max_power]  | Inverter Max Power. Only when solar panels flag is true |
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
GET /api/v1/customers/5/eans
Content-Type: application/json
Authorization: Bearer 3516a9e9fe399dbf57a48c5c643a54d7
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
    "number": "542201118980411876",
    "product": "electricity",
    "reason": "reopened",
    "building": "9378",
    "building_addon": "Suite 519",
    "street": "Boyle Center",
    "city": "Port Jasperland",
    "state": "ready",
    "postal_code": "32006-8890",
    "solar_panels": true,
    "inverter_max_power": 1083,
    "fixed_fee": "20.0",
    "tariff_group": "dual",
    "recording_period": "automatic",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-08T13:49:03.764Z",
    "supplier": {
      "id": 6,
      "name": "Bartell-Hodkiewicz 6"
    }
  },
  {
    "id": 5,
    "customer_id": 5,
    "number": "545791672899549543",
    "product": "electricity",
    "reason": "new",
    "building": "86981",
    "building_addon": "Apt. 702",
    "street": "Mills Square",
    "city": "East Reyes",
    "state": "ready",
    "postal_code": "23925",
    "solar_panels": true,
    "inverter_max_power": 142,
    "fixed_fee": "28.0",
    "tariff_group": "mono",
    "recording_period": "monthly",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-08T13:49:03.768Z",
    "supplier": {
      "id": 6,
      "name": "Bartell-Hodkiewicz 6"
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
POST /api/v1/customers/38/eans/bulk
Content-Type: application/json
Authorization: Bearer 4daa6885407fa3aa20b9f64909330c2d
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
        "supplier_id": 11,
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
    "id": 9,
    "customer_id": 38,
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
    "created_at": "2020-04-08T13:49:04.881Z",
    "supplier": {
      "id": 11,
      "name": "Block-Lind 11"
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
POST /api/v1/customers/37/eans/bulk
Content-Type: application/json
Authorization: Bearer b2efc9639342bc4f88b81b147b7bab72
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
        "supplier_id": 9,
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


