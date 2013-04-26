CustomerAccounts
================

The account API is currently just for reading, not writing. Any authenticated user has access.

Get account
-----------

* `GET /customer_account.xml` returns info about the current user’s Highrise account.

This endpoint includes:

* id
* company name
* first name, last name
* salutation
* contact title
* Street address, city, State, zip
* a telephone number, and an alternate telephone number
* email address
* purchase order


**Response:**

``` xml
<account>
  <id type="integer">1</id>
  <company_name>Your Company</company_name>
  <first_name>John</first_name>
  <last_name>Doe</last_name>
  <salutation>Hi</salutation>
  <contact_title>CEO</contact_title>
  <street_address>Your Address</street_address>
  <city>Your City</city>
  <state>Your State</state>
  <zip>Your ZIP Code</zip>
  <country>Your ZIP Code</country>
  <telephone_1>Your Primary Phone Number</telephone_1>
  <telephone_2>Your Secondary Phone Number</telephone_2>
  <industry>Your Industry</industry>
  ...
  
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```