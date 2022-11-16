# php-reflection-deflector
 [![Latest Stable Version](https://poser.pugx.org/flarone/reflection/v/stable)](https://packagist.org/packages/flarone/reflection) [![Total Downloads](https://poser.pugx.org/flarone/reflection/downloads)](https://packagist.org/packages/flarone/reflection) [![Latest Unstable Version](https://poser.pugx.org/flarone/reflection/v/unstable)](https://packagist.org/packages/flarone/reflection) [![License](https://poser.pugx.org/flarone/reflection/license)](https://packagist.org/packages/flarone/reflection)
<br>
Test your **Private/Protected** Methods/Properties with any testing package and with **Zero** configuration.

**New:** Can reflect multiple classes at same time.

# Usage
### Step 1: Install Through Composer
```php
composer require flarone/reflection --dev
```

### Step 2: Import the trait
Import the `Flarone\Reflection\ReflectableTrait` in your `TestClass` of any package. Eg: `PhpUnit`, `PhpSpec`, `Laracasts\Integrated`.

For `PhpUnit`
```php
use Flarone\Reflection\ReflectableTrait

class ModelTest extends PHPUnit_Framework_TestCase
{
  use ReflectableTrait;
}
```

And That's it. You are all set to go. :)

**Now you can do the following to test private/protected methods or properties:**

### Instantiate the Reflector
By using `reflect()` method like this:
```php
$randomClass = new RandomClass();
$this->reflect($randomClass);
```
**This Method is not chainable**<br>
**Note:** Its preferable to use this in `constructor` or for PhpUnit in `setUp()` method etc.

By using `on()` method like this:
```php
$randomClass = new RandomClass();
$this->on($randomClass)->call($method, $args = []);
```
**This method is chainable**
**Note: **This method relfects the class object only once. That is only for one call to method or property. It can be used for relfecting multiple classes at same time.

# Available Methods
#### reflect($classObj);
**Description:** Reflect the Class Object
<br>
<br>
#### on($classObj);
**Description:** Reflect the Class Object. This is Chainable Method.<br>
Possible Chaining:
```php
$this->on($classObject)->callMethod($arguments = []);
$this->on($classObject)->call($method, $arguments = []);
$this->on($classObject)->get($property);
$this->on($classObject)->get{Proerty};
```
<br>
<br>
#### call($method, $arguments = []);
**Description:** Call any valid public/Private/Protected Method of reflected Class Object. This is not Chainable Method.
<br>
<br>
#### call{Method}($arguments = []);
**Description:** Same as `call()` but dynamically calls the method. This is not Chainable Method.<br>
{method} Can be any valid public/private/protected method of reflected Class Object.
<br>
<br>
#### get($property);
**Description:** Get the value of any valid Public/Private/Protected property of the reflected Class Object. This is not Chainable Method.
<br>
<br>
#### get{Property};
**Description:** Same as `get()` but dynamically gets the value of the property. This is not Chainable Method.<br>
{property} Can be any valid Public/Private/Protected property of the reflected Class Object.
<br>
<br>
#### set($name, $value);
**Description:** Set the value of valid Public/Private/Protected property of the reflected Class Object. This is not Chainable Method.
<br>
<br>
#### set{Property} = $value;
**Description:** Same as `set()` but dynamically sets the value of the property. This is not Chainable Method.<br>
{property} Can be any valid Public/Private/Protected property of the reflected Class Object.

-
### Reflect Multiple classes at same time
**Example:**
```php
// Considering phpunit

 protected function setUp()
  {
    $this->foo = new Foo();
    $this->reflect($this->foo);
  }
  

  public function test_something()
  {
    $hello = $this->callSayHello(); // this will call SayHello() of class `Foo`
    $this->assertEquals('Hello', $hello);

    $hello = $this->on(new FooBar())->callSayHello(); // this will call SayHello() of class `FooBar`
    $this->assertEquals('Hello FooBar', $hello);

    $hello = $this->callSayHello(); // this will call SayHello() of class `Foo`
    $this->assertEquals('Hello', $hello);
  }
```

# Contribution
Feel free to report issues or make Pull Requests.
If you find this document can be improved in any way, please feel free to open an issue for it.

# License
The php-reflection-deflector was forked from `skagarwal/reflection`.
The php-reflection-deflector is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
