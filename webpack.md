## make a bundle
webpack yourPrincipalScript.js ./boundle.js
------yourPrincipalScript.js----------|
var message = require("./script.2");  |
------script.2.js---------------------|
module.exports = "this is an alert";   |
--------------------------------------|

## config file 
webpack.config.js
module.exports = {
  entry : './src/script.1.js',
  output : {
    path : 'dist',
    filename : 'boundle.js'
  }
}
-----then is just type webpack

## webpack.config.js
var webpack = require('webpack');
var path = require('path');

var BUILD_DIR = path.resolve(__dirname, 'src/client/public');
var APP_DIR = path.resolve(__dirname, 'src/client/app');

var config = {
  entry: APP_DIR + '/index.jsx',
  output: {
    path: BUILD_DIR,
    filename: 'bundle.js'
  },
  module : {
    loaders : [
      {
        test : /\.jsx?/,
        include : APP_DIR,
        loader : 'babel'
      }
    ]
  }
};
module.exports = config;
--------------------------------------------------------------------------
## command
### build
webpack -d
### build watch
webpack -d --watch