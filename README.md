IP Subnet Calculator
=================

JavaScript class for calculating optimal subnet masks for non-standard IP ranges, e.g. 5.4.3.21 - 6.7.8.9

[View demo](http://franksrevenge.github.io/IPSubnetCalculator/)


What does it do?
----------------

* Calculates subnet masks for standard and non-standard IP ranges. For example, `10.0.0.5 - 10.0.0.23` will result in `10.0.0.5/32, 10.0.0.6/31, 10.0.0.8/29, 10.0.0.16/29`.

* Calculates CIDR prefixes from subnet masks, e.g. `10.0.0.5/255.255.128.0` will result in `10.0.0.0/17`.

* Calculates subnet masks from CIDR prefixes, e.g. `10.0.0.5/17` will result in `255.255.128.0`.


Support
-------

* Node.js
* RequireJS
* Direct browser use


Installation
------------

```sh
> bower install ip-subnet-calculator

> npm install ip-subnet-calculator
```


Node.js
-------

```javascript
var IpSubnetCalculator = require( 'ip-subnet-calculator' );

console.log( IpSubnetCalculator.calculate( '5.4.3.21', '6.7.8.9' ) );
```


RequireJS
---------

```javascript
require( [ 'ip-subnet-calculator' ],

function( IpSubnetCalculator )
{
   console.log( IpSubnetCalculator.calculate( '5.4.3.21', '6.7.8.9' ) ); 
} );
```


Direct browser use
------------------

```html
<script src='IpSubnetCalculator.js'></script>

<script>
    console.log( IpSubnetCalculator.calculate( '5.4.3.21', '6.7.8.9' ) );
</script>
```


API
---

### IpSubnetCalculator.calculate( ipStart, ipEnd ) ###

Calculates an optimal set of IP masks for the given IP address range.

*ipStart* (string) Lowest IP in the range to be calculated in string format (`123.123.123.123`)

*ipEnd* (string) Highest IP (inclusive) in the range to be calculated in string format (`123.123.123.12`)

The function returns `null` in case of an error. Otherwise, an array containing one or more subnet
masks is returned:

```javascript
var result = [
    {
        ipLow              : 2071689984,
        ipLowStr           : "123.123.123.0",
        ipHigh             : 2071690239,
        ipHighStr          : "123.123.123.255",
        prefixMask         : 4294967040,
        prefixMaskStr      : "255.255.255.0",
        prefixSize         : 24,
        invertedMask       : 255,
        invertedMaskStr    : "0.0.0.255",
        invertedMaskSize   : 8
    },
    
    ...
];
```

Each object in question contain the following properties:

| Property             | Use                                                            |
:----------------------|:---------------------------------------------------------------|
| ipLow                | Decimal representation of the lowest IP address in the range   |
| ipLowStr             | String representation of the lowest IP address in the range    |
| ipHigh               | Decimal representation of the highest IP address in the range  |
| ipHighStr            | String representation of the highest IP address in the range   |
| prefixMask           | Decimal representation of the prefix (subnet) mask             |
| prefixMaskStr        | String representation of the prefix (subnet) mask              |
| prefixSize           | Size of the prefix (subnet) mask in bits                       |
| invertedMask         | Decimal representation of the inverted prefix mask             |
| invertedMaskStr      | String representation of the inverted prefix mask              |
| invertedSize         | Size of the inverted prefix max in bits                        |


### IpSubnetCalculator.calculateSubnetMask( ip, prefixSize ) ###

Calculates a subnet mask from CIDR prefix.

*ip* (string) IP address in string format

*prefixSize* Number of relevant bits in the subnet mask

The function returns an object containing full description of the IP range, as described in `IpSubnetCalculator.calculate()`.


### IpSubnetCalculator.calculateCIDRPrefix( ip, subnetMask ) ###

Calculates a CIDR prefix from subnet mask.

*ip* (string) IP address in string format

*subnetMask* IP subnet mask in string format

The function returns an object containing full description of the IP range, as described in `IpSubnetCalculator.calculate()`.



License
-------

[Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)


