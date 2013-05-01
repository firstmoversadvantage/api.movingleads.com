<!-- 
    customer_account_list_order_watch_lists GET    
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists(.:format)  watch_lists#index
                                            POST   
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists(.:format)  watch_lists#create
 new_customer_account_list_order_watch_list GET    
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/new(.:format)  watch_lists#new
edit_customer_account_list_order_watch_list GET    
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/:id/edit(.:format) watch_lists#edit
     customer_account_list_order_watch_list GET    
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/:id(.:format)  watch_lists#show
                                            PUT    
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/:id(.:format)  watch_lists#update
                                            DELETE 
            /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/:id(.:format)  watch_lists#destroy
 -->
WatchList
================

For the full XML representation of watch_lists, [check out the data reference](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/data_reference.md#watch_list).

The account API is currently just for reading, not writing. Any authenticated user has access.


Get watch_list
-----------

* `GET /watch_list.xml` returns info about the current user’s customer account.

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


Get watch_lists
-------------

* `GET /watch_lists.xml` returns a collection of watch_lists that are visible to the authenticated user.
* `GET /watch_lists.xml?n=#{offset}` returns a collection of watch_lists offset by the given amount.
* `GET /watch_lists.xml?tag_id=#{tag_id}` returns a collection of watch_lists that have a specific tag.
* `GET /watch_lists.xml?since=20070425154546` returns a collection of watch_lists that have been created or updated since the time passed in through the URL. 
The list is paginated using offsets. If 500 elements are returned (the page limit), use `?n=500` to check for the next 500 and so on.

When filtering with the `since` parameter, the collection is ordered by ascending `updated_at` (oldest to newest). The `since` parameter should be in the `yyyymmddhhmmss` format and in UTC.

If watch_lists under a tag are requsted and no watch_lists with that tag exist, an empty `<watch_lists>` container will be returned.

**Response:**

``` xml
<watch_lists>
  <watch_list>
    ...
  </watch_list>
  <watch_list>
    ...
  </watch_list>
</watch_lists>
```


Create watch_list
--------------

* `POST /watch_lists.xml` creates a new watch_list with the currently authenticated user as the author.

The XML for the new watch_list is returned on a successful request with the timestamps recorded and ids for the contact data associated.

By default, a new watch_list is assumed to be visible to `Everyone`. You can also chose to make the watch_list only visible to the creator using `Owner` as the value for the `visible-to` tag. Or `NamedGroup` and pass in a `group-id` tag too.

As always, the URL for the newly-created watch_list is passed back in the `Location` header.

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
    Location: https://example.firstmoversadvantage.com/watch_lists/#{new-watch_list-id}.xml

    <watch_list>
      ...
    </watch_list>


Update watch_list
--------------

* `PUT /watch_lists/#{id}.xml` updates an existing watch_list with new details from the submitted XML.

Contact data and Subject data that include an id will be updated, data that doesn’t will be assumed to be new and created from scratch. To remove a piece of data, prefix its id with a minus sign (e.g. `-1`).

Use `?reload=true` to get XML of the successfully updated watch_list.

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


Destroy watch_list
---------------

* `DELETE /watch_lists/#{id}.xml` destroys the watch_list at the referenced URL.

**Response:**

    Status: 200 OK