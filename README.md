Moving Leads by First Movers Advantage, LLC
===========================================
First Movers Advantage, LLC provides sales leads and customer retention services to the moving and storage industry in the USA. This API is intended for use by software providers in the industry to integrate customer acquisition and customer retention features into their software offerings.

Example Customer Story
======================
Anne works for a moving company and wishes to purchase a direct mail list for her customer acquisition campaign. She will start at [customers.movingleads.com](http://customers.movingleads.com) and create a new User account. Our system will send Anne an email asking her to confirm her email address and activate the User account.

After the User account is activated, Anne will create a CustomerAccount for billing purposes. If Anne has more that one location, she can create a separate CustomerAccount for each location. We will send one Invoice for each CustomerAccount, so Anne can keep track of expenses by location or cost center.

After creating each CustomerAccount, Anne will be asked to review and sign our UserAgreement. To sign the agreement, she will check a box to say 'I Agree' and press a submit button.

After signing the User Agreement, Anne can create one or more ListOrders for service (per CustomerAccount). Our system will automatically create one default ListOrder for our pre-movers mailing list. The new ListOrder is inactive by default and Anne will be prompted to call us to review her list selection criteria, provide credit card information, and begin service.

While Anne's service is active, we will send a weekly mailing list by email on Monday mornings. The email will include a PDF attachment that has been pre-formatted for mailing labels. She will also receive the same list in XLS format for use in a mail merge with a word processor.

Anne will also receive a weekly email with her invoice attached (one per CustomerAccount).

Please contact us at (303) 443-0767 with questions about our service.

Moving Leads API
================
The [Moving Leads](http://www.movingleads.com/) API is implemented as vanilla JSON or XML over HTTP using all four verbs (GET/POST/PUT/DELETE). Every resource, like User, CustomerAccount, or ListOrder, has their own URL and are manipulated in isolation. In other words, we've tried to make the API follow the REST principles as much as we can.

You can explore the view part of the API (everything that's fetched with GET) through a regular browser. Using Firefox for this is particularly nice as it has a good, simple XML renderer (unlike Safari which just strips the tags and dumps the content). The API is versioned where the version number is in the request path. For example: `/api/v1/customer_accounts.xml` for XML or `/api/v1/customer_accounts.json` for JSON.

API Endpoints
-------------
* [Users](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/users.md) represents a user of our system. Each user can create, and be associated with, multiple CustomerAccounts. The User model handles authentication for both the HTML and API interfaces.
* [CustomerAccounts](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/customer_accounts.md) are created for billing purposes and to manage related ListOrders. We will issue one invoice per CustomerAccount. If you want separate invoices for different cost centers, you can create a CustomerAccount for each cost center. A CustomerAccount can have multiple ListOrders.
* [ListOrders](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/list_orders.md) represents a standing order to purchase direct mail lists, turnkey postcard services, or customer retention services. A CustomerAccount can have as many list orders as the customer desires.
* [WatchLists](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/watch_lists.md) are used for our Clairvoyance customer retention services. The WatchList contains a list of customer-supplied names and addresses for customer retention monitoring. Each WatchList record is related to a specific ListOrder.

Authentication
--------------

When you're using the API, it's always through an existing User. There's no special API user. So when you use the API as "John Doe", you get to see and work with what "John Doe" is allowed to see and do. Authenticating is done with an authentication token, which you'll find on the User Profile screen in [customers.movingleads.com](http://customers.movingleads.com).

When using the authentication token, you don't need a separate password. But since Moving Leads uses [HTTP Basic Authentication](http://www.ietf.org/rfc/rfc2617.txt), and lots of implementations assume that you want to have a password, it's often easier just to pass in a dummy password, like X.

Here's an example using the authentication token and a dummy password through curl:

    curl -u 605b32dd:X https://customers.movingleads.com/api/v1/customer_accounts.xml

Remember that anyone who has your authentication token can see and change everything you have access to. So you want to guard that as well as you guard your username and password. If you come to fear that it has been compromised, you can regenerate it at any time from the User Profile screen in [customers.movingleads.com](http://customers.movingleads.com).

Reading through the API
-----------------------

The Moving Leads API has two category of actions for reading: Get one, or get many. All these actions are done through an HTTP GET, which also means that they're all easily explorable through a browser as described above.

Here's a few examples of reading with curl:

    curl -u 605b32dd:X https://customers.movingleads.com/api/v1/customer_accounts/4/list_orders/5.xml

    curl -u 605b32dd:X https://customers.movingleads.com/api/v1/customer_accounts/2/list_orders/3/watch_lists.xml

If the read is successful, you'll get an XML response back along with the status code `200 OK`.


Writing through the API
-----------------------

Creating, updating, and deleting resources through the API is almost as easy as reading, but you can't explore it as easily through the browser. Regardless of your implementation language, though, using curl to play first is a great idea. It makes it very easy to explore the API and is perfect for small scripts too.

When you're creating and updating resources, you'll be sending JSON or XML into Moving Leads. You need to let the system know that fact by adding the header `Content-type: application/xml` or `Content-type: application/json`, so we know that it's not regular form-encoded data coming in. Then you just include the XML or JSON of the resource in the body of your request.

Here's a few examples creating new resources, first with the XML inline, second referencing the XML from a file:

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d '<customer_account><company_name>Important matters</company_name></customer_account>' https://customers.movingleads.com/api/v1/customer_accounts/4.xml

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d @note.xml https://customers.movingleads.com/api/v1/customer_accounts/5/customer_accounts/2.xml

The response to a successful creation is the status code `201 Created`. You can get the URL of the new resource in the Location header (such that you know where to update your new resource in the future). We also include the complete XML for the final resource in the response. This is because you can usually get away with creating a new resource with less than all its regular attributes. Especially attributes like `created_at` can be helpful to get back from the creation.

Updating resources is done through the PUT verb and against the URL of the resource you want to update. Here's a few examples:

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d '<customer_account><company_name>Doe Company, LLC</company_name></customer_account>' https://customers.movingleads.com/api/v1/customer_accounts/4.xml

    curl -u 605b32dd:X -X PUT -H 'Content-Type: application/xml' \
    -d @note.xml https://customers.movingleads.com/api/v1/customer_accounts/2.xml

The response to a successful update is "200 OK".  Finally, you can delete resources (if you're allowed to) using the DELETE verb. A few examples of that:

    curl -u 605b32dd:X -X DELETE https://customers.movingleads.com/api/v1/customer_accounts/4.xml

    curl -u 605b32dd:X -X DELETE https://customers.movingleads.com/api/v1/customer_accounts/2.xml

NOTE: DELETE will be a no-op for most users. If you would like to deactivate an account, use the edit feature instead.

Note that you don't need to pass the content-type header because you're not sending any XML. The response to a successful DELETE is `200 OK`.

Dealing with failure
--------------------

If a request fails, the error information is returned with the HTTP status code. For instance, if a requested record could not be found, the HTTP response might look something like:

    HTTP/1.1 404 The record could not be found
    Date: Thu, 16 Mar 2006 17:41:40 GMT
    ...

Note that, in general, if a request causes a new record to be created (like a new message, or to-do item, etc.), the response will use the "201 Created" status. Any other successful operation (like a successful query, delete, or update) will use a 200 status code.

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

Please tell us how we can make this API better. If you have a specific feature request or if you found a bug, please contact us at (303) 443-0767.
