 ```
  npm install --save-dev eslint eslint-config-airbnb-base eslint-plugin-import
  npm install --save-dev jest
  node --experimental-vm-modules node_modules/jest/bin/jest.js
  ```
  
  file: .eslintrc
  ===================
 
 env:
  jest: true
  
 extends: airbnb-base
 
 rules: {
  no-console: off
}


/* eslint-disable no-unused-vars */
exports.serverError = (err, req, res, next) => res.render('500');
/* eslint-enable no-unused-vars */
   
##config .eslintrc

```
env:
  browser: true
  es2021: true
  node: true
  jest: true
extends:
  - 'airbnb-base'
parserOptions:
  ecmaVersion: latest
  sourceType: module
rules: {
  "no-underscore-dangle": 'off'
}
```
