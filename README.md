# chore-minimum-js
## Eslint
```
  npm install --save-dev eslint eslint-config-airbnb-base eslint-plugin-import
  npm install --save-dev jest
  node --experimental-vm-modules node_modules/jest/bin/jest.js
  
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
   
```
## linux
```
du: 
  du -h --max-depth=1 | sort -rh
```

### postgresql:
```
sudo -u postgres createuser --createdb nameRole

dropuser nameRole
createdb nameDB

```
