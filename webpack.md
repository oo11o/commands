### install, npm run
```
    npm i -D webpack webpack-cli
    
   "scripts": {
     "dev": "webpack --mode development",
      "build": "webpack --mode production"
    },
    
```

### min
```
const path = require('path');

module.exports = {
    mode: 'development',
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
}
```
### multiply entry and hash

```
module.exports = {
    entry: {
        main: './src/index.js',
        api: './src/api.js'
    },
    output: {
        filename: '[name].bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
}

Output: main.bundle.js
        api.bundle.js
        
        
======================================================        
        option HASH
======================================================
    output: {
        filename: '[name].[contenthash].js',
        ...
    }
    
Output: main.6c07c1fd62a63b9edd6a.js
        api.257c1fd62a63bwe23ssa.js    

```
### HTMLWebpackPlugin
```
    [plugin]
    npm i -D html-webpack-plugin    [generate html-files based on html-templates(src/index.html) include js] 
    npm i -D clear-webpack-plugin   [clear generated old files] 
    
    const path = require('path');
    
===========================================    
const path = require('path');    
const HTMLWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');

module.exports = {
    entry: {
        main: './src/index.js',
    },
    output: {
        filename: '[name].[contenthash].js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HTMLWebpackPlugin({
            template: './src/index.html' 
        }),
        new CleanWebpackPlugin()
    ]
}
```
