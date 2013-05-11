CustomerAccounts
================

<!-- 
      customer_accounts GET    /customer_accounts(.:format)           customer_accounts#index
                        POST   /customer_accounts(.:format)           customer_accounts#create
   new_customer_account GET    /customer_accounts/new(.:format)       customer_accounts#new
  edit_customer_account GET    /customer_accounts/:id/edit(.:format)  customer_accounts#edit
       customer_account GET    /customer_accounts/:id(.:format)       customer_accounts#show
                        PUT    /customer_accounts/:id(.:format)       customer_accounts#update
                        DELETE /customer_accounts/:id(.:format)       customer_accounts#destroy
 -->


Get customer_account
-----------

* `GET /customer_account.xml` returns info about the current user’s customer account.

This endpoint includes:

* id
* company name
* first name, last name
* salutation
* contact title
* Street address, city, State, zip, country
* a telephone number, and an alternate telephone number
* email address
* industry
* brand affiliation
* user agreement status
* accounting ID
* billing information
* web address
* purchase order


**Response:**

``` xml
<account>
  <id type="integer">1</id>
  <company_name>Your Company</company_name>
  <first_name>John</first_name>
  <last_name>Doe</last_name>
  <salutation>Mr</salutation>
  <contact_title>CEO</contact_title>
  <street_address>Your Address</street_address>
  <city>Your City</city>
  <state>Your State</state>
  <zip>Your ZIP Code</zip>
  <country>Your ZIP Code</country>
  <telephone_1>Your Primary Phone Number</telephone_1>
  <telephone_2>Your Secondary Phone Number</telephone_2>
  <industry>Your Industry</industry>
  <brand_affiliation>Your Brand Affiliation</brand_affiliation>
  <user_agreement_signed_on> Date You Signed User Agreement</user_agreement_signed_on>
  <accounting_id>Your ID for our Accounting System</accounting_id>
  <billing_first_name>John</billing_first_name>
  <billing_last_name>Doe</billing_last_name>
  <billing_street_address>Billing Street Address</billing_street_address>
  <billing_city>Billing City</billing_city>
  <billing_state>Billing State</billing_state>
  <billing_zip>Billing ZIP Code</billing_zip>
  <billing_country>Billing Country</billing_country>
  <telephone_fax>Billing Address Fax Number</telephone_fax>
  <web_address>Your Website</web_address>
  <purchase_order>Purchase Order</purchase_order>
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```


Get customer_accounts
-------------

* `GET /customer_accounts.xml` returns a collection of customer_accounts that are visible to the authenticated user.

**Response:**

``` xml
<customer_accounts>
  <customer_account>
    ...
  </customer_account>
  <customer_account>
    ...
  </customer_account>
</customer_accounts>
```


Create customer_account
--------------

* `POST /customer_accounts.xml` creates a new customer_account with the currently authenticated user as the author.

The XML for the new customer_account is returned on a successful request with the timestamps recorded and ids for the contact data associated.

As always, the URL for the newly-created customer_account is passed back in the `Location` header.

**Request:**

``` xml
<account>
  <company_name>Your Company</company_name>
  <first_name>John</first_name>
  <last_name>Doe</last_name>
  <salutation>Mr</salutation>
  <contact_title>CEO</contact_title>
  <street_address>Your Address</street_address>
  <city>Your City</city>
  <state>Your State</state>
  <zip>Your ZIP Code</zip>
  <country>Your ZIP Code</country>
  <telephone_1>Your Primary Phone Number</telephone_1>
  <telephone_2>Your Secondary Phone Number</telephone_2>
  <industry>Your Industry</industry>
  <brand_affiliation>Your Brand Affiliation</brand_affiliation>
  <user_agreement_signed_on> Date You Signed User Agreement</user_agreement_signed_on>
  <accounting_id>Your ID for our Accounting System</accounting_id>
  <billing_first_name>John</billing_first_name>
  <billing_last_name>Doe</billing_last_name>
  <billing_street_address>Billing Street Address</billing_street_address>
  <billing_city>Billing City</billing_city>
  <billing_state>Billing State</billing_state>
  <billing_zip>Billing ZIP Code</billing_zip>
  <billing_country>Billing Country</billing_country>
  <telephone_fax>Billing Address Fax Number</telephone_fax>
  <web_address>Your Website</web_address>
  <purchase_order>Purchase Order</purchase_order>
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```

**Response:**

    Status: 201 Created
    Location: https://example.firstmoversadvantage.com/customer_accounts/#{new-customer_account-id}.xml

    <customer_account>
      ...
    </customer_account>


Update customer_account
--------------

* `PUT /customer_accounts/#{id}.xml` updates an existing customer_account with new details from the submitted XML.
<!-- Use `?reload=true` to get XML of the successfully updated customer_account. -->

**Request:**

``` xml
<account>
  <id type="integer">1</id>
  <company_name>Your Company</company_name>
  <first_name>John</first_name>
  <last_name>Doe</last_name>
  <salutation>Mr</salutation>
  <contact_title>CEO</contact_title>
  <street_address>Your Address</street_address>
  <city>Your City</city>
  <state>Your State</state>
  <zip>Your ZIP Code</zip>
  <country>Your ZIP Code</country>
  <telephone_1>Your Primary Phone Number</telephone_1>
  <telephone_2>Your Secondary Phone Number</telephone_2>
  <industry>Your Industry</industry>
  <brand_affiliation>Your Brand Affiliation</brand_affiliation>
  <user_agreement_signed_on> Date You Signed User Agreement</user_agreement_signed_on>
  <accounting_id>Your ID for our Accounting System</accounting_id>
  <billing_first_name>John</billing_first_name>
  <billing_last_name>Doe</billing_last_name>
  <billing_street_address>Billing Street Address</billing_street_address>
  <billing_city>Billing City</billing_city>
  <billing_state>Billing State</billing_state>
  <billing_zip>Billing ZIP Code</billing_zip>
  <billing_country>Billing Country</billing_country>
  <telephone_fax>Billing Address Fax Number</telephone_fax>
  <web_address>Your Website</web_address>
  <purchase_order>Purchase Order</purchase_order>
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```

**Response:**

    Status: 200 OK


Destroy customer_account
---------------

* `DELETE /customer_accounts/#{id}.xml` destroys the customer_account at the referenced URL.

**Response:**

    Status: 200 OK