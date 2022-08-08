# posthtml-beautify

> A [posthtml](https://github.com/posthtml) plugin to beautify you html files

[![Travis Build Status](https://img.shields.io/travis/posthtml/posthtml-beautify/master.svg?style=flat-square&label=unix)](https://travis-ci.org/posthtml/posthtml-beautify)[![node](https://img.shields.io/node/v/post-sequence.svg?maxAge=2592000&style=flat-square)]()[![npm version](https://img.shields.io/npm/v/posthtml-beautify.svg?style=flat-square)](https://www.npmjs.com/package/posthtml-beautify)[![Dependency Status](https://david-dm.org/gitscrum/posthtml-beautify.svg?style=flat-square)](https://david-dm.org/gitscrum/posthtml-beautify)[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg?style=flat-square)](https://github.com/sindresorhus/xo)[![Coveralls status](https://img.shields.io/coveralls/posthtml/posthtml-beautify.svg?style=flat-square)](https://coveralls.io/r/posthtml/posthtml-beautify)

[![npm downloads](https://img.shields.io/npm/dm/posthtml-beautify.svg?style=flat-square)](https://www.npmjs.com/package/posthtml-beautify)[![npm](https://img.shields.io/npm/dt/posthtml-beautify.svg?style=flat-square)](https://www.npmjs.com/package/posthtml-beautify)[![Package Quality](http://npm.packagequality.com/shield/posthtml-beautify.svg?style=flat-square)](http://packagequality.com/#?package=posthtml-beautify)

## Why?
Format your html and inline css markup according to the [HTML5 syntax Style Guide](http://www.w3schools.com/html/html5_syntax.asp), [Code Guide](http://codeguide.co/#html). Full list of supported options:
- [x] Transform lower case element names
- [x] Transform lower case attribute names
- [x] Only double quotes
- [x] Close all html elements 
- [x] Removing trailing slash in self-closing 
- [x] Removes spaces at the equal sign
- [x] Add blank lines to separate large or logical code blocks
- [x] Add 2 spaces of indentation. *Do not use TAB*.
- [x] Add language attribute
- [ ] Add character encoding
- [x] Attribute order
- [x] Boolean attributes
- [ ] Creates file from the inline styles
- [ ] Create scoped class name (*use css-modules*) instead inline styles
- [ ] validate elements and attributes name
- [x] parses Internet Explorer Conditional Comments (*not support Downlevel-revealed and valid version, [htmlparse2 invalid parses](https://github.com/posthtml/posthtml-beautify/issues/36)*)

## Install

```bash
npm i -S posthtml posthtml-beautify
```

> **Note:** This project is compatible with node v10+

## Usage

```js
import {readFileSync, writeFileSync} from 'fs';
import posthtml from 'posthtml';
import beautify from 'posthtml-beautify';

const html = readFileSync('input.html', 'utf8');

posthtml()
  .use(beautify({rules: {indent: 4}}))
  .process(html)
  .then(result => {
    writeFileSync('output.html', result.html);
  });

```
*Returns html-formatted according to rules based on the use [HTML5 syntax Style Guide](http://www.w3schools.com/html/html5_syntax.asp), [Code Guide](http://codeguide.co/#html) with custom settings `indent: 4`*

## [Example](https://posthtml.github.io/posthtml-beautify/)

## Options

### `rules`
Type: `Object`  
Default:

  - **Indent**  
  Type: `Number|String(only tab)`  
  Default: 2  
  Description: *A numeric value indicates specifies the number of spaces. The string value only `tab`*

  - **blankLines**  
  Type: `String|Boolean(only false)`  
  Default: '\n'  
  Description: *Add or remove blank lines to separate large or logical code blocks*

  - **eol** (*end of line*)  
  Type: `String`  
  Default: '\n'  
  Description: *As value is a string symbol which is added to the end of the row*

  - **eof** (*end of file*)  
  Type: `String|Boolean`  
  Default: '\n'  
  Description: *As value is a string symbol which is added to the end of the file and will not adds if you specify a [boolean](https://www.scaler.com/topics/boolean-in-javascript/) value of `false`*

  - **maxlen**  
  Type: `Number`  
  Default: '80'  
  Description: *checks for the max length of the content, indents the whole content to a new line*

  - **sortAttr**  
  Type: `Boolean`  
  Default: false  
  Description: *Sort the order of attributes in elements*

  - **lang**  
  Type: `String | Boolean(only false)`  
  Default: false  
  Description: *Add a `lang` attribute in elements, eg: `{ lang: 'fr' }`*

  - **commentFormat**  
  Type: `Boolean`  
  Default: true  
  Description: Formats the comments. It does the following 
    - If there are multi line comments then there would be 
      leading and trailing newline like this 

      ```html
      // Input

      <!-- multiline 
      comments-->

      // Output

      <!-- 
      multiline 
      comments
      -->
      ``` 
    - If there is a single line comment, it would make it to a single line with the comment starting and ending
      notation in same line

      Input
      ```
      <!-- 
        singleline comments
      -->
      ```

      Output

      `<!-- singleline comments -->`


### `mini`
Type: `Object`  
Default:

  - **removeAttribute**  
  Type: `String|Boolean`  
  Default: false  
  Description: *Removes attributes that do not matter. The string value only `empty`*

### `jsBeautifyOptions`
Type: `Object`  
Default: *All options as per package [js-beautify](https://github.com/beautify-web/js-beautify) except, `indent_level` because calculated and set according to context*

## Related
  - [js-beautify](https://github.com/beautify-web/js-beautify) - Beautifier for javascript
