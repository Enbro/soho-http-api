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
Authorization: Bearer 30594080d2566e1b940412b5d032778f
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "kiersten@zemlakbergnaum.name",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "profile": {
      "first_name": "Danny",
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-09",
      "city": "West Foster",
      "street": "8725 Morissette Crossing",
      "building": "9335",
      "building_addon": "Suite 946",
      "postal_code": "98001",
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
  "id": 22,
  "email": "kiersten@zemlakbergnaum.name",
  "created_at": "2020-04-09T15:01:20.929Z",
  "updated_at": "2020-04-09T15:01:20.972Z",
  "organisation": {
    "id": 17,
    "name": "Yost-Schamberger",
    "domain": "kuphalhackett-blickblanda-11",
    "created_at": "2020-04-09T15:01:20.882Z"
  },
  "profile": {
    "id": 22,
    "customer_id": 22,
    "title": "mr",
    "first_name": "Danny",
    "last_name": "Ocean",
    "birth_date": "2000-04-09",
    "phone": "+3256980144",
    "city": "West Foster",
    "street": "8725 Morissette Crossing",
    "building": "9335",
    "building_addon": "Suite 946",
    "postal_code": "98001",
    "language": "fr",
    "created_at": "2020-04-09T15:01:20.931Z",
    "updated_at": "2020-04-09T15:01:20.931Z"
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
Authorization: Bearer 53f94624f6bbb61fb60635b9c9700bd4
```

`POST /api/v1/customers`

#### Parameters


```json
{
  "customer": {
    "email": "blake.murphy@buckridge.org",
    "terms_and_conditions": true,
    "privacy_policy": true,
    "profile": {
      "first_name": null,
      "last_name": "Ocean",
      "title": "mr",
      "phone": "+3256980144",
      "birth_date": "2000-04-09",
      "city": "New Gregory",
      "street": "8646 Buford Canyon",
      "building": "1386",
      "building_addon": "Apt. 417",
      "postal_code": "05736-6186",
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
Authorization: Bearer e07b91d18bd54367d20748f990386d8b
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
      "id": 1,
      "email": "lorean@flatley.biz",
      "created_at": "2020-04-09T15:01:20.386Z",
      "updated_at": "2020-04-09T15:01:20.386Z",
      "organisation": {
        "id": 2,
        "name": "Ratke-Pollich",
        "domain": "metz-moen-1",
        "created_at": "2020-04-09T15:01:20.357Z"
      },
      "profile": {
        "id": 1,
        "customer_id": 1,
        "title": "mr",
        "first_name": "Hsiu",
        "last_name": "Ledner",
        "birth_date": "1957-05-16",
        "phone": "+3232411132",
        "city": "Lake Russbury",
        "street": "Bergstrom Orchard",
        "building": "27393",
        "building_addon": "Suite 780",
        "postal_code": "09760-8646",
        "language": "fr",
        "created_at": "2020-04-09T15:01:20.437Z",
        "updated_at": "2020-04-09T15:01:20.437Z"
      }
    },
    {
      "id": 3,
      "email": "linh.jacobson@armstrong.info",
      "created_at": "2020-04-09T15:01:20.457Z",
      "updated_at": "2020-04-09T15:01:20.457Z",
      "organisation": {
        "id": 2,
        "name": "Ratke-Pollich",
        "domain": "metz-moen-1",
        "created_at": "2020-04-09T15:01:20.357Z"
      },
      "profile": {
        "id": 3,
        "customer_id": 3,
        "title": "mr",
        "first_name": "Jennette",
        "last_name": "Cruickshank",
        "birth_date": "2000-03-20",
        "phone": "+3256980144",
        "city": "South Quentinmouth",
        "street": "Wilber Terrace",
        "building": "2192",
        "building_addon": "Apt. 105",
        "postal_code": "86555-3067",
        "language": "fr",
        "created_at": "2020-04-09T15:01:20.461Z",
        "updated_at": "2020-04-09T15:01:20.461Z"
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
GET /api/v1/customers/23
Content-Type: application/json
Authorization: Bearer eee6e53375ed5febdd31ef50f32cb00b
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
  "id": 23,
  "email": "loria_mckenzie@kerluke.biz",
  "created_at": "2020-04-09T15:01:21.175Z",
  "updated_at": "2020-04-09T15:01:21.175Z",
  "organisation": {
    "id": 20,
    "name": "Kuvalis, Berge and Schuppe",
    "domain": "lind-beahan-13",
    "created_at": "2020-04-09T15:01:21.171Z"
  },
  "profile": {
    "id": 23,
    "customer_id": 23,
    "title": "mr",
    "first_name": "Blaine",
    "last_name": "Bauch",
    "birth_date": "1961-08-23",
    "phone": "+3225551212",
    "city": "South Reubenfort",
    "street": "Shields Common",
    "building": "164",
    "building_addon": "Suite 614",
    "postal_code": "14522-1564",
    "language": "fr",
    "created_at": "2020-04-09T15:01:21.179Z",
    "updated_at": "2020-04-09T15:01:21.179Z"
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
GET /api/v1/customers/27
Content-Type: application/json
Authorization: Bearer 61249cee7d430c66beb8f2218a5ac8ce
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
POST /api/v1/customers/32/eans
Content-Type: application/json
Authorization: Bearer 34c4d6dd65ff27d9bec725eb98b845dc
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 5,
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
    "contract_end_date": "2020-10-09",
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
  "id": 3,
  "customer_id": 32,
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
  "contract_end_date": "2020-10-09",
  "fixed_fee": "1.0",
  "tariff_group": "mono",
  "recording_period": "february",
  "wkk": "0.00341",
  "gsc": "0.0214",
  "created_at": "2020-04-09T15:01:21.758Z",
  "supplier": {
    "id": 5,
    "name": "Terry and Sons 5"
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
POST /api/v1/customers/31/eans
Content-Type: application/json
Authorization: Bearer 7216bde8172661b351f1f33c8d5b6da3
```

`POST /api/v1/customers/:customer_id/eans`

#### Parameters


```json
{
  "ean": {
    "number": "542170967180397340",
    "product": "electricity",
    "reason": "normal",
    "supplier_id": 3,
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
    "contract_end_date": "2020-10-09",
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
GET /api/v1/customers/33/eans
Content-Type: application/json
Authorization: Bearer 0300b3a7b32fdfc86ffc8896dba2630e
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
    "customer_id": 33,
    "number": "542394291906836553",
    "product": "electricity",
    "reason": "new",
    "building": "6559",
    "building_addon": "Apt. 338",
    "street": "Bechtelar Ferry",
    "city": "Welchburgh",
    "state": "ready",
    "postal_code": "90165",
    "solar_panels": true,
    "inverter_max_power": 1625,
    "fixed_fee": "19.0",
    "tariff_group": "dual",
    "recording_period": "monthly",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-09T15:01:21.839Z",
    "supplier": {
      "id": 6,
      "name": "Kuvalis-Koss 6"
    }
  },
  {
    "id": 5,
    "customer_id": 33,
    "number": "543787838066271119",
    "product": "electricity",
    "reason": "normal",
    "building": "648",
    "building_addon": "Apt. 134",
    "street": "Williamson Circle",
    "city": "South Freddie",
    "state": "ready",
    "postal_code": "43579",
    "solar_panels": true,
    "inverter_max_power": 151,
    "fixed_fee": "11.0",
    "tariff_group": "mono",
    "recording_period": "automatic",
    "wkk": "0.00425",
    "gsc": "0.0215",
    "created_at": "2020-04-09T15:01:21.844Z",
    "supplier": {
      "id": 6,
      "name": "Kuvalis-Koss 6"
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
Authorization: Bearer e9104b10c70eea2cddee2efc4f2a2300
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
        "contract_end_date": "2020-10-09",
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
    "contract_end_date": "2020-10-09",
    "fixed_fee": "1.0",
    "tariff_group": "mono",
    "recording_period": "february",
    "wkk": "0.00341",
    "gsc": "0.0214",
    "created_at": "2020-04-09T15:01:22.030Z",
    "supplier": {
      "id": 11,
      "name": "Pouros, Armstrong and Dickinson 11"
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
POST /api/v1/customers/35/eans/bulk
Content-Type: application/json
Authorization: Bearer 277632ad939540c86d3edbd580f8c1c7
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
        "supplier_id": 7,
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
        "contract_end_date": "2020-10-09",
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


