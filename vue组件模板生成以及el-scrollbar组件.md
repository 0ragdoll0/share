## 文件模板生成方法
### 1.vscode
使用vscode自带的user snippets
#### 步骤：
1. preferences --> user snippets --> 选择/新建需要生成模板的文件类型
2. 编辑对应的代码片段配置。  
具体配置项可参照:[https://code.visualstudio.com/docs/editor/userdefinedsnippets](https://code.visualstudio.com/docs/editor/userdefinedsnippets)

#### 实例：
为vue文件创建模板
1. vue.json代码片段配置
```
{
	// Example:
	"Print to console": {
		"prefix": "vue",
		"body": [
			"<template>",
			"  <div>$0$TM_FILENAME_BASE</div>",
			"</template>",
			"",
			"<script src=\"./$TM_FILENAME_BASE.comp.ts\" lang=\"ts\">",
			"</script>",
			"<style src=\"./$TM_FILENAME_BASE.comp.scss\" lang=\"scss\" scoped>",
			"</style>"
		],
		"description": "Log output to console"
	}
}
```
2. 创建vue文件  
* 创建文件AnalysisContent.vue，输入vue触发user snippets
![usersnippets](https://github.com/0ragdoll0/share/blob/master/pics/20191012/1.png)
* 使用user snippets（主要功能为根据文件名动态生成script和style的src）
![usersnippets1](https://github.com/0ragdoll0/share/blob/master/pics/20191012/2.png)

### 局限：
* **不适用于生成复杂文件模板**   
配置文件的body（即模板内容）需要逐句填写，因此更加试用于小段代码的补全/生成简单文件模板，不适用于生成简单文件模板（例如vue-class-component）
* **效率较低**  
需要先创建文件，再使用user snippets生成模板。项目中使用文件夹封装组件，因此新建一个组件需要手动创建多个文件再分别使用user snippets。

### 2.node生成
1. 功能：根据模板生成vue组件文件夹，并且替换文件中的ComponentName为输入的组件名称。
2. 构成
   * index.ts（主要功能代码）
   * template文件夹（模板文件存放）
   * 如图：![folder](https://github.com/0ragdoll0/share/blob/master/pics/20191012/3.png)
3. 使用方法：在需要生成组件的路径，运行componentCreate/index.ts，输入组件名称
4. 修改模板方法：修改componentCreate/template中的文件即可
5. 获取地址：[componentCreate](https://github.com/0ragdoll0/tool.git)
6. 实例：
    * 路径转到项目的components文件夹，运行componentCreate/index.ts![1](https://github.com/0ragdoll0/share/blob/master/pics/20191012/4.png)
    * 输入组件名，创建组件文件夹![2](https://github.com/0ragdoll0/share/blob/master/pics/20191012/5.png)
    * 生成模板文件![3](https://github.com/0ragdoll0/share/blob/master/pics/20191012/6.png)![4](https://github.com/0ragdoll0/share/blob/master/pics/20191012/7.png)![5](https://github.com/0ragdoll0/share/blob/master/pics/20191012/8.png)![6](https://github.com/0ragdoll0/share/blob/master/pics/20191012/9.png)
    
## elementui中的el-scrollbar
==el-scrollbar==在elementui的一些组件以及其官网中被使用，但在elementui官方文档中未提及。
如图：![el-scroll1](https://github.com/0ragdoll0/share/blob/master/pics/20191012/10.png)![el-scroll](https://github.com/0ragdoll0/share/blob/master/pics/20191012/11.png)

* **Scrollbar组件**  
Scrollbar组件可在element-ui的packages中找到，组件具体内容可在源码中查看：
![el-scroll2](74515F09A6F54E8FA6E23C410836F265)

* **Scrollbar组件主要属性** 
```
props: {
    native: Boolean,
    wrapStyle: {},
    wrapClass: {},
    viewClass: {},
    viewStyle: {},
    noresize: Boolean, // 如果 container 尺寸不会发生变化，最好设置它可以优化性能
    tag: {
      type: String,
      default: 'div'
    }
  },
```
![el-scroll4](https://github.com/0ragdoll0/share/blob/master/pics/20191012/12.png)

* **Scrollbar组件使用方法**  
1. 将需要添加滚动条的内容放在el-scrollbar组件标签内
2. 设置wrap-class对应样式的max-height
3. 实例：
链接：[el-scrollbar使用实例](https://codepen.io/0ragdoll0/pen/RwwraJe)
![el-scroll5](https://github.com/0ragdoll0/share/blob/master/pics/20191012/13.png)
4. 注意：不要改变wrap-class对应样式的padding。




