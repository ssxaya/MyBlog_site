---
title: 【功能测试】  0基础&快速使用BackStopJS
date: 2025-04-17 20:24:05
tags: [功能测试,学习]
categories: [学习]
excerpt: "backstopjs是一个基于 JavaScript (Node.js)语言的视觉回归测试工具，主要用于在应用程序的界面发生变化时进行自动化测试，它通过对比不同版本的网页截图来检测 UI 的视觉差异，帮助开发人员在页面的修改中发现潜在的视觉问题。"
---

# 0基础使用BackStopJS

如果你有一定基础、想快速使用backstopjs的话，请直接跳转到**快速启动**标题来获取最简洁的使用方式[待更新]

## Backstopjs是什么

backstopjs是一个基于 JavaScript (Node.js)语言的视觉回归测试工具，主要用于在应用程序的界面发生变化时进行自动化测试，它通过对比不同版本的网页截图来检测 UI 的视觉差异，帮助开发人员在页面的修改中发现潜在的视觉问题。

具体来说，它在运行时会捕获被测网页，并将这些截图与基准截图进行对比，若对比结果中有显著差异，BackstopJS 会将其标记出来，供开发人员检查。

<br>

## 安装&删除 Backstopjs

### 前置条件

首先系统需要下载Node.js，这样我们才能运行npm命令下载backstopjs，如果你不会下载，可以观看我的往期文章[待更新]

### 安装

随后，通过命令行（cmd，base等等）运行以下代码全局下载backstopjs工具

```cmd
npm install -g backstopjs
```

-g 代表global，会使得backstopjs被安装在全局的 `node_modules` 目录中，这样我们就能在任何目录下通过命令行直接运行该工具

如果你想让backstopjs只在当前项目安装，把上面代码的`-g`删掉就好

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_01.gif)

> 作者的安装过程

<br>

<br>

### 删除

想要删除全局下的backstopjs，只需要在`install`前加上`un`

```cmd
npm uninstall -g backstopjs
```

如果想要删除当前目录下的backstopjs，把上面代码的`-g`删掉就行

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_02.gif)

<br>

## 初始化工作环境

仅仅是下载工具是不行的，我们需要在合适的目录下构建配置文件

期间需要你cd（跳转）到符合你需要的目录下，例如我想在D:\prog\code\python\PycharmProjects\test03目录下来管理和使用backstopjs配置文件，那么我就需要

```cmd
cd /d D:\prog\code\python\PycharmProjects\test03
```

之后确保你在你需要的目录下后运行以下构建代码:

```cmd
backstop init
```

<br>

如果你在JetBrians或者vscode等等ide工具中，可以直接在ide的终端（内置控制台）下运行构建代码，因为 IDE 的终端通常会默认以当前打开的项目目录为起始路径），这样你就不需要手动切换目录去运行init指令了。

~~如果你想把目录放在项目目录的子目录下，那么还是需要跳转一下的()~~

> tips： 可以使用 ./ 来代替当前目录，../来代替父目录，可以连续使用多次跳转，例如../../，跳转到上上级目录

如果你的控制台出现如下提示便构建成功

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_03.png)

在构建代码后，你会发现你当前目录下多出如下文件夹

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_04.png)

<br>

## 修改配置文件

我们先不用管`backstop_data`文件夹，这是backstop的数据文件，我们先修改容易理解的配置文件`backstop.json`

backstop的配置文件是以json格式存储的，我们简易的了解一下json格式：
	json是一种轻量级的数据传输格式，很适合作为配置文件,而：
	`{"key"："value"}`
	则是一个最小的标准json单元，它由一个key（键）和一个value（值）组成，我们称之为键值对。
	其中，key是唯一的，如果key的值重复了，后面的key会把前面的key对应的value覆盖掉。并且key必须是字	符串、数字、布尔值（true/false）或 null。
	json还允许数组，即：
	`[value1,value2,value3]`
	这种形式的序列，而键值对的值和数组可以互相嵌套。

