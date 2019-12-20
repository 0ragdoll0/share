## Chrome DevTools Performance Tab
### 模块划分
* 控制面板
profile配置参数选择
![1](https://github.com/0ragdoll0/share/blob/master/pics/20191220/1.png)
* 概览面板
FPS,CPU,NET
![2](https://github.com/0ragdoll0/share/blob/master/pics/20191220/2.png)
* 线程面板
Frames,Main,Raster
![3](https://github.com/0ragdoll0/share/blob/master/pics/20191220/3.png)
* 统计面板
![4](https://github.com/0ragdoll0/share/blob/master/pics/20191220/4.png)

## 项目性能分析
performance = loading performance + redenring performance       
### 分析过程
由于Summary中显示Rendering占比最高，因此主要进行对redenring performance的分析。查看线程面板的Main和统计面板的Call Tree，分析有无造成Render时间过长的原因
![5](https://github.com/0ragdoll0/share/blob/master/pics/20191220/5.png)
* 由线程面板的Main可看出由36s到70s的期间，一直在执行同一个task，且一直在进行recalculate style
![6](https://github.com/0ragdoll0/share/blob/master/pics/20191220/6.png)

* 点击对应task，查看Call Tree。发现recalculate style是因执行StudentWorkbook的computeStyle造成

![7](https://github.com/0ragdoll0/share/blob/master/pics/20191220/7.png)   

computeStyle函数如下，猜测在使用getPropertyValue获取元素高度之前，使用js改变了元素的样式，导致等待recalculate style的时间过长。
```
  private computeStyle(): void {
    const { workbookContent } = this
    topContainer.style.display = 'block'
    const height = window
      .getComputedStyle(workbookContent)
      .getPropertyValue('height')
    this.workbookHeight = Number(height.substring(0, height.length - 2))
    topContainer.style.display = ''
    this.shouldUpdate = false
  }
```

删除`topContainer.style.display = 'block'`后重新录制profile，大幅减少时间
![8](https://github.com/0ragdoll0/share/blob/master/pics/20191220/8.png)   

### Avoid forced synchronous layouts
Shipping a frame to screen has this order:   
![9](https://github.com/0ragdoll0/share/blob/master/pics/20191220/9.png)
First the JavaScript runs, then style calculations, then layout. It is, however, possible to force a browser to perform layout earlier with JavaScript. It is called a forced synchronous layout.                      
eg：[实例](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing)













