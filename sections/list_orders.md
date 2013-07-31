ListOrders
==========

<!-- 
    customer_account_list_orders GET    /customer_accounts/:customer_account_id/list_orders(.:format)         list_orders#index
                                 POST   /customer_accounts/:customer_account_id/list_orders(.:format)        list_orders#create
 new_customer_account_list_order GET    /customer_accounts/:customer_account_id/list_orders/new(.:format)     list_orders#new
edit_customer_account_list_order GET    /customer_accounts/:customer_account_id/list_orders/:id/edit(.:format)list_orders#edit
     customer_account_list_order GET    /customer_accounts/:customer_account_id/list_orders/:id(.:format)     list_orders#show
                                 PUT    /customer_accounts/:customer_account_id/list_orders/:id(.:format)    list_orders#update
                                 DELETE /customer_accounts/:customer_account_id/list_orders/:id(.:format)   list_orders#destroy


              shared_list_orders GET    /shared_list_orders(.:format)          shared_list_orders#index
                                 POST   /shared_list_orders(.:format)          shared_list_orders#create
           new_shared_list_order GET    /shared_list_orders/new(.:format)      shared_list_orders#new
          edit_shared_list_order GET    /shared_list_orders/:id/edit(.:format) shared_list_orders#edit
               shared_list_order GET    /shared_list_orders/:id(.:format)      shared_list_orders#show
                                 PUT    /shared_list_orders/:id(.:format)      shared_list_orders#update
                                 DELETE /shared_list_orders/:id(.:format)      shared_list_orders#destroy -->


Get list_order
-----------

* `GET /api/v1/customer_accounts/#{customer_account_id}/list_orders/#{id}` returns information about the specified list order belonging to the specified customer account.

This endpoint includes:

* created_by_user_id
* customer_account_id
* delivery_email_addresses, 
* delivery_email_subject
* geo_city, geo_state, geo_country, geo_latitude, geo_longitude, geo_radius_miles
* geo_street_address, geo_zip
* id
* is_active
* max_price
* min_price
* order_by
* record_limit
* list_type_id (1 = Pre-Mover Mailing List, 3 = Pre-Mover Turnkey Marketing, 28 = Clairvoyance Retention with Postcards)


**Response:**

``` xml
<list_order>
  <created_by_user_id>User</created_by_user_id>	
  <customer_account_id type="integer">1</created_by_user_id>	
  <delivery_email_addresses>John@gmail.com</delivery_email_addresses>
  <delivery_email_subject>Subject</delivery_email_subject>
  <geo_city>Your City</geo_city>
  <geo_state>Your State</geo_state>
  <geo_country>Your Country</geo_country>
  <geo_latitude>Your Latitude</geo_latitude>
  <geo_longitude>Your Longitude</geo_longitude>
  <geo_radius_miles>Your Miles</geo_radius_miles>
  <geo_street_address>Your Street Address</geo_street_address>
  <geo_zip>Your Zip</geo_zip>	
  <id type="integer">1</id>
  <is_active>Y/N</is_active>
  <max_price>Max Price</max_price>
  <min_price>Min Price</min_price>
  <order_by>Order By</order_by>
  <record_limit>Record Limit</record_limit>
</list_order>
```


Get list_orders
-------------

* `GET /api/v1/customer_accounts/#{customer_account-id}/list_orders.xml` returns a collection of list_orders that are associated with specified customer account.

**Response:**

``` xml
<list_orders>
  <list_order>
    ...
  <list_order>
  <list_order>
    ...
  </list_order>
</list_orders>
```


Create list_order
--------------

* `POST /api/v1/customer_accounts/#{customer_account-id}/list_orders.xml` creates a new list_order for the specified customer account with the details from the submitted XML.
								

**Request:**

``` xml
<list_order>
  <created_by_user_id>User</created_by_user_id>	
  <customer_account_id type="integer">1</created_by_user_id>	
  <delivery_email_addresses>John@gmail.com</delivery_email_addresses>
  <delivery_email_subject>Subject</delivery_email_subject>
  <geo_city>Your City</geo_city>
  <geo_state>Your State</geo_state>
  <geo_country>Your Country</geo_country>
  <geo_latitude>Your Latitude</geo_latitude>
  <geo_longitude>Your Longitude</geo_longitude>
  <geo_radius_miles>Your Miles</geo_radius_miles>
  <geo_street_address>Your Street Address</geo_street_address>
  <geo_zip>Your Zip</geo_zip>	
  <id type="integer">1</id>
  <is_active>Y/N</is_active>
  <max_price>Max Price</max_price>
  <min_price>Min Price</min_price>
  <order_by>Order By</order_by>
  <record_limit>Record Limit</record_limit>
</list_order>
```

**Response:**

Status: 201 Created
Location: https://example.firstmoversadvantage.com/customer_accounts/#{customer_account-id}/list_orders.xml

	<list_order>
	  ...
	</list_order>


Update list_order
--------------

* `PUT /api/v1/customer_accounts/#{customer_account-id}/list_orders/#{id}.xml` updates an existing list_order with new details from the submitted XML.


**Request:**

``` xml
<list_order>
  <created_by_user_id>User</created_by_user_id>	
  <customer_account_id type="integer">1</created_by_user_id>	
  <delivery_email_addresses>John@gmail.com</delivery_email_addresses>
  <delivery_email_subject>Subject</delivery_email_subject>
  <geo_city>Your City</geo_city>
  <geo_state>Your State</geo_state>
  <geo_country>Your Country</geo_country>
  <geo_latitude>Your Latitude</geo_latitude>
  <geo_longitude>Your Longitude</geo_longitude>
  <geo_radius_miles>Your Miles</geo_radius_miles>
  <geo_street_address>Your Street Address</geo_street_address>
  <geo_zip>Your Zip</geo_zip>	
  <id type="integer">1</id>
  <is_active>Y/N</is_active>
  <max_price>Max Price</max_price>
  <min_price>Min Price</min_price>
  <order_by>Order By</order_by>
  <record_limit>Record Limit</record_limit>
</list_order>
```


**Response:**

    Status: 200 OK


Destroy list_order
---------------

* `DELETE /api/v1/customer_accounts/#{customer_account-id}/list_orders/#{id}.xml` destroys the list_orders at the referenced URL.

**Response:**

    Status: 200 OK
