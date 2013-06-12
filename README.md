Moving Leads API
================

The Moving Leads API is implemented as vanilla XML over HTTP using all four verbs (GET/POST/PUT/DELETE). Every resource, like User, CustomerAccount, or ListOrder, has their own URL and are manipulated in isolation. In other words, we've tried to make the API follow the REST principles as much as we can.

You can explore the view part of the API (everything that's fetched with GET) through a regular browser. Using Firefox for this is particularly nice as it has a good, simple XML renderer (unlike Safari which just strips the tags and dumps the content). Pretty much any URL in Moving Leads can be viewed in its XML form by adding the .xml extension. So `/customer_accounts/4` becomes `/customer_accounts/4.xml` if you want to see the XML version.

API Endpoints
-------------
* [Users](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/users.md) represent a user of our system. Each user can be associated with multiple CustomerAccounts.
* [CustomerAccounts](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/customer_accounts.md) are created for billing purposes and to manage related ListOrders. We will issue one invoice per CustomerAccount. If you want separate invoice for different cost centers, you can create a CustomerAccount for each cost center. A CustomerAccount can have multiple ListOrders.
* [ListOrders](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/list_orders.md) represent a standing order to purchase leads, turnkey postcard services, or customer retention services.
* [WatchLists](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/watch_lists.md) are used for our Clairvoyance customer retention service. The WatchList contains a list of customer-supplied names and addresses for customer retention monitoring. Each WatchList record is related to a specific ListOrder.

Authentication
--------------

When you're using the API, it's always through an existing user in Moving Leads. There's no special API user. So when you use the API as "john doe", you get to see and work with what "john doe" is allowed to. Authenticating is done with an authentication token, which you'll find on the "My Info" screen in Moving Leads (click the "Reveal authentication token for feeds/API" link).

When using the authentication token, you don't need a separate password. But since Moving Leads uses [HTTP Basic Authentication](http://www.ietf.org/rfc/rfc2617.txt), and lots of implementations assume that you want to have a password, it's often easier just to pass in a dummy password, like X.

Here's an example using the authentication token and a dummy password through curl:

    curl -u 605b32dd:X https://customers.movingleads.com/customer_accounts/1.xml

Remember that anyone who has your authentication token can see and change everything you have access to. So you want to guard that as well as you guard your username and password. If you come to fear that it has been compromised, you can regenerate it at any time from the "My Info" screen in Moving Leads.

Note that the `/me.xml` endpoint is the one exception to token authentication: you can use a username and password to authenticate against this action. This allows developers to obtain the token for a user, given that user's username and password, which makes it easier for users to authenticate on mobile platforms and the like.


Reading through the API
-----------------------

The Moving Leads API has two category of actions for reading: Get one, or get many. All these actions are done through an HTTP GET, which also means that they're all easily explorable through a browser as described above.

Here's a few examples of reading with curl:

    curl -u 605b32dd:X https://customers.movingleads.com/customer_accounts/4/list_orders/5.xml

    curl -u 605b32dd:X https://customers.movingleads.com/customer_accounts/27/customer_accounts/2/list_orders/3/watch_lists.xml

If the read is successful, you'll get an XML response back along with the status code `200 OK`.


Writing through the API
-----------------------

Creating, updating, and deleting resources through the API is almost as easy as reading, but you can't explore it as easily through the browser. Regardless of your implementation language, though, using curl to play first is a great idea. It makes it very easy to explore the API and is perfect for small scripts too.

When you're creating and updating resources, you'll be sending XML into Moving Leads. You need to let the system know that fact by adding the header `Content-type: application/xml`, so we know that it's not regular form-encoded data coming in. Then you just include the XML of the resource in the body of your request.

Here's a few examples creating new resources, first with the XML inline, second referencing the XML from a file:

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d '<kase><name>Important matters</name></kase>' https://customers.movingleads.com/customer_accounts/4/list_orders.xml

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d @note.xml https://customers.movingleads.com/customer_accounts/5/customer_accounts/2/list_orders/3/watch_lists.xml

The response to a succesful creation is the status code `201 Created`. You can get the URL of the new resource in the Location header (such that you know where to update your new resource in the future). We also include the complete XML for the final resource in the response. This is because you can usually get away with creating a new resource with less than all its regular attributes. Especially attributes like `created_at` can be helpful to get back from the creation.

Updating resources is done through the PUT verb and against the URL of the resource you want to update. Here's a few examples:

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d '<kase><name>Really important matters</name></kase>' https://customers.movingleads.com/customer_accounts/4/list_orders/5.xml

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d @note.xml https://customers.movingleads.com/customer_accounts/2/list_orders/3/watch_lists/27.xml

The response to a successful update is "200 OK".  Finally, you can delete resources (if you're allowed to) using the DELETE verb. A few examples of that:

    curl -u 605b32dd:X -X DELETE https://customers.movingleads.com/customer_accounts/4/list_orders/5.xml

    curl -u 605b32dd:X -X DELETE https://customers.movingleads.com/customer_accounts/2/list_orders/3/watch_lists/27.xml

Note that you don't need to pass the content-type header because you're not sending any XML. The response to a successful delete is `200 OK`.


Dealing with failure
--------------------

If a request fails, the error information is returned with the HTTP status code. For instance, if a requested record could not be found, the HTTP response might look something like:

    HTTP/1.1 404 The record could not be found
    Date: Thu, 16 Mar 2006 17:41:40 GMT
    ...

Note that, in general, if a request causes a new record to be created (like a new message, or to-do item, etc.), the response will use the "201 Created" status. Any other successful operation (like a successful query, delete, or update) will use a 200 status code.


SSL Usage
---------

A non-SSL request made against an account that has SSL enabled (and vice versa) will receive a "302 Found" response. The Location header will contain the correct URI.

If SSL is enabled for your account, ensure that you're using https. If it's not, ensure you're using http.


Alternative formats
-------------------

We support XML and JSON formats. Replace '.xml' with '.json' if you would like JSON responses.


Conventions in the API documentation
------------------------------------

In the documentation that follows, the following notation is used:

    #{text}: Indicates text that should be replaced by your own data

    ...: Indicates content from the response has been elided for brevity in documentation. See the list of data responses at the end of the page for a full description of the format of that response type.


Help us make it better
----------------------

Please tell us how we can make this API better. If you have a specific feature request or if you found a bug, please contact us at (303) 43-0767.
