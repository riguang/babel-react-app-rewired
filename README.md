在create-react-app中使用装饰器

create-react-app ExampleApp
npm run eject

//非react
npm install --save-dev babel-plugin-transform-decorators-legacy

//针对react
npm install babel-preset-stage-2 --save-dev
npm install babel-preset-react-native-stage-0 --save-dev
npm install --save mobx mobx-react
根目录下创建.babelrc

// react
{
  "presets": ["react-native-stage-0/decorator-support"]
}

// 非react
{
  "presets": [
    "es2015",
    "stage-1"
  ],
  "plugins": ["transform-decorators-legacy"]
}
--------------------------------------------------------------------
https://github.com/timarney/react-app-rewired

Utilities (injectBabelPlugin)

Adding a Babel plugin can be done via the injectBabelPlugin(pluginName, config) function. You can also use the "rewire" packages from this repo or listed below to do common config modifications.

const rewireMobX = require('react-app-rewire-mobx');
const rewirePreact = require('react-app-rewire-preact');
const {injectBabelPlugin} = require('react-app-rewired');

/* config-overrides.js */
module.exports = function override(config, env) {
  // add a plugin
  config = injectBabelPlugin('emotion/babel',config)
  
  // use the Preact rewire
  if (env === "production") {
    console.log("⚡ Production build with Preact");
    config = rewirePreact(config, env);
  }
  
  // use the MobX rewire
  config = rewireMobX(config,env);
  
  return config;
}