# Cordova Zeroconf Example App

Barebones Wifi zeroconf/mdns scanning demo application using [cordova-plugin-zeroconf](https://github.com/becvert/cordova-plugin-zeroconf).

# Usage

```sh
git clone https://github.com/emcniece/ZeroconfDemo.git
cd ZeroconfDemo

npm install

cordova platform add android
cordova build android
cordova emulate android
cordova run android
```

Once running, open the browser devtools to see console logs of discovered services.

This project only modifies one file after running `cordova create`: [www/js/index.js](/www/js/index.js).

When using the Zeroconf plugin, ensure your calls are performed _after_ the `onReady` call runs:

```js
onDeviceReady: function() {
    this.receivedEvent('deviceready');

    var zeroconf = window.cordova.plugins.zeroconf;

    window.cordova.plugins.zeroconf.watch('_http._tcp.', 'local.', function(result) {
        var action = result.action;
        var service = result.service;
        if (action == 'added') {
            console.log('service added', service);
        } else if (action == 'resolved') {
            console.log('service resolved', service);
        } else {
            console.log('service removed', service);
        }
    });
},
```