<br>

我们打开`backstop.json`，可以看到整体的代码：
```json
{
  "id": "backstop_default",
  "viewports": [
    {
      "label": "phone",
      "width": 320,
      "height": 480
    },
    {
      "label": "tablet",
      "width": 1024,
      "height": 768
    }
  ],
  "onBeforeScript": "puppet/onBefore.js",
  "onReadyScript": "puppet/onReady.js",
  "scenarios": [
    {
      "label": "BackstopJS Homepage",
      "cookiePath": "backstop_data/engine_scripts/cookies.json",
      "url": "https://garris.github.io/BackstopJS/",
      "referenceUrl": "",
      "readyEvent": "",
      "readySelector": "",
      "delay": 0,
      "hideSelectors": [],
      "removeSelectors": [],
      "hoverSelector": "",
      "clickSelector": "",
      "postInteractionWait": 0,
      "selectors": [],
      "selectorExpansion": true,
      "expect": 0,
      "misMatchThreshold" : 0.1,
      "requireSameDimensions": true
    }
  ],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "report": ["browser"],
  "engine": "puppeteer",
  "engineOptions": {
    "args": ["--no-sandbox"]
  },
  "asyncCaptureLimit": 5,
  "asyncCompareLimit": 50,
  "debug": false,
  "debugWindow": false
}

```

这么多配置文件，我们只需要修改其中一部分就足够让我们使用了。

<br>

### `"id": "backstop_default"` 

定义唯一标识符，默认为`backstop_default`
	会在运行后的测试报告上标注id的名字，并且作为配置文件的唯一标识符，命名的时候最好是能够通过名字看	到这个配置文件是做什么的，最重要的是一定要 **唯一**

<br>

### `"viewports": []`

定义测试时使用的设备屏幕分辨率，默认给出了"phone"和"tablet"两个设备的分辨率
这里的value是一个数组，每个代表一个设备的分辨率

```json
"viewports": [
    {
        "label": "设备名",
        "width": "宽度（像素）",
        "height": "高度（像素）"
    }
]
```

就算看不懂也没关系，json不是强制缩进的语言，因此可以把空格与回车删除，变成如下样子：

```json	
"viewports": [{"label": "设备名","width": "宽度（像素）","height": "高度（像素）"}]	
```

> 还是第一种的代码风格更便于程序员阅读和理解，因此要在理解键值对的基础上明白常用代码风格的样子

<br>

### `"onBeforeScript": "puppet/onBefore.js"`

在进行视觉回归测试前执行的js脚本路径。这通常用于设置环境、执行前置操作等

### `"onReadyScript": "puppet/onReady.js"`

在页面加载完成后执行的js脚本路径，通常用于页面状态准备好后的一些处理（例如动态内容加载完成后执行）

value对应的是backstop_data目录下的脚本路径，默认在backstop_data\puppet文件夹里

> 这两个配置文件是可以让工具知道你存放的js脚本位置的，不懂就不写，没有关系

<br>

### `"scenarios": []`

定义一系列场景（tests），每个场景代表一次浏览器交互及截图操作。

- `"label"`：tests的标签名字，起到辨别的作用
- `"cookiePath"`：存储和加载 cookie 的文件路径
- `"url"`：测试的网页地址
- `"referenceUrl"`：基准 URL（如果需要与另一个页面进行比较时）
- `"readyEvent"`：页面准备好的事件（如果需要特定的事件触发）
- `"readySelector"`：页面准备好的选择器（页面完全加载时的 DOM 元素选择器）
- `"delay"`：执行操作前的延迟时间（单位：毫秒）
- `"hideSelectors"`：在截图时需要隐藏的元素的 CSS 选择器数组
- `"removeSelectors"`：在截图时需要移除的元素的 CSS 选择器数组
- `"hoverSelector"`：鼠标悬停时需要作用的元素选择器
- `"clickSelector"`：点击时需要点击的元素选择器
- `"postInteractionWait"`：在交互操作后等待的时间（单位：毫秒）
- `"selectors"`：要截图的 DOM 元素的 CSS 选择器
- `"selectorExpansion"`：是否扩展元素选择器的范围。
- `"expect"`：截图期望匹配的像素数量
- `"misMatchThreshold"`：定义匹配的容差（数值越小越严格）
- `"requireSameDimensions"`：是否要求对比截图具有相同的尺寸

