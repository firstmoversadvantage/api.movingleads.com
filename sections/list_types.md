ListTypes
=====

Get list_types
-----------

* `GET /api/v1/list_types` returns a list of all list types. 

**XML Response:**

``` xml
<list-types type="array">
  <list-type>
    <idtype="integer">1</id>
    <description>Pre-Movers List</description>
  </list-type>
  <list-type>
    <idtype="integer">3</id>
    <description>Pre-Movers Turnkey Postcards</description>
  </list-type>
  <list-type>
    <idtype="integer">11</id>
    <description>Pre-Movers Telemarketing</description>
  </list-type>
  <list-type>
    <idtype="integer">17</id>
    <description>Postcards</description>
  </list-type>
  <list-type>
    <idtype="integer">26</id>
    <description>Clairvoyance</description>
  </list-type>
  <list-type>
    <idtype="integer">28</id>
    <description>Clairvoyance Postcards</description>
  </list-type>
</list-types>
```


**JSON Response:**

``` json
{"list_types":
  [
    {"list_type":
      {"id":1,"description":"Pre-Movers List"}
    },
    {"list_type":
      {"id":3,"description":"Pre-Movers Turnkey Postcards"}
    },
    {"list_type":
      {"id":11,"description":"Pre-Movers Telemarketing"}
    },
    {"list_type":
      {"id":17,"description":"Postcards"}
    },
    {"list_type":
      {"id":26,"description":"Clairvoyance"}
    },
    {"list_type":
      {"id":28,"description":"Clairvoyance Postcards"}
    }
  ]
}
```


Get list_type
-----------

* `GET /api/v1/list_types/:id` returns information on the list type with the specified ID


**XML Response:**

``` xml
<list-type>
  <idtype="integer">1</id>
  <description>Pre-Movers List</description>
</list-type>
```

**JSON Response:**

``` json
{"list_type":
  {"id":1,"description":"Pre-Movers List"}
}
```