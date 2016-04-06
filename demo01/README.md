## 开始编译

在终端运行`$ webpack ./entry.js bundle.js`，编译`entry.js`文件并且生成`bundle.js`


output
```bash
Hash: 8b231dfafb36fcecaafd
Version: webpack 1.12.14
Time: 41ms
    Asset     Size  Chunks             Chunk Names
bundle.js  1.42 kB       0  [emitted]  main
   [0] ./entry.js 28 bytes {0} [built]
```

在浏览器中打开`index.html`，显示结果：

It works.

## 第二个文件

接着，我们新增一个名为`content.js`的文件

更新`entry.js`内容为
```js
document.write(require("./content.js"));
```

再次运行`$ webpack ./entry.js bundle.js`

webpack output
```bash
Hash: 7e44ccfcefd4fb69018a
Version: webpack 1.12.14
Time: 49ms
    Asset     Size  Chunks             Chunk Names
bundle.js  1.55 kB       0  [emitted]  main
   [0] ./entry.js 41 bytes {0} [built]
   [1] ./content.js 46 bytes {0} [built]
```

## 第一个loader

安装以下loader
```bash
npm install css-loader style-loader
```

新增一个名为`style.css`样式文件，并添加以下内容：
```css
body {
    background: yellow;
}
```

修改`entry.js`,添加以下语句：
```js
require("!style!css!./style.css");
```

重新编译并用浏览器查看结果，会发现页面背景变成黄色。

## 配置文件

每次编译的时候输入过长的字符对于程序猿是个折磨，更好的办法是将其写入到配置文件中。

新建一个名为`webpack.config.js`的文件

```js
module.exports = {
    entry: "./entry.js",
    output: {
        path: __dirname,
        filename: "bundle.js"
    },
    module: {
        loaders: [
            { test: /\.css$/, loader: "style!css" }
        ]
    }
};
```

现在，我们只需要在命令行中运行`webpack`

webpack output

```bash
Hash: 3b0c30ec48200e410020
Version: webpack 1.12.14
Time: 603ms
    Asset     Size  Chunks             Chunk Names
bundle.js  11.8 kB       0  [emitted]  main
   [0] ./entry.js 64 bytes {0} [built]
   [5] ./content.js 46 bytes {0} [built]
    + 4 hidden modules
```

## 更美观的输出

随着项目的日渐庞大，编译时间很有可能越来越久，所以我们希望能够出现一个进度条，当然如果能有艳丽的颜色更棒！

```bash
webpack --progress --colors
```

## 监控模式

我们不希望每次修改代码后都需要手动去编译它。

```bash
webpack --progress --colors --watch
```

## 开发服务器
