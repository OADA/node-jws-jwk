node-jws-jwk
============

This is basically just [node-jws][] augmented so that
`secretOrKey` can be a [JWk][] or set of [JWKs][].

Example
-------
```javascript
var jws = require('jws-jwk');

var signature = getJWSFromSomwhere();
var jwk = { kid: '1234', kty: 'RSA', n: "12345...XYZ=', e: 'AQAB' };

if (jws.verify(signature, jwk)) {
  // Do stuff here, signature was verified using the JWK
}
```

Overriding [node-js][]
----------------------
You might want to make it so when other code you are using does the following:
```javascript
var jws = require('jws');
```
The module in the variable `jws` is augmented.
One reason to do this is to make modules using [node-jws][]
work with JWKs, e.g. [jsonwebtoken][].
Requiring node-jws-jwk like so will add its augmented functions to the
[node-jws][] module:
```javascript
var jws = require('jws-jwk').shim();
```

In-Browser Usage
----------------
This module shims in [jsrsasign][] when [browserified][browserify]
to make `jws.verify` work in-browser (with JWKs and normally).

References
----------
[node-jws]: https://github.com/brianloveswords/node-jws "jws"
1. [node-jws][]
2. [JSON Web Key (JWK) Draft 31] https://tools.ietf.org/html/draft-ietf-jose-json-web-key-31)
[JWK] https://tools.ietf.org/html/draft-ietf-jose-json-web-key-31#section-4 "JSON Web Key"
[JWKs] https://tools.ietf.org/html/draft-ietf-jose-json-web-key-31#section-5 "JSON Web Key Set"
[jsonwebtoken]: https://github.com/auth0/node-jsonwebtoken
[jsrsasign]: https://github.com/kjur/jsrsasign
[browserify]: https://github.com/substack/node-browserify