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

### Context
```
module.exports = {
    context: path.resolve(__dirname,'src'),               <- ADD Context, work with src folder
    entry: {
        main: './index.js',  [without context:  './src/index.js]
        api: './api.js'      [without context:  './src/api.js]
    },
```   

## 2 Interact with FILE (LOADER) | different from js 
### 2.1 CSS
```
[loader]
npm i -D style-loader, css-loader 

css-loader -  interprets import css and will resolve them.
style-loader - inject style into DOM

require import css
import './styles/style.css'

====================================

const path = require('path');
const HTMLWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');

module.exports = {
    context: path.resolve(__dirname,'src'),
    entry: {
        main: './index.js',
    },
    output: {
        filename: '[name].[contenthash].js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HTMLWebpackPlugin({
            template: './index.html' 
        }),
        new CleanWebpackPlugin()
    ],
    module: {
        rules: [
            {
                test: /\.css$/,
                use: ['style-loader','css-loader']
            }
        ]
    }
}

```
### 2.2 PNG | JPG
```
Prior to webpack 5 it was common to use:

raw-loader to import a file as a string
url-loader to inline a file into the bundle as a data URI
file-loader to emit a file into the output directory
Asset Modules type replaces all of these loaders by adding 4 new module types:

asset/resource emits a separate file and exports the URL. Previously achievable by using file-loader.
asset/inline exports a data URI of the asset. Previously achievable by using url-loader.
asset/source exports the source code of the asset. Previously achievable by using raw-loader.
```

### 2.3 FONT 

WEBPACK 5 [loader]
```
        {
                test: /\.(woff|woff2|eot|ttf|otf)$/i,
                type: 'asset/resource',
        },
```
            
```
const path = require('path');
const HTMLWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');

module.exports = {
    context: path.resolve(__dirname,'src'),
    entry: {
        main: './index.js',
        analytics: './analytics.js'
    },
    output: {
        filename: '[name].[contenthash].js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HTMLWebpackPlugin({
            template: './index.html' 
        }),
        new CleanWebpackPlugin()
    ],
    module: {
        rules: [
            {
                test: /\.css$/,
                use: ['style-loader','css-loader']
            },
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/i,
                type: 'asset/resource',
            },
        ]
    }
}
````

### 3. Optimization
```
    Example. We have two different file. index.js, api.js (webpack entry)
    What happens if two files need the same libery and import axios?
    We will get the same code in both files. (axios)
    
    optimization: {
        splitChunks: {
                chunks: 'all'
        }
    },
    
```
### 4. Dev Server

```
  npm i -D webpack-dev-server
   
  *webpack5*
  
      devServer: {
        open: true,
        hot: true,
        static: {
            directory: path.join(__dirname, "src"),
        }
    },
    
 
*full*
const path = require('path');
const HTMLWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');

module.exports = {
    context: path.resolve(__dirname,'src'),
    entry: {
        main: './index.js',
        api: './api.js'
    },

    output: {
        filename: '[name].[contenthash].js',
        path: path.resolve(__dirname, 'dist')
    },

    optimization: {
        splitChunks: {
                chunks: 'all'
        }
    },

    devServer: {
        open: true,
        hot: true,
        static: {
            directory: path.join(__dirname, "src"),
        }
    },

    plugins: [
        new HTMLWebpackPlugin({
            template: './index.html' 
        }),
        new CleanWebpackPlugin()
    ],

    module: {
        rules: [
            {
                test: /\.css$/,
                use: ['style-loader','css-loader']
            },
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/i,
                type: 'asset/resource',
            },
        ]
    }
}
   
   
```

### 5. Copy

```
npm install copy-webpack-plugin --save-dev

[plugin]

        new CopyWebPackPlugin({
            patterns: [
                {
                    from: path.resolve(__dirname,'src/assets/favicon.ico'),
                    to: path.resolve(__dirname, 'dist')
                }
           ]
        })

