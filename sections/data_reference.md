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