Data Reference
==============

All timestamps communicated from (and to) MovingLeads are in the `UTC` timezone.

User
----

``` xml
<user>
  <id type="integer">1</id>
  <first_name>John</first_name>
  <last_name>Doe</last_name>
  <organization>User Corporation</organization>
  <email>john.doe@example.com</email>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>

  <!-- when requested as /me.xml -->
  <token>#{api_token}</token>
  <dropbox>#{dropbox_email_address}</dropbox>
</user>
```

CustomerAccount
---------------

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
  <brand_affiliation>Your Brand Affiliation</brand_affiliation>
  <user_agreement_signed_on> Date You Signed User Agreement</user_agreement_signed_on>
  <credit_balance>Your Credit Balance</credit_balance>
  <credit_limit>Your Credit Limit</credit_limit>
  <credit_hold> True If On Credit Hold</credit_hold>
  <credit_card_vault_id>Your Vault ID For Authorize.net</credit_card_vault_id>
  <credit_card_last_four_digits>Last Four Digits of Credit Card Number</credit_card_last_four_digits>
  <credit_card_expires_on>Your Credit Card Expiration Date</credit_card_expires_on>
  <peachtree_id>Your ID for Peachtree Accounting System</peachtree_id>
  <sales_representative_id>Your Peachtree Accounting Sales Rep ID</sales_representative_id>
  <shipping_method_id>Peachtree Shipping Method</shipping_method_id>
  <general_ledger_account_id>Your G/L Account ID for Peachtree Accounting</general_ledger_account_id>
  <billing_first_name>John</billing_first_name>
  <billing_last_name>Doe</billing_last_name>
  <billing_street_address>Billing Street Address</billing_street_address>
  <billing_city>Billing City</billing_city>
  <billing_state>Billing State</billing_state>
  <billing_zip>Billing ZIP Code</billing_zip>
  <billing_country>Billing Country</billing_country>
  <telephone_fax>Billing Address Fax Number</telephone_fax>
  <uses_standard_terms> True If You Use Standard Terms and Peachtree Accounting</uses_standard_terms>
  <web_address>Your Website</web_address>
  <authorize_customer_profile_id>Your Authorize.net Profile ID</authorize_customer_profile_id>
  <authorize_payment_profile_id>Your Authorize.net Payment ID</authorize_payment_profile_id>
  <credit_card_type>Your Credit Card Type</credit_card_type>
  <purchase_order>Purchase Order</purchase_order>
  <!-- <deactivated_on></deactivated_on> -->
  
  <created-at type="datetime">2007-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2007-01-12T15:00:00Z</updated-at>
</account>
```
