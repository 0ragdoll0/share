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
![usersnippets](D59834B1A5474DE2B19A5CB625BAC46F)
* 使用user snippets（主要功能为根据文件名动态生成script和style的src）
![usersnippets1](836772E43A9944A39226422848AC0756)

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
   * 如图：![folder](97B08A26B76245DC8A2FEDCC43EAA8BF)
3. 使用方法：在需要生成组件的路径，运行componentCreate/index.ts，输入组件名称
4. 修改模板方法：修改componentCreate/template中的文件即可
5. 获取地址：[componentCreate](https://github.com/0ragdoll0/tool.git)
6. 实例：
    * 路径转到项目的components文件夹，运行componentCreate/index.ts![1](0D2424A15C8F4D6DA7C3C0B8CCEDD88C)
    * 输入组件名，创建组件文件夹![2](5917EB3A8CD345668D71D0A726089684)
    * 生成模板文件![3](36B5EC9A3BBC4F0FA92334F9DE31E409)![4](20D432C99141469B9BBEDBE18C34C67B)![5](4A4B74D964A04A6C8C88F621D78405CE)![6](FA75F3F47083465F92AC551A787CF48D)
    
## elementui中的el-scrollbar
==el-scrollbar==在elementui的一些组件以及其官网中被使用，但在elementui官方文档中未提及。
如图：![el-scroll1](57DF2487127541DEAB821942D6165D81)![el-scroll](89EA00E48E4E439E857A56F23A0574D7)

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
![el-scroll4](65663BD720B64A36BD2A3DA62500C699)

* **Scrollbar组件使用方法**  
1. 将需要添加滚动条的内容放在el-scrollbar组件标签内
2. 设置wrap-class对应样式的max-height
3. 实例：
链接：[el-scrollbar使用实例](https://codepen.io/0ragdoll0/pen/RwwraJe)
![el-scroll5](6A77F37DF17E4EBFB5FED8B7D0A244DE)
4. 注意：不要改变wrap-class对应样式的padding。




