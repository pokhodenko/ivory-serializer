# Accessor

The accessor allows you to configure how to get a property.

## Example

In this example, we configure the username property to use the getUsername method when serializing.

``` php
namespace Acme;

use Ivory\Serializer\Mapping\Annotation as Serializer;

class User
{
    /**
     * @Serializer\Accessor("getUsername")
     *
     * @var string
     */
    public $username;
    
    /**
     * @return string
     */
    public function getUsername()
    {
        return strtolower($this->username);
    }
}
```

## Usage

``` php
use Acme\User;

$user = new User();
$user->username = 'GeLo';

$serialize = $serializer->serialize($user, $format);
// echo $serialize;

$deserialize = $serializer->deserialize($serialize, User::class, $format);
// $deserialize->username === 'gelo'
```

## Results

### JSON

``` json
{
    "username": "gelo"
}
```

### XML

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<result>
    <username>gelo</username>
</result>
```

### YAML

``` yaml
username: gelo
```

### CSV

``` csv
username
gelo
```

## Definitions

If you prefer use an other definition format, the following examples are identical. 

### XML

``` xml
<?xml version="1.0" encoding="UTF-8" ?>

<serializer
    xmlns="http://egeloen.fr/schema/ivory-serializer"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://egeloen.fr/schema/ivory-serializer
                        http://egeloen.fr/schema/ivory-serializer/mapping-1.0.xsd"
>
    <class name="Acme\User">
        <property name="username" accessor="getUsername" />
    </class>
</serializer>
```

### YAML

``` yaml
Acme\User:
    properties:
        username:
            accessor: getUsername
```

### JSON

``` json
{
    "Acme\\User": {
        "properties": {
            "username": {
                "accessor": "getUsername"
            }
        }
    }
}
```
