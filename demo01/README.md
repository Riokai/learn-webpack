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

## 绑定loaders
