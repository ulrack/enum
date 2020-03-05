[![Build Status](https://travis-ci.com/ulrack/enum.svg?branch=master)](https://travis-ci.com/ulrack/enum)

# Ulrack Enum

Ulrack Enum is an implementation of enumerable objects for PHP.
It uses two interpreter hooks to allow type-hinting and simply retrieving the value.

## Installation

To install the package run the following command:

```
composer require ulrack/enum
```

## Usage

In order to create an enumerable, create a new class which extends `Ulrack\Enum\Enum`.
Then add all the options as constants in the newly created class.
Optionally it is possible to define the callable methods in a doc-block above the class definition.

An implementation of the enumerable would look like the following:
```php
<?php
/**
 * Copyright (C) GrizzIT, Inc. All rights reserved.
 * See LICENSE for license details.
 */

namespace MyProject\MyPackage\Common;

use Ulrack\Enum\Enum;

/**
 * @method static EnumMock FOO()
 * @method static EnumMock BAR()
 */
class MyEnum extends Enum
{
    const FOO = 'foo';
    const BAR = 'bar';
}
```

The desired enumerable value can then be retrieved by calling `MyProject\MyPackage\Common\MyEnum::FOO()`.
This will retrieve an instance of `MyProject\MyPackage\Common\MyEnum` with a set value of `foo`.
The value `foo` can be retrieved by casting the object to a string.

An implementation of this in action would look like the following:
```php
<?php
/**
 * Copyright (C) GrizzIT, Inc. All rights reserved.
 * See LICENSE for license details.
 */

namespace MyProject\MyPackage\Namespace;

use MyProject\MyPackage\Common\MyEnum;

class MyImplementation
{
    /**
     * Constructor
     *
     * @param MyEnum $option
     */
    public function __construct(MyEnum $option)
    {
        $this->option = (string) $option;
    }
}

new MyImplementation(MyEnum::FOO());
```

The `MyProject\MyPackage\Common\MyEnum` class also inherits some functionality from the `Ulrack\Enum\Enum` class.
For example to retrieve all options, the static method `getOptions` can be called on `MyEnum`.
This would retrieve an associative array of the options.

It is also possible to retrieve the enumerable name by supplying the value to a different function.
This can be done by calling `MyEnum::getOrdinal('foo')` which would yield `FOO`.

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CODE_OF_CONDUCT](CODE_OF_CONDUCT.md) for details.

## MIT License

Copyright (c) 2019 GrizzIT

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
