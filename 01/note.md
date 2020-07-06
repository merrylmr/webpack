webpack版本：4.43.0

## 基本使用

新建一个空项目


1.在项目下安装webpack

```javascript
yarn add -D webpack webpack-cli
```


2.使用webpack


index.html文件引入打包之后的文件

````html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div class="logo">
  <h1>logo</h1>
</div>
<!--webpack输入的文件-->
<script src="./dist/bundle.js"></script>
</body>
</html>
````
 index.js
```javascript

function printf() {
  console.log('hello,world');
}

printf();
```

webpack.config.js
```javascript
const path = require('path');

module.exports = {
  // JavaScript 执行入口文件
  entry: './js/index.js',
  output: {
    // 把所有依赖的模块合并输出到一个 bundle.js 文件
    filename: 'bundle.js',
    // 输出文件都放到 dist 目录下
    path: path.resolve(__dirname, './dist'),
  }
};
```

在package.json的"scripts"配置
 `dev:webpack --config=webpack.config.js`
 
运行`yarn dev`即可

 
 
###  使用loader

1.index.js添加`main.css`

```javascript
import '../css/main.css'
function printf() {
  console.log('hello,1111');
}

printf();
```

2.webpack.config.js添加module

```javascript
module.exports = {
  module: {
    rules: [
      {
        // 用正则去匹配要用该 loader 转换的 CSS 文件
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      }
    ]
  }
};
```

### 使用plugin

把注入到bundle.js文件里面的css提取到单独的文件中

```javascript
module.exports = {
plugins: [
    new ExtractTextPlugin({
      // 从 .js 文件中提取出来的 .css 文件的名称
      filename: `[name]_[md5:contenthash:hex:8].css`,
    }),
  ]
}
```


注意：如果安装的是webpack4，需要安装最新的版本
`yarn add -D extract-text-webpack-plugin@next`

filename:[contenthash:8]需要改变成[md5:contenthash:hex:8]


### devServer使用

1.提供 HTTP 服务而不是使用本地文件预览；

2.监听文件的变化并自动刷新网页，做到实时预览；

3.支持 Source Map，以方便调试。





