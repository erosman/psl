# PSL (Public Suffix List)
JavaScript module for parsing `hostname`, based on the [The Public Suffix List](https://github.com/publicsuffix/list).

## The Public Suffix List

A "public suffix" is one under which Internet users can (or historically could) directly register names. Some examples of public suffixes are .com, .co.uk and pvt.k12.ma.us. The Public Suffix List is a list of all known public suffixes.

See https://publicsuffix.org/ and the [Wiki](https://github.com/publicsuffix/list/wiki) link above for more information.

## How to Use

Include `psl.js` as a module and `import` for use.

`parse()` returns an `Object` with the following properties:

- **subdomain**: `string` parts before the domain
- **domain**: `string` domain name (i.e. sld + tld)
- **sld**: `string` Second level domain (i.e. domain without tld)
- **tld**: `string` Top level domain (i.e. The Public Suffix)


### Example
```js
import {PSL} from './psl.js';


// domain without subdomain
const psl1 = PSL.parse('example.com');
console.log(psl1.subdomain);    // ''
console.log(psl1.domain);       // 'example.com'
console.log(psl1.sld);          // 'example'
console.log(psl1.tld);          // 'com'

// domain with subdomain
const psl2 = PSL.parse('www.example.com');
console.log(psl2.subdomain);    // 'www'
console.log(psl2.domain);       // 'example.com'
console.log(psl2.sld);          // 'example'
console.log(psl2.tld);          // 'com'

// domain with nested subdomains
const psl3 = PSL.parse('a.b.c.example.com');
console.log(psl3.tld);          // 'com'
console.log(psl3.domain);       // 'example.com'
console.log(psl3.sld);          // 'example'
console.log(psl3.subdomain);    // 'a.b.c'
```
