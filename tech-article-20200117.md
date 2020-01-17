## 文章分享
### 1. [纯CSS实现简单骨骼动画](https://juejin.im/post/5deb49a251882512302daa92#heading-0)
骨骼动画原理：人的运动——走，跑，跳，是由骨骼带动躯干和四肢完成的。「骨骼动画」，顾名思义，就是模拟骨骼运动的机制而制作的动画。详见：[骨骼动画原理与前端实现浅谈](https://xieguanglei.github.io/blog/post/skeleton.html)      

**如何纯CSS实现简单骨骼动画？** 
* 1.分离元素：拆分需要生成动画的物体
* 2.添加动效：主要使用animation和transform

### 2. [AntV/G2Plot 开源 - 精雕细琢，打造极致可视化图表体验](https://zhuanlan.zhihu.com/p/102488345)
视频地址：[第三届 SEE Conf 2020: 精雕细琢，打造极致可视化图表体验](https://zhuanlan.zhihu.com/p/102488345)             
ppt下载地址：[精雕细琢，打造极致可视化图表体验](https://www.yuque.com/attachments/yuque/0/2020/pdf/84182/1578899633581-6feb4b27-5f01-410c-91c1-648f2a4dd036.pdf?from=https%3A%2F%2Fwww.yuque.com%2Fseeconf%2F2020%2Fslide)

#### 1.架构升级
* **约束布局**
Auto Padding（向内收缩） :fa-arrow-right:  约束布局（线性等式，不等式的非负解求解算法）

* **交互语法**
Event API :fa-arrow-right: 交互语法
![1](https://github.com/0ragdoll0/share/blob/master/pics/20200117/1.png)

#### 2.打磨图表细节体验
* **主要针对：折线图，柱状图，饼图**
* **主要改进：标签描边，标签重叠的处理，数据过多...**

### 3. [欢迎进入 2020 数据可视化智能研发时代](https://zhuanlan.zhihu.com/p/101427562)
**AVA**：一个智能可视分析框架，包含研发时的智能研发向导，阅读时的智能交互增强，可视分析时的智能辅助
####  当前实现的可视化智能研发
* **可视化 UI 配置面板**
```
// 唤起 AVA 研发态的可视化 UI 配置面板，自由调整，即时生效。调整完成，拷贝配置到代码，开发就完成了。
AVA.autoChart(container, data, { config: { type: 'line' }});
```
* **ChartCube设计到研发链路打通**
通过代码在研发时唤起 AVA 的可视化 UI 配置面板去还原设计稿，这是给前端工程师的专属武器，但如果设计师、产品经理也是用 AVA 的能力去做设计搞，工程师又何必动武呢？ChartCube 正是为此准备，这是给设计师、产品经理准备的专属武器，从 ChartCube 到 AVA，设计到研发链路打通，设计合理性、技术可行性无需反复沟通，中间产物可以被无缝连接，设计还原零失真。

* **智能向导模式**
```
// 你会看到 AVA 的研发向导，选择「从数据特征开始」，仅需数据特征即可自动生成 Mock 数据，为可视化研发提供研发态数据准备。
AVA.autoChart(container, []);
```
## 业务相关分享
### vuex-module-decorators与vuex返回的Error差异
**1. 项目中出现的bug**
预期：断网时，页面发出请求后应提示“网络出错，请检查网络或稍后重试”
实际：页面发出请求后先提示“获取数据失败”，再提示“网络出错，请检查网络或稍后重试”
相关代码：
```
// 实际调用
try {
      await this.fetchRecommendedQuestions(params)
} catch (e) {
      if (e && e.isHandled) {
        return
      }
      this.$message.error('获取变式题失败')
    }
```
```
// App.comp.ts中对请求异常的处理
if (!error || !error.response) {
      error.isHandled = true
      this.showNetErrorMessage({
        message: '网络出错',
      })
      return
    }
```
App.comp.ts中对请求异常Error的处理后，error.isHandled应该置为true，实际调用处应直接return，不应出现二次提示。但实际情况是出现了二次提示。

**2. 实际返回的Error是什么？**
通过观察发现，之前使用js+vuex写的页面不会出现二次提示。对比一下使用vuex和vuex-module-decorators时，实际调用Action方法时，返回的Error及其error.isHandled
vuex：
![2](https://github.com/0ragdoll0/share/blob/master/pics/20200117/2.png)
vuex-module-decorators：
![3](https://github.com/0ragdoll0/share/blob/master/pics/20200117/3.png)

可见vuex-module-decorators返回的error.isHandled为undefined。因此会出现二次提示。

**3. 为什么error.isHandled为undefined**
vuex-module-decorators源码中，Action装饰器，对error进行了处理。对原始error进行了包裹，因此返回的error并不是原始error，error.isHandled当然为undefined。
```
catch (e) {
        throw rawError
          ? e
          : new Error(
              'ERR_ACTION_ACCESS_UNDEFINED: Are you trying to access ' +
                'this.someMutation() or this.someGetter inside an @Action? \n' +
                'That works only in dynamic modules. \n' +
                'If not dynamic use this.context.commit("mutationName", payload) ' +
                'and this.context.getters["getterName"]' +
                '\n' +
                new Error(`Could not perform action ${key.toString()}`).stack +
                '\n' +
                e.stack
            )
      }
```
**4. 处理方法**
为装饰器添加rawError参数
```
@Action({ rawError: true })
```



