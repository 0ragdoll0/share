## 网页水印
### 实现思路
1. 结构
```
<div class="content-Container">
  <div class="content">
    content
  </div>
  <water-mark class="water-mark"/>
<div>
```

2. 实现：定位 + z-index
```
.content-Container {
  position: relative;
  .content {
    position: relative;
  }
  .water-mark {
    position: absolute;
  }
}
```
3. 生成水印
文字/img/canvas等均可

### 生成平铺水印
类似
![avoid](https://github.com/0ragdoll0/share/blob/master/pics/20191122/1.png)

需要两个canvas
1. 生成水印基础文字
利用canvas1生成单个图片img
![avoid](https://github.com/0ragdoll0/share/blob/master/pics/20191122/2.png)


2. 生产平铺水印
调用canvas2的createPattern方法，在repetition指定的方向上重复canvas1生成的图片（或跳过第一步使用制定图片）。
```
CanvasPattern ctx.createPattern(image, repetition)
```
repetition: "repeat"/"repeat-x"/"repeat-y"/"no-repeat"

### 问题
1. 需要动态获取需要生成水印的content的宽高，宽高改变后需要重置canvas的宽高，重新绘制水印层
2. 如何获取样式为`display: none`的元素的宽和高
    * 元素style或class中明确写明width和height值=>可直接使用`window.getComputedStyle(Element).getPropertyValue('width')` 
    * 元素style或class中明确写明width和height值=> 使用上述方法，返回auto。因此1）需要将元素设置为`display: block`2）使用`window.getComputedStyle(Element).getPropertyValue('width')` 3）设置`display: none`
    （注：需要考虑此操作和项目本身样式的冲突）

3. 水印打印问题：虽获取了元素宽高，可为其水印。但在打印时页面会使用`break-inside: avoid;`使表格，图片等不从分页处截断，是否会影响元素实际的打印高度？