```

### 6. Compress CSS, HTML, JS
```
npm install --save-dev mini-css-extract-plugin



const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  plugins: [new MiniCssExtractPlugin()],
  
            =or=
            new MiniCssExtractPlugin({
                filename: '[name].[contenthash].css',
             })
  
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: [{
                 loader: MiniCssExtractPlugin.loader
                 options: { }
    
            }, "css-loader"],
      },
    ],
  },
};


========================
=   Minimize HTML
========================
cross-env
 "scripts": {
    "dev": "cross-env NODE_ENV=development webpack --mode development",
    "build": "cross-env NODE_ENV=production webpack --mode production",
    "watch": "cross-env NODE_ENV=development webpack --mode development --watch",
    "start": "cross-env NODE_ENV=development webpack-dev-server --mode development"
  },

const isDev = process.env.NODE_ENV === 'development'

[plugin]       
       new HTMLWebpackPlugin({
            template: './index.html',
            minify: {
                collapseWhitespace: !isDev
            }
        }),

========================
=   Minimize JS
========================


npm install terser-webpack-plugin --save-dev

        config.minimizer =  [
            new TerserWebpackPlugin()
        ]
        
========================
=   Minimize CSS
========================

npm install --save-dev mini-css-extract-plugin

        config.minimizer =  [
            new CssMinimizerPlugin(),
            new TerserWebpackPlugin()
        ]
 
========================
=  full
========================

const path = require('path');
const HTMLWebpackPlugin = require('html-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');
const CopyWebPackPlugin = require('copy-webpack-plugin')
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const TerserWebpackPlugin = require("terser-webpack-plugin");
const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");


const isDev = process.env.NODE_ENV === 'development'
console.log('IS DEV:', isDev);

const optimization = () => {
    const config = {
         splitChunks: {
           chunks: 'all'
        }
    }

    if(!isDev) {
        config.minimizer =  [
            new CssMinimizerPlugin(),
            new TerserWebpackPlugin()
        ]
    }

    return config;
} 

module.exports = {
    context: path.resolve(__dirname,'src'),
    entry: {
        main: './index.js',
        analytics: './analytics.js'
    },
    
    output: {
        filename: '[name].[contenthash].js',
        path: path.resolve(__dirname, 'dist')
    },

    optimization: optimization(),

    devServer: {
        open: true,
        hot: true,
        static: {
            directory: path.join(__dirname, "src"),
        }
    },

    plugins: [
        new HTMLWebpackPlugin({
            template: './index.html',
            minify: {
                collapseWhitespace: !isDev
            }
        }),
        new CleanWebpackPlugin(),
        new CopyWebPackPlugin({
            patterns: [
                {
                    from: path.resolve(__dirname,'src/assets/favicon.ico'),
                    to: path.resolve(__dirname, 'dist')
                }
           ]
        }),
        new MiniCssExtractPlugin({
            filename: '[name].[contenthash].css',
        })
    ],

    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    {
                        loader: MiniCssExtractPlugin.loader,
                        options: {
                          
                        }
                    },
                    'css-loader'
                ]
            },
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/i,
                type: 'asset/resource',
            },
        ]
    }
}
  
```
### 7.sass

npm install sass-loader sass webpack --save-dev

            {
                test: /\.s[ac]ss$/,
                use: [
                    {
                        loader: MiniCssExtractPlugin.loader,
                        options: {}
                    },
                    'css-loader',
                    "sass-loader",
                ]
            },
 ### 8. TS through Babel
 
 npm install --save-dev babel-loader @babel/core
 
 npm install --save-dev @babel/preset-env
 npm install --save-dev @babel/preset-typescript
 
             {
                test: /\.ts$/,
                exclude: /node_modules/,
                use: {
                  loader: "babel-loader",
                  options: {
                    presets: [
                        "@babel/preset-env", 
                        "@babel/preset-typescript"
                    ]
                  }
                }
            },
 
