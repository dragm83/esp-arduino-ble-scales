# Bluetooth scales library for ESP on Arduino Framework

This library defines3 main abstract concepts:
* A `RemoteScales`  which is used as a common interface to connect to scales, retrieve their weight and tare. It also supports a callback that is triggered when a new weight is received. 
* A `RemoteScalesScanner` which is used to scan for `RemoteScales` instances that are supported, and
* A `RemoteScalesPluginRegistry` which holds all the scales that are supported by the library. 

This allows for easy extention of the library for more bluetooth enabled scales. 

### Currently implemented scales

* [Acaia Lunar](https://acaia.co/collections/coffee-scales/products/lunar_2021) - [Tested]
* [Acaia Pearl](https://acaia.co/collections/coffee-scales/products/pearl) - [Tested]
* [Bookoo Themis](https://bookoocoffee.com/shop/bookoo-mini-scale/?coupon=gaggiuino) - [Tested]
* [Difluid microbalance](https://digitizefluid.com/products/microbalance) - [Tested]
* [Difluid microbalance Ti](https://digitizefluid.com/collections/m-series/products/microbalance-ti) - [Tested]
* [Eclair](https://makerworld.com/en/models/664430#profileId-591777) - [Tested]
* [Timemore Black Mirror DUO](https://www.timemore.com/collections/coffee-scale/products/timemore-coffee-scale-black-mirror-duo) - [Tested]

Want a specific model? Implement it 🚀 Read on to find out how... 

### How do implement new scales

We can do this either in this repo or in a separate repo. In both cases we need to:
1. Create a class for the new Scales (i.e. `AcaiaScales`) that implements the protocol of the scales and extends `RemoteScales`. This is 99.9% of the work as it involves reverse engineering or reading the datasheet of the scales and implementing it accordingly. 
2. Create a plugin (i.e. `AcaiaScalesPlugin`) that extends `RemoteScalesPlugin` and implement an `apply()` method which should register the plugin to the `RemoteScalesPluginRegistry` singleton.
3. Import your new library together with the `remote_scales` library and apply your plugin (i.e. `MyScalesPlugin::apply()`) during the initialisaion phase. 

