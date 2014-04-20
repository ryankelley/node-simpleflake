node-simpleflake
================

[![travis](http://img.shields.io/travis/simonratner/node-simpleflake.svg)](https://travis-ci.org/simonratner/node-simpleflake) &nbsp;
[![deps](http://david-dm.org/simonratner/node-simpleflake.svg)](https://david-dm.org/simonratner/node-simpleflake) &nbsp;
[![npm](http://img.shields.io/npm/v/simpleflake.svg)](https://www.npmjs.org/package/simpleflake)

Distributed id generation for the lazy. Inspired by [this article](http://engineering.custommade.com/simpleflake-distributed-id-generation-for-the-lazy/).

Generates ids consisting of a 41 bit time (millisecond precision with custom
epoch) followed 23 random bits. Result is a `Buffer` with an added feature
of base58 and base10 conversions for producing compact and readable strings.

Custom epoch starts on 2000-01-01T00:00:00.000Z, which should be good until
around mid-2069.

Install
-------
```
npm install simpleflake
```

Use
---
Generate an id using current time and a random sequence number:
```javascript
var flake = require('simpleflake');
var id = flake();                         // <Buffer 34 62 a7 d5 c7 36 7c b9>
id.toString('hex');                       // '3462a7d5c7367cb9'
id.toString('base58');                    // '9mCpPjW7D5a'
id.toString('base10');                    // '3774763974302006457'
```

Generate an id using deterministic time and sequence:
```javascript
var id = flake(Date.UTC(2014, 1, 1), 1);  // <Buffer 33 bf f7 7e 00 00 00 01>
```

Parse an id into its time and sequence components:
```javascript
flake.parse(id);                                  // [ 1396671731598, 3570873 ]
flake.parse('9mCpPjW7D5a', 'base58');             // [ 1396671731598, 3570873 ]
flake.parse('3774763974302006457', 'base10');     // [ 1396671731598, 3570873 ]
```

Customise generation options (default values shown):
```javascript
flake.options.epoch = Date.UTC(2000, 0, 1);
flake.options.timebits = 41;
```

License
-------

The MIT License (MIT)

Copyright (c) 2014 Simon Ratner

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
