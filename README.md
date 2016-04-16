JsCheatsheet
=================
2016-03-26



Some js code that I use more often than not.




Extend
-----------

```js
function extend(){
    for(var i=1; i<arguments.length; i++)
        for(var key in arguments[i])
            if(arguments[i].hasOwnProperty(key))
                arguments[0][key] = arguments[i][key];
    return arguments[0];
}
```

http://stackoverflow.com/questions/11197247/javascript-equivalent-of-jquerys-extend-method





JsDispatcher
---------------

https://github.com/lingtalfi/jsdispatchers




js plugins
---------------

```js
window.myObject = function (options) {
    this.d = $.extend({
        plugins: [],
    }, options);
};
window.myObject.prototype = {
    _call: function (method, ...args) {
        for (var i in this.d.plugins) {
            if (method in this.d.plugins[i]) {
                this.d.plugins[i][method](...args);
            }
        }
    },
};
```




Random number between
------------

```js
function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

http://stackoverflow.com/questions/1527803/generating-random-numbers-in-javascript-in-a-specific-range




Is available pattern
---------------------

```js

var isAvailable = true;
var minDelay = 200;

jTarget.on('mousewheel DOMMouseScroll', function (e) {


    clearTimeout(currentTimeout);
    currentTimeout = setTimeout(function () {
        isAvailable = true;
    }, minDelay);
    
    console.log(isAvailable);
    
    isAvailable = false;

});
```

https://github.com/lingtalfi/Lys, waterball sensor



History Log
------------------

- 1.1.0 -- 2016-04-16

    - add js plugins section

- 1.0.0 -- 2016-03-31

    - initial commit
    
