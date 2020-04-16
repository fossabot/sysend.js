[![npm](https://img.shields.io/badge/npm-1.3.3-blue.svg)](https://www.npmjs.com/package/sysend)
![bower](https://img.shields.io/badge/bower-1.3.3-yellow.svg)
![downloads](https://img.shields.io/npm/dt/sysend.svg)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjcubic%2Fsysend.js.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjcubic%2Fsysend.js?ref=badge_shield)

## sysend.js

sysend.js is small library that allow to send message between pages that are
open in the same browser. It also support Cross-Domain comunication. The library doesn't have
any dependencies and uses the HTML5 LocalStorage API or BroadcastChannel API.
If your browser don't support BroadcastChannel (see [Can I Use](https://caniuse.com/#feat=broadcastchannel))
then you can send any object that can be serialized to JSON with BroadcastChannel you can send any object
(it will not be serialized to string but the values are limited to the ones that can be copied by
the [structured cloning algorithm](https://html.spec.whatwg.org/multipage/structured-data.html#structured-clone)).
You can also send empty notification.


Tested on:

GNU/Linux: in Chromium 34, FireFox 29, Opera 12.16 (64bit)<br/>
Windows 10 64bit: in IE11 and Edge 38, Chrome 56, Firefox 51<br/>
MacOS X El Captain: Safari 9, Chrome 56, Firefox 51

## Instalation

Include `sysend.js` file in your html, you can grab the file from npm:

```
npm install sysend
```

or bower


```
bower install sysend
```

you can also get it from unpkg.com CDN:

```
https://unpkg.com/sysend
```


## Usage

```javascript

window.onload = function() {
    sysend.on('foo', function(message) {
        console.log(message);
    });
    var input = document.getElementsByTagName('input')[0];
    document.getElementsByTagName('button')[0].onclick = function() {
        sysend.broadcast('foo', {message: input.value});
    };
};
```

If you want to add support for Cross-Domain communication you need to call proxy method with url on target domain
that have [proxy.html file](https://github.com/jcubic/sysend.js/blob/master/proxy.html).

```javascript
sysend.proxy('https://jcubic.pl');
sysend.proxy('https://terminal.jcubic.pl');
```

on Firefox you need to add **CORS** for the proxy.html that will be loaded into iframe (see [Cross-Domain LocalStorage](https://jcubic.wordpress.com/2014/06/20/cross-domain-localstorage/))

## Demo

Open this [demo page](http://jcubic.pl/sysend.php) in two tabs/windows.

## API

sysend object:

* on(name, callback) - callback(object, name) - add event of specified name
* off(name [, callback]) - remove callback
* broadcast(name [, object]) - send object and fire all events with specified name (in different pages that register callback using on). You can also just send notification without object
* proxy(url) - create iframe proxy for different domain, the targer domain/url should have [proxy.html](https://github.com/jcubic/sysend.js/blob/master/proxy.html) file. If url domain is the same as page domain, it's ignored. So you can put both proxy calls on both domains (new in 1.3.0)

## License

Copyright (C) 2014-2018 [Jakub T. Jankiewicz](http://jcubic.pl)<br/>
Released under the [MIT license](https://opensource.org/licenses/MIT)

This is free software; you are free to change and redistribute it.<br/>
There is NO WARRANTY, to the extent permitted by law.


[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fjcubic%2Fsysend.js.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fjcubic%2Fsysend.js?ref=badge_large)