> 太多了看不懂没关系，在这么多配置选项里只需要注意`url`——你的被测网页地址，写入其中即可

### `"paths": []`

定义有关于测试流程的各种数据及文件的目录位置

- `"bitmaps_reference"`：存储基准截图的文件夹
- `"bitmaps_test"`：存储测试截图的文件夹
- `"engine_scripts"`：存储引擎脚本的文件夹
- `"html_report"`：存储 HTML 格式的测试报告的文件夹
- `"ci_report"`：存储持续集成报告的文件夹

> 太多了看不懂没关系( ~~好熟悉？~~，看不懂的话只需要关注`"bitmaps_reference"`与`"bitmaps_test"`，尤其是`"bitmaps_reference"`，它的意思是把你期望的ui页面的截图放入这个路径中（一般来说用户需求书里会有）

<br>

剩下的配置项就算不配置也不影响使用，看不懂的就不用管了

### `"report": []`

指定测试报告的格式和方式。此处设置为 `["browser"]`，表示生成浏览器格式的报告，其他选项还可以包括 `["json"]` 或 `["html"]`。

### `"engine": "puppeteer"`

指定使用的浏览器引擎，这里是 Puppeteer（基于 Chrome 的浏览器自动化工具）。也可以设置为 "playwright" 等其他引擎。

### `"engineOptions"`

为浏览器引擎传递额外的选项。这里使用 `args: ["--no-sandbox"]` 禁用沙盒模式，通常用于 CI 环境中的 Chrome 浏览器运行。

### `"asyncCaptureLimit": 5`

设置并发截图的限制数目。控制在同一时间内最多能够捕获的截图数量

### `"asyncCompareLimit": 50`

设置并发比较截图的限制数目。控制在同一时间内最多能够进行的截图比较数量

### `"debug": fals`

是否启用调试模式。设置为 `true` 会输出更多的调试信息

### `"debugWindow": false`

是否显示调试窗口。设置为 `true` 会显示浏览器窗口以便调试

<br>

## 测试的简单流程

我们了解了配置文件后，接下来我会以最少的操作完成一次对backstopjs工具的使用

模拟需求：

​	业务点：百度一下搜索页

​	预期ui页面：

<br>	![](https://img.ssxaya.fun/PicGo/posts/backstopjs_05.png)

​	像素： 3184x1680 （16:10笔记本3k分辨率全屏浏览器）

<br>

1. 我会修改`backstop.json`文件中的：
   
   `"viewports"` 被测分辨率符合用户需求的3184x1680 （第3行）

```json
 "viewports": 
 [
	{
  		"label": "3k",
  		"width": 3184,
  		"height": 1680
	}
],
```
​	"url" 被测页面的url：https://www.baidu.com/（第27行）

```
"url": "https://www.baidu.com/",
```

2. 在backstop_data目录下创建`bitmaps_reference`文件夹，用于存放用户需求书里的预期ui页面，并且把图片放入其中
3. 随后将控制台跳转到工具目录下后，运行`backstop test`指令开始测试
   等待一段时间后会自动跳出浏览器窗口，并展示有关的测试报告

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_07.png)

4. 修改图片名后，再次运行测试

![](https://img.ssxaya.fun/PicGo/posts/backstopjs_08.png)

<br>

可以发现这个测试failed了，原因是每次刷新页面百度页面的内容总会随机变化，导致两次测试内容不同

<br>

以上









