## 新闻
### StateOfJS 发布了 2019 年 JavaScript 生态圈调查报告
*  **语言选择：** TypeScript 一骑绝尘，但 Reason 与 TypeScript 一样，都拥有着高使用率和高满意度。
*  **框架：** React 仍保持第一，而 Vue 紧随其后位居第二。在 GitHub 上，Vue 以 155k 的 star 数超越了 React 的 141k，未来将有机会坐上冠军宝座。
*  **数据层：** Redux 依旧是应用最广泛的数据层工具，Apollo 的用户从 2018 年的 11.1% 增长到今年的 24.9% 。
*  **后端框架：** 没有取得重大突破，虽然新的框架不断出现，但还是没有可以挑战 Express 地位的成功框架出现。值得一提的是 Next.js，虽无法撼动 Express 的霸主地位，但因其专注于解决 React 应用的服务器渲染问题的特性，其用户数已从 2018 年的 8.6% 上升到了 24.7%。

### JavaScript 引擎 V8 发布 v8.0 版本
12 月 18 日，JavaScript 引擎 V8 发布 v8.0 版本，此版本除了修复一些 bug 外，还带来了性能的提高。
* 性能改进
    * 指针压缩：经过测试，平均节省了 40％ 的堆内存
    * 优化高阶内置程序：消除了 TurboFan 优化管道中的一个限制，该限制阻止了对高阶内置函数的优化。

* JS新特性
    * Optional Chaining：使开发者可以编写更可靠的属性访问链，以检查中间值是否为空。如果中间值是空值，则整个表达式的计算结果为 undefined。
    ```
    const nameLength = db?.user?.name?.length;
    ```
    * null合并:`a ?? b `当a为null或undefined时运算结果为`b`，否则应为`a`。避免使用`a || b `取默认值时, `a`为`false`的情况。

## 文章
### 1.[face-api.js — JavaScript API for Face Recognition in the Browser with tensorflow.js](https://itnext.io/face-api-js-javascript-api-for-face-recognition-in-the-browser-with-tensorflow-js-bcc2a6c4cf07)
face-api.js是一个建立在「tensorflow.js」内核上的 javascript 模块，它实现了三种卷积神经网络（CNN）架构，用于完成人脸检测、识别和特征点检测任务。
* 人脸检测：人脸边框预测，返回每张人脸的边界框，并返回每个边框相应的分数。
* 人脸对齐：使人脸识别更加准确。
* 人脸特征点检测：返回给定图像的 68 个人脸特征点。
* 人脸识别：将对齐后的人脸图像输入到人脸识别网络中，该网络已经被训练去学习出人脸特征到人脸描述符的映射。人脸识别通过对比两个人脸描述符之间的欧氏距离判断两张人脸图像是否相似。

### 2.[纯前端实现人脸识别自动佩戴圣诞帽](http://kms.netease.com/article/13818)
使用face-api.js中的人脸检测检测和特征点检测，为图片中的人物戴上圣诞帽。


