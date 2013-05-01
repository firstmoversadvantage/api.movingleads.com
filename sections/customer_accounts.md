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


Get customer_account
-----------

* `GET /customer_account.xml` returns info about the current user’s customer account.

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


Get customer_accounts
-------------

* `GET /customer_accounts.xml` returns a collection of customer_accounts that are visible to the authenticated user.
* `GET /customer_accounts.xml?n=#{offset}` returns a collection of customer_accounts offset by the given amount.
* `GET /customer_accounts.xml?tag_id=#{tag_id}` returns a collection of customer_accounts that have a specific tag.
* `GET /customer_accounts.xml?since=20070425154546` returns a collection of customer_accounts that have been created or updated since the time passed in through the URL. 
The list is paginated using offsets. If 500 elements are returned (the page limit), use `?n=500` to check for the next 500 and so on.

When filtering with the `since` parameter, the collection is ordered by ascending `updated_at` (oldest to newest). The `since` parameter should be in the `yyyymmddhhmmss` format and in UTC.

If customer_accounts under a tag are requsted and no customer_accounts with that tag exist, an empty `<customer_accounts>` container will be returned.

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

By default, a new customer_account is assumed to be visible to `Everyone`. You can also chose to make the customer_account only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

As always, the URL for the newly-created customer_account is passed back in the `Location` header.

**Request:**

``` xml
<account>
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

**Response:**

    Status: 201 Created
    Location: https://example.firstmoversadvantage.com/customer_accounts/#{new-customer_account-id}.xml

    <customer_account>
      ...
    </customer_account>


Update customer_account
--------------

* `PUT /customer_accounts/#{id}.xml` updates an existing customer_account with new details from the submitted XML.

Contact data and Subject data that include an id will be updated, data that doesn’t will be assumed to be new and created from scratch. To remove a piece of data, prefix its id with a minus sign (e.g. `-1`).

Use `?reload=true` to get XML of the successfully updated customer_account.

**Request:**

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

**Response:**

    Status: 200 OK


Destroy customer_account
---------------

* `DELETE /customer_accounts/#{id}.xml` destroys the customer_account at the referenced URL.

**Response:**

    Status: 200 OK