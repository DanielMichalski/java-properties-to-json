Java Properties to JSON
---------------------------------------------

How to generate JSON from Java properties?

You can generate Json from:
- from Java properties (java.util.Properties)
- from Map<String,String> (import java.util.Map)
- from InputStream with properties (java.io.InputStream)

below variable "properties" as one of the above types:

Simple Example
---------------------------------------------
code snippet:
```java

import pl.jalokim.propertiestojson.util.PropertiesToJsonParser;

...
String json = PropertiesToJsonParser.parseToJson(properties);

```

example properties:
```bash
object.man.name=John
object.man.surname=Doe
object.type=SOMETYPE
object.simpleNumber=1.2345
object2.simpleArray[0]=value1
object2.simpleArray[1]=value2
object2.simpleArray[2]=value3
object2.simpleArray[3]=value4
object2.objectArray[0].field1=value1
object2.objectArray[0].field2=value2
object2.objectArray[0].field3=value3
object3.arrayWithDelimeter=value1,value2,value3
object3.simpleString=stringValue
```

Will result:

```json
{
   "object2":{
      "simpleArray":[
         "value1",
         "value2",
         "value3",
         "value4"
      ],
      "objectArray":[
         {
            "field1":"value1",
            "field3":"value3",
            "field2":"value2"
         }
      ]
   },
   "object3":{
      "arrayWithDelimeter":[
         "value1",
         "value2",
         "value3"
      ],
      "simpleString":"stringValue"
   },
   "object":{
      "simpleNumber":1.2345,
      "man":{
         "surname":"Doe",
         "name":"John"
      },
      "type":"SOMETYPE"
   }
}
```
Example of use filters:
---------------------------------------------

code snippet:
```java

import pl.jalokim.propertiestojson.util.PropertiesToJsonParser;

...
String json = PropertiesToJsonParser.parseToJson(properties, "man.groups", "man.hoobies", "insurance.cost");
```

example properties:
```bash
man.groups[0].type=Commercial
man.groups[0].name=group1
man.groups[1].type=Free
man.groups[1].name=group2
man.groups[2].type=Commercial
man.groups[2].name=group3
man.hoobies[0]=cars
man.hoobies[1]=science
man.hoobies[2]=women
man.hoobies[3]=computers
man.insurance.cost=126.543
man.adress.street=Jp2
man.adress.city=Waraw
man.emails= example@gg.com ,example2@cc.com, example3@gg.com,example3@gg.com
man.name=John
man.surname=Surname
insurance.type=Medical
insurance.cost=123
field1=someValue2
field2=someValue3

```

Will result
```json
{
   "insurance":{
      "cost":123.0
   },
   "man":{
      "hoobies":[
         "cars",
         "science",
         "women",
         "computers"
      ],
      "groups":[
         {
            "name":"group1",
            "type":"Commercial"
         },
         {
            "name":"group2",
            "type":"Free"
         },
         {
            "name":"group3",
            "type":"Commercial"
         }
      ]
   }
}
```

Requirements
---------------------------------------------

- java 1.8

- properties structure must have structure compatible with json

For example properties from below will throws ParsePropertiesException!
```properties
object.man.name=John
object.man=simpleValue

## reason: in first key 'man' is consider as json object type and so on.

object.array[0]=simpleValue
object.array[1].someField=someObjectSomeFieldValue
object.array[1].someField2=someObjectSomeFieldValue2

## reason: in first key 'array' is consider as array for primitive type not for objects and so on.

```


Build from sources
---------------------------------------------

How to build from sources
```bash
mvn clean install
```