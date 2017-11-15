JsCheatsheet
=================
2016-03-26



Some js code that I use more often than not.



getUriParams
----------------

```js
function getUriParams() {

    // http://locutus.io/php/strings/parse_str/
    function parse_str(str, array) {
        var strArr = String(str).replace(/^&/, '').replace(/&$/, '').split('&')
        var sal = strArr.length
        var i
        var j
        var ct
        var p
        var lastObj
        var obj
        var undef
        var chr
        var tmp
        var key
        var value
        var postLeftBracketPos
        var keys
        var keysLen
        var _fixStr = function (str) {
            return decodeURIComponent(str.replace(/\+/g, '%20'))
        }
        var $global = (typeof window !== 'undefined' ? window : global)
        $global.$locutus = $global.$locutus || {}
        var $locutus = $global.$locutus
        $locutus.php = $locutus.php || {}
        if (!array) {
            array = $global
        }
        for (i = 0; i < sal; i++) {
            tmp = strArr[i].split('=')
            key = _fixStr(tmp[0])
            value = (tmp.length < 2) ? '' : _fixStr(tmp[1])
            while (key.charAt(0) === ' ') {
                key = key.slice(1)
            }
            if (key.indexOf('\x00') > -1) {
                key = key.slice(0, key.indexOf('\x00'))
            }
            if (key && key.charAt(0) !== '[') {
                keys = []
                postLeftBracketPos = 0
                for (j = 0; j < key.length; j++) {
                    if (key.charAt(j) === '[' && !postLeftBracketPos) {
                        postLeftBracketPos = j + 1
                    } else if (key.charAt(j) === ']') {
                        if (postLeftBracketPos) {
                            if (!keys.length) {
                                keys.push(key.slice(0, postLeftBracketPos - 1))
                            }
                            keys.push(key.substr(postLeftBracketPos, j - postLeftBracketPos))
                            postLeftBracketPos = 0
                            if (key.charAt(j + 1) !== '[') {
                                break
                            }
                        }
                    }
                }
                if (!keys.length) {
                    keys = [key]
                }
                for (j = 0; j < keys[0].length; j++) {
                    chr = keys[0].charAt(j)
                    if (chr === ' ' || chr === '.' || chr === '[') {
                        keys[0] = keys[0].substr(0, j) + '_' + keys[0].substr(j + 1)
                    }
                    if (chr === '[') {
                        break
                    }
                }
                obj = array
                for (j = 0, keysLen = keys.length; j < keysLen; j++) {
                    key = keys[j].replace(/^['"]/, '').replace(/['"]$/, '')
                    lastObj = obj
                    if ((key !== '' && key !== ' ') || j === 0) {
                        if (obj[key] === undef) {
                            obj[key] = {}
                        }
                        obj = obj[key]
                    } else {
                        // To insert new dimension
                        ct = -1
                        for (p in obj) {
                            if (obj.hasOwnProperty(p)) {
                                if (+p > ct && p.match(/^\d+$/g)) {
                                    ct = +p
                                }
                            }
                        }
                        key = ct + 1
                    }
                }
                lastObj[key] = value
            }
        }
    }



    // that's my wrapper
    var queryString = window.location.search;
    if ('' !== queryString) {
        queryString = queryString.substr(1);
    }
    var arr = {};
    parse_str(queryString, arr);
    return arr;
}
```


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

- 1.2.0 -- 2017-11-15

    - add getUriParams function

- 1.1.0 -- 2016-04-16

    - add js plugins section

- 1.0.0 -- 2016-03-31

    - initial commit
    
