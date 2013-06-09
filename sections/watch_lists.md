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

Get watch_list
-----------

* `GET /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/#{watch_list-id}.xml` returns info about the specified watchlist.

This endpoint includes:

* watchlist ID
* list order id
* full name
* street address
* city
* state
* 9-digit zip code
* dpbc
* unit type
* unit number
* your account
* filter before
* sold on date
* timestamps (created_at, updated_at)


**Response:**

``` xml
<watch_list>
  <id>1</id>
  <list_order_id>5</list_order_id>
  <full_name> John Doe</full_name>
  <street_address> 123 Example St.</street_address>
  <city> Exampleville</city>
  <state>CO</state>
  <zip_9> 80303-4444</zip_9>
  <dpbc>DPBC</dpbc>
  <unit_type> unit type</unit_type>
  <unit_number> unit number</unit_number>
  <your_account> account</your_account>
  <filter_before> filter before</filter_before>
  <sold_on> sold on date</sold_on>
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</watch_list>
```

Get watch_lists
-------------

* `GET /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists.xml` returns a collection of watch_lists that are visible to the authenticated user.

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

* `POST /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists.xml` creates a new watch_list with the currently authenticated user as the author.

The XML for the new watch_list is returned on a successful request with the timestamps recorded and ids for the contact data associated.

As always, the URL for the newly-created watch_list is passed back in the `Location` header.

**Request:**

``` xml
<watch_list>
  <list_order_id>5</list_order_id>
  <full_name> John Doe</full_name>
  <street_address> 123 Example St.</street_address>
  <city> Exampleville</city>
  <state>CO</state>
  <zip_9> 80303-4444</zip_9>
  <dpbc>DPBC</dpbc>
  <unit_type> unit type</unit_type>
  <unit_number> unit number</unit_number>
  <your_account> account</your_account>
  <filter_before> filter before</filter_before>
  <sold_on> sold on date</sold_on>
</watch_list>
```

**Response:**

    Status: 201 Created
    Location: https://example.firstmoversadvantage.com/customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/#{new-watch_list-id}.xml

    <watch_list>
      ...
    </watch_list>


Update watch_list
--------------

* `PUT /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/#{watch_list-id}.xml` updates an existing watch_list with new details from the submitted XML.

Use `?reload=true` to get XML of the successfully updated watch_list.

**Request:**

``` xml
<watch_list>
  <id>1</id>
  <list_order_id>5</list_order_id>
  <full_name> John Doe</full_name>
  <street_address> 123 Example St.</street_address>
  <city> Exampleville</city>
  <state>CO</state>
  <zip_9> 80303-4444</zip_9>
  <dpbc>DPBC</dpbc>
  <unit_type> unit type</unit_type>
  <unit_number> unit number</unit_number>
  <your_account> account</your_account>
  <filter_before> filter before</filter_before>
  <sold_on> sold on date</sold_on>
</watch_list>
```

**Response:**

    Status: 200 OK


Destroy watch_list
---------------

* `DELETE /customer_accounts/:customer_account_id/list_orders/:list_order_id/watch_lists/#{watch_list-id}.xml` destroys the watch_list at the referenced URL.

**Response:**

    Status: 200 OK