用Webpack打包Backend时报错，日志如下：
```
module.exports = require("chalk");
                 ^

Error [ERR_REQUIRE_ESM]: require() of ES Module /Users/yourname/Workspace/backend/node_modules/chalk/source/index.js from /Users/yourname/Workspace/backend/dist/app.js not supported.
Instead change the require of index.js in /Users/yourname/Workspace/backend/dist/app.js to a dynamic import() which is available in all CommonJS modules.
    at Object.chalk (/Users/yourname/Workspace/backend/dist/app.js:349:18)
    at __webpack_require__ (/Users/yourname/Workspace/backend/dist/app.js:533:41)
    at eval (webpack://rsg-backend/./src/logger/index.js?:9:63)
    at Object../src/logger/index.js (/Users/yourname/Workspace/backend/dist/app.js:139:1)
    at __webpack_require__ (/Users/yourname/Workspace/backend/dist/app.js:533:41)
    at eval (webpack://rsg-backend/./src/main.js?:20:74)
    at Object../src/main.js (/Users/yourname/Workspace/backend/dist/app.js:149:1)
    at __webpack_require__ (/Users/yourname/Workspace/backend/dist/app.js:533:41)
    at /Users/yourname/Workspace/backend/dist/app.js:585:37
    at Object.<anonymous> (/Users/yourname/Workspace/backend/dist/app.js:587:12) {
  code: 'ERR_REQUIRE_ESM'
```

查了一下是chalk升级到最新版本`5.2.0`，回退版本解决。

先remove
```shell
yarn remove chalk
```
然后再重新安装4.x最新版本。
```shell
yarn add chalk@^4.1.2
```