CustomerAccounts
================

For the full XML representation of users, [check out the data reference](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/data_reference.md#customer_account).

The account API is currently just for reading, not writing. Any authenticated user has access.

<!-- 
      customer_accounts GET    /customer_accounts(.:format)           customer_accounts#index
                        POST   /customer_accounts(.:format)           customer_accounts#create
   new_customer_account GET    /customer_accounts/new(.:format)       customer_accounts#new
  edit_customer_account GET    /customer_accounts/:id/edit(.:format)  customer_accounts#edit
       customer_account GET    /customer_accounts/:id(.:format)       customer_accounts#show
                        PUT    /customer_accounts/:id(.:format)       customer_accounts#update
                        DELETE /customer_accounts/:id(.:format)       customer_accounts#destroy
 -->


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