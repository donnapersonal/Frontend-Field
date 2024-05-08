# HTML 基础

### 一. 初识 HTML

#### HTML 概念

`HTML`: 全称是超文本标记语言 `(HyperText Markup Language)`，在网页中所有的文字图片和组织架构均由 HTML 来编写

`HTML` 并不是一种编程语言，它是一种计算机语言，其不具备像 c/c++/java 等编程语言中的变量或函数等东西，它仅仅由 `标签` 组成，如 `<html></html>`

`HTML` 就是`文档`，万维网的雏形是一个`文档共享系统`，而现在的万维网则是一个`资源共享的网络`，包括图片、多媒体等

> 万维网就是一个放大版的`文档共享系统`， HTML 的本质其实是文档（`document`）

#### 常见标签

**1. \<html\>\</html\>**

`根标签`，页面其他东西都要放在这个标签里面编写

可以在根标签里来加属性 `lang` 来告诉搜索引擎、爬虫网站使用什么语言，`zh-cmn`  是中文，`en` 是英文，一般二者一起写
```js
<html lang=”en, zh-cmn”>
```

**2. \<head\>\</head\>**

根标签次一级的标签

该标签中的内容主要是给 `浏览器` 看的，比如 `title` 用来设置页面的标题、meta、style 设置样式、link 外链 CSS 样式文件、设置移动端的页面显示大小、为网页被搜索时设置关键字等

`meta` 标签：由 `name` 和 `content` 两个属性定义，用来描述一个 **HTML 网⻚文档的属性**，如作者、日期和时间、网⻚描述、关键词、⻚面刷新等，除了一些 http 标准规定了一些 name 作为大家使用的共识，开发者也可以自定义 name

- `charset` 用于描述 HTML 文档的`编码形式`，英文正常显示但中文就会变成一堆乱码，这是由于浏览器不识别中文字符，可通过 \<meta\> 标签来设置编码格式
  ```js
  <meta charset = "utf-8">
  ```
  常见编码集主要有 `gbk`、`gb2312`、`unicode`、`utf-8`
  - `gb2312` 是国标 2312 条，可以识别简中日韩等亚洲语言
  - `gbk` 是国标扩展，可以识别繁体中文
  - `unicode` 是万国码 (unicode transformation format)，世界各国语言都包括在内，这个编码格式是公用的，可以识别所有的语言 
  - `utf-8` 是 `unicode` 的升级版本
  
- `http-equiv`，顾名思义相当于 http 的文件头作用，如下面的代码就可以设置 http 的缓存过期日期
  ```js
  // refresh：每 30s 刷新一次文档
  <meta http-equiv="refresh" content="30" />

  // X-UA-Compatible：告知浏览器以何种方式渲染界面，下面例子使用 `IE` 最新版本
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />

  // Cache-Control：请求和响应应遵循的缓存机制，可声明缓存的内容、修改过期时间，可多次声明
  // no-transform：不得对资源进行转换或转变
  // no-siteapp：禁止百度进行转码
  <meta http-equiv="Cache-Control" content="no-transform" />
  <meta http-equiv="Cache-Control" content="no-siteapp" />

  <meta http-equiv="expires" content="Wed, 20 Jun 2019 22:33:00 GMT">
  ```

- `viewport`，移动前端最熟悉不过，Web 开发人员可以控制视口的大小和比例 (`viewport` 即视区窗口，浏览器中显示网页的部分)
  ```js
  // width=device-width：将页面宽度设置为跟随屏幕宽度变化而变化
  // initial-scale=1.0：设置浏览器首次加载页面时的初始缩放比例（0.0 - 10.0 正数）
  // maximum-scale=1.0：允许用户缩放的最大比例（0.0 - 10.0 正数），必须大于等于 minimum-scale
  // minimum-scale=1.0：允许用户缩放的最小比例（0.0 - 10.0 正数），必须小于等于 maximum-scale
  // user-scalable=no：是否允许用户手动缩放（yes 或 no）
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
  ```

- `property`，可以让网页成为一个`富媒体对象`，同意网页内容被其他网站引用，同时在应用时不会只是一个链接，会提取相应的信息展现给用户
  ```js
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://..." />
  <meta property="og:site-name" content="TN's blog" />
  ```

- `apple-mobile-web-app-status-bar-style`，开发过 PWA 应用的开发者应该很熟悉，为了自定义评估工具栏的颜色
  ```js
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  ```

**3. \<body\>\</body\>**

根标签次一级的标签，`与 head 标签平级`，它是整个页面的主体部分，页面展示出来的内容一般都放在 body 标签下面

**4. \<div\>\</div\>\<span\>\</span\>**

它们是最常见的两个`结构化标签`，一般用来当做容器来盛放其他的标签

另外一个作用：用来为其里面的子元素设置样式，一般元素若某一条属性没有被开发者设置样式的话，它会自动继承父级元素的相应属性的样式

`span` 标签里多数情况下盛放`文字`或`小 icon`之类的

`div` 中间的文字会在这个 div 标签的边界处自动换行，即这个 div 标签圈定了一个范围，里面的文字或其他标签都默认在这个范围里面显示
> **在 div 中书写的是一串英文字符时，这串英文字符在 div 的边界处并没有换行而是一直显示下去，这是为什么呢？**
>
> 计算机会把每个汉字认出来是一个单独的单词，每个汉字都会默认地和其他汉字分隔开，但英文字母却不会默认地分隔开，因为计算机不知道多少个英文字母才算是一个单词，因此需要手动为其添加分隔符（即常用的空格），在这一串字符中间加几个空格，则被空格隔开的字符就会被当做是一个单词从而与其他的单词分隔开

空格的作用是当做分隔符来使用，并不是那种空白的一个格，怎么在 HTML 中写空白格呢？
- 这里用到 `编码集`，在书写 HTML 时很多特殊的符号是无法写出来的，这时只能用编码来让浏览器识别所想的符号，编码的格式是：`&编码;`
  
- 空格的编码就是 `&nbsp;`，当写多个 `&nbsp;` 时在页面中也就可以看到多个空白格
  
- 用来当做标签的尖括号 `<>` 也是无法正常通过符号来显示出来的，`<` 的编码是 `&lt;` 即 `less than` 的意思；`>` 的编码是 `&gt;` 即 `great than` 的意思
  
- `回车`也是属于分隔符，在 HTML 中回车是没有作用的，想要在网页上让文字显示出`回车换行`的效果，可以使用 `<br>` 标签，起作用就是**换行**
  > `W3C` 标准中提到 `<br>` 标签是空标签，意味着它没有结束标签，因此这是错误的 `<br></br>`
  >
  > 在 `XHTML` 中把结束标签放在开始标签中，即 `<br />`

```
- p 标签（独占一行，段落上下都会有一定的间隔距离）
- 标题标签 h1-h6、strong 标签（文字加粗放大且独占一行，h4 的默认大小是正常的文字大小，不过是加粗的）
- em 标签（文字变成斜体）
- del 标签（文字中间画一条横线，一般在打折时使用）
- address 标签（内容变成斜体并且独占一行）
```

**4. ol li**

`有序列表`，ol 是外面的列表框，li 是里面的子项且每个 li 子项前都会`带有序号`

ol 有个属性叫做 `type` 属性，这个属性的作用是用来设置每个子项前的显示内容，默认情况下按照数字来排序的

- `type=”a”`：序号是按照小写字母来排序
  
- `type 设置成 A`：按照大写字母来排序
  
- `设置成 i`：按照 i 的个数来排序（罗马数字）
  
- `设置成 I`：按照大写 I 的个数来排序

- 除此之外，设置成其他的属性均是错误的，而错误的情况下 ol 会按照默认的数字来排序

ol 的第二个属性 `reversed`，当给 ol 加上 `reversed=”reversed”` 时子项就会变成倒序来排列，这个属性直接写 reversed 也可，不过写完整才是规范的写法

ol 的第三个属性叫做 `start`，该属性的意思是让子项从第几个序号开始显示，当写 start=”2″ 时前面的序号就会变成 2、3、4 而不是默认的 1、2、3，字母也是同样的道理

**4. ul li**

`无序列表`，除了前面的序号都变成了点 `•` 外，其他的和有序列表基本一样

ul 同样有一个 `type` 属性，这个属性值设置的是每个子项前显示的符号的形式，默认的值是 `disc 圆点`

在使用 ul、li 标签时，一般会先设置 ul 的默认样式 `list-style: none`
> 无序列表一般用来当做`导航栏、里面的结构样式都一样`的部分，像淘宝等网页的导航栏就是用 ul、li 来写的

**5. a**

其有个必须写的属性 `href (hyperText reference)` 超文本链接，里面写的是地址

a 的英文单词是 `anchor` 锚点的意思，因此这个标签的作用主要有以下几点：

- `定点跳转指定的 id 的元素位置`，这个用法需`在 href 中写上 id 的值`，如 `<a href=”#clickme”></a>`，这会跳转到 id 是 clickme 的元素位置
  
- `超链接`，href 中写一个本地或网上的链接，如 [www.baidu.com](www.baidu.com)，点击时会跳转到这个网页
  
- `协议限定符`，href 中可`书写 JS 代码`，如： 
  ```
  href=”javascript:while(1){alert(‘你中毒了’)}”
  ```
  点击这个 a 标签后浏览器就会弹出对话框
  
  通常在移动端都用 a 标签来调用接口，如：href=”phoneto:12234512345″ 调用手机的拨号功能来拨打电话，像美团外卖就是用的这个功能

> a 标签默认的是`蓝色的字体`且`带有下划线`，在页面初始化时通常也习惯将 a 标签的颜色和下划线的默认属性都去掉

a 标签可`将图片作为链接下载`:
```js
<a href="../img/footer.png" download="../img/footer.png">下载图片</a>
```

**6. img**

`img` 标签即 image 图片，有个必备属性叫 `src –-> source`，该属性值是图片的地址，一般来说给 src 填写两种值：

- 网上链接
- 本地链接

本地链接分为两种：`相对地址` 和 `绝对地址`
> 相对地址中 `../` 是返回当前文件的上一层目录 ，`./` 是当前文件所在的目录
>
> 绝对地址通常是不用的，因为当文件上传到服务器上时，凡是用绝对地址写的链接统统都会失效的

`img` 标签还有两个属性:
- `alt`：该属性为图片设置占位符，即当图片因网速或链接错误等原因加载不出来时就会显示 alt 里面设置的值
  > 推荐在每个图像中都使用这个属性，原因：
  > - 即使图像无法显示，用户还是可以知道此处丢失的是什么信息
  > - 对于有视力障碍的人们来说，`alt` 属性通常是他们了解图像内容的唯一方式

  **`alt` 只能用在 `img`、`area`、`input`、`applet` 元素中**

- `title`：图片提示符，当鼠标移入图片时在鼠标旁边会出现一个小方块来显示这个 title 属性里面设置的值（`tooltip text`）
  > `title` 属性常与 `form` 及 `a` 元素一起使用，以提供关于输入格式和链接目标的信息，同时它也是 `abbr` 和 `acronym` 元素的必须属性
  >
  > `title` 属性是比较广泛使用的，可以用在除了`base`、`basefont`、`head`、`html`、`meta`、`param`、`script` 和 `title` 之外的所有标签，但**并不是必须的**

  `title` 属性的一个很好的用途：
  - 为链接添加描述性文字，特别是当链接本身并不是十分清楚的表达了链接的目的，这样就使得访问者知道那些链接将会带他们到什么地方，他们就不会加载一个可能完全不感兴趣的页面
  - 为图像提供额外的说明信息，如日期或其他非本质的信息

`srcset/sizes`

- 可以设计响应式图片，可以使用这两个新属性来提供更多额外的资源图像和提示，帮助浏览器选择正确的一个资源
- `srcset` 定义了允许浏览器选择的图像集以及每个图像的大小
- `sizes`  定义了一组媒体条件（如屏幕宽度）且指明当某些媒体条件为真时，什么样的图片尺寸是最佳选择

有了这些属性，浏览器会
- 查看设备宽度
- 检查 sizes 列表中哪个媒体条件是第一个为真
- 查看给予该媒体查询的槽大小
- 加载 srcset 列表中引用的最接近所选的槽大小的图像
```js
<img 
  src="clock-demo-thumb-200.png" 
  alt="Clock"
  srcset="clock-demo-thumb-200.png 200w, clock-demo-thumb-400.png 400w"
  sizes="(min-width: 600px) 200px, 50vw"
/>
```

**7. picture（追加）**

能起到上面 `srcset` 相似作用

通过包含`零或多个 <source> 元素`和`一个 <img> 元素`来为不同的显示/设备场景提供图像版本
> 浏览器会选择最匹配的子 `<source>` 元素，若没有匹配的就选择 `<img>` 元素的 src 属性中的 URL，然后所选图像呈现在 `<img>` 元素占据的空间中

`picture` 同样可以通过不同设备来匹配不同的图像资源
```js
<picture>
  <source 
    srcset="/media/examples/surfer-240-200.jpg" 
    media="(min-width: 800px)"
  >
  <img src="/media/examples/painted-hand-298-332.jpg" />  
</picture>
```

**8. 表单 form**

这个元素可实现前端和后台的数据交互，通过 `form` 表单向后台发送数据

数据都是由两部分组成的：`数据名` + `数据内容`
- `数据名`：需要在 `input` 标签里写一个 `name` 属性来告诉浏览器这个数据的名字是什么
- `数据内容`：给 `input` 标签设置的 `value` 属性的值

属性：
- `action`：填写服务器地址，意思是把数据传递到哪个服务器
- `method`：传输方法，通过什么方式来传输数据，一般填写的都是 `POST/GET` 两种中的一个，虽然有其他的方式但用的相对少
  
表单拥有的子元素：
- `input` 是一个单标签，不需要闭合，有个 `type` 属性，该属性值决定了 input 标签的类型是什么
  - `type="text"`，该 input 标签就是一个输入框，可以在里面输入文字信息
  - `type="password"`，该 input 标签就是一个密码框，在里面输入的文字信息会以隐藏形式展现 
  - `type="submit"`，该 input 标签是个提交按钮，点击该提交按钮会把整个表单数据发送到后台服务器
  - `type="radio"`，单选框，当给一个 input 设置 radio 的 type 后，它就会变成一个圆点，可点击选择这个圆点
    > 写很多单选框时它们似乎都可被选中并没有单选的作用，这是因为还没有为这一组单选框设置名字，当给几个 radio 都设置了同一个 name 时，它们就会变得只能选择一个单选框了

  - `type="checkbox"`：复选框，当 input 的 type 值设置成这个后和 radio 一样的道理，设置复选框的名字，可以同时选择很多的选项
  
  input 的 `readonly` 与 `disabled` 属性：
  - `disabled`：当 input 元素加载时禁用此元素，input 内容不会随着表单提交
  - `readonly`：规定输入字段为只读，input 内容会随着表单提交
  - 无论设置 readonly 还是 disabled，都能**通过 JS 脚本更改 input 的 value**

- `select` 下拉列表的标签
  - 下拉列表的 `name` 属性写在 `select` 标签上，里面 `option` 中间填写的内容就是`默认的数据`
  - 若给每个 option 都加一个 `value` 属性，则以 `value 的值作为传递的数据的值` (option 中间的文字不作为传递的数据值)
  - 下拉列表的默认选中的是`第一个选项`，若要改变默认选项则要添加的属性是 `selected="selected"`
    ```js
    <select>
      <option>山东</option>
      <option>黑龙江</option>
      <option>北京</option>
    </select>
    ```

**9. iframe**

`HTML 内联框架元素`，表示`嵌套的 browsing context` ([浏览上下文](https://developer.mozilla.org/en-US/docs/Glossary/browsing_context))，它能够将另一个 HTML 页面嵌入到当前页面中，每个嵌入的浏览上下文都有自己的会话和 `DOM` 树
- 被包含在 `window.frames` 伪数组（类数组对象）中
- 通过 `contentWindow` 访问 `iframe` 的 `window` 对象
- 通过 `contentDocument` 访问 `iframe` 的 `document` 元素，等同于 `contentWindow.document`
- 通过 `window.parent` 引用父窗口对象
- **这些脚本访问必须遵循同源策略**
> 注意：页面上的每个 `<iframe>` 都需要增加内存和其它计算资源，这是因为**每个浏览上下文都拥有完整的文档环境**，虽然理论上来说能够在代码中写出来无限多的 iframe，但最好还是先看看这么做会不会导致某些性能问题

优点：
- `iframe` 能够原封不动的把嵌入的网页展现出来
- 若有多个网页引用 `iframe`，只需修改 `iframe` 的内容就可实现调用的每个页面内容的更改，方便快捷
- 网页若为了统一风格，如头部和版本都是一样的，就可写成一个页面，用 `iframe` 来嵌套，可以增加代码的可重用（导航栏的应用）
- 

缺点：
- `iframe` 会阻塞主页面的 `onload` 事件
- 搜索引擎的检索程序无法解读这种页面，`不利于 SEO`
  > 使用 iframe 前需考虑这两个缺点，若需使用 iframe，最好是**通过 JS 动态给 iframe 添加 src 属性值**，这样可以绕开以上两个问题
- 产生多个页面，不易管理
- 页面样式调试麻烦，出现多个滚动条
- 增加服务器的 HTTP 请求，对于大型网站是不可取的
- 每个 `iframe` 对应一个页面，其多余的 `CSS` 和 `JS` 文件的载入会增加请求的开销
- 浏览器的后退按钮失效
- 小型的移动设备无法完全显示框架
- 不易打印

> `iframe` 现在已渐渐退出了前端开发的舞台
  
**10. label**

`label`标签：表示用户界面中某个元素的说明。增加命中区域，屏幕阅读器可以读出标签，使使用辅助技术的用户更容易理解输入哪些数据

`label` 标签用来定义表单控件间的关系，当用户选择该标签时浏览器会自动将焦点转到和标签相关的表单控件上
> 标签文本不仅与相应的文本输入元素在视觉上相关联，程序中也是如此。意味着当用户聚焦到这个表单输入元素时屏幕阅读器可以读出标签；点击关联的标签来聚焦或激活这个输入元素，就像直接点击输入元素一样，扩大了元素的可点击区域

`label` 标签的作用主要是用来绑定的，它有一个 `for` 属性，通过 `for` 属性写上要绑定的标签 `id`，就可把该 `label` 标签绑定到相对应的标签上
> 若在 JS 代码中要表示 label 标签的 for 属性，不能直接写 for，要写 `htmlFor`

```js
// 使用方法一
<label for="Name">Number:</label>
<input type="text" name="Name" id="Name" />

// 使用方法二
<label>Date:<input type="text" name="B" /></label>
```

注意：
- 关联标签的表单控件称为 `label` 标签的`已关联标签的控件`，一个 `input` 可以与多个 `label` 标签相关联
- 点击或轻触 `(tap)` 与表单控件相关联的 `<label>` 也可以触发关联控件的 `click` 事件
- 不要在 `label` 元素的内部放置可交互的元素，如 `a` 或 `button`，会更难触发相关联的输入元素
- 在 `label` 中放置标题元素会干扰许多辅助技术
- 若 `input` 元素声明了 `type=“button”` 和有效的 `value` 属性，则不需为其添加标签，添加标签可能会影响辅助技术理解这个输入按钮的语义

实例：
- 利用 `label` "模拟" `button` 来解决不同浏览器原生 `button` 样式不同的问题
  ```js
  <input type="button" id="btn" />
  <label for="btn">Button</label>
  
  <style>
    input[type='button'] {
      display: none;
    }
    label {
      display: inline-block;
      padding: 10px 20px;
      background: #456;
      color: #fff;
      cursor: pointer;
      box-shadow: 2px 2px 4px 0 rgba(0,0,0,.3);
      border-radius: 2px;
    }
  </style>
  ```

- 结合 `checkbox`、`radio` 表单元素实现纯 `CSS` 状态切换，如控制 `CSS` 动画播放和停止。下面是一部分代码[详细实例地址](https://codepen.io/mts123/pen/EzqdbM)
  ```js
  <input type="checkbox" id="controller" />
  <label class="icon" for="controller">
    <div class="play"></div>
    <div class="pause"></div>
  </label>
  <div class="animation"></div>
  
  <style>
    ...
    #controller:checked ~ .animation {
      animation-play-state: paused;
    }
    ...
  </style>
  ```

- `input` 的 `focus` 事件会触发锚点定位，可以利用 `label` 当触发器实现选项卡切换效果，下面代码选自张鑫旭《`CSS` 世界》，[实际效果链接](https://demo.cssworld.cn/6/4-3.php)
  ```js
  <div class="box">
    <div class="list"><input id="one" readonly>1</div>
    <div class="list"><input id="two" readonly>2</div>
    <div class="list"><input id="three" readonly>3</div>
    <div class="list"><input id="four" readonly>4</div>
  </div>
  <div class="link">
    <label class="click" for="one">1</label>
    <label class="click" for="two">2</label>
    <label class="click" for="three">3</label>
    <label class="click" for="four">4</label>
  </div>
  
  .box {
    width: 20em;
    height: 10em;
    border: 1px solid #ddd;
    overflow: hidden;
  }
  .list {
    height: 100%;
    background: #ddd;
    text-align: center;
    position: relative;
  }
  .list > input { 
    position: absolute; top:0; 
    height: 100%; width: 1px;
    border:0; padding: 0; margin: 0;
    clip: rect(0 0 0 0);
  } 
  ```

- 还有一个基于 `radio` 的实例：[摩斯密码键盘](https://codepen.io/mts123/pen/vqpQvR)

**11. script**

详见 [script 标签 defer 与 async](https://github.com/donnapersonal/Some-Field/blob/main/contents/html/script_defer_async.md)

#### 标签的分类

行级/内联/行内元素 `display: inline`，这一类元素的特点是：
- 不沾满整行，元素所占空间完全由内容所控制
- 不可以改变宽高
- 标签代表有：`a/em/br/select/span/strong`
  
块级元素 `display: block`，这一类元素的特点是：
- 占满整行，无论内容多还是少
- 可以改变宽高
- 标签代表有：`div/address/form/h1-h6/p/ul/ol/li/table`
  
第三种标签 `display: inline-block`，这类标签既不属于行级元素也不属于块级元素，它们既不独占一行，又可以随意改变宽高，如 `<img> <input>` 标签

空元素：`<br/>、<hr/>、<img/>、<input/>、<link/>、<meta/>`

块级元素和行内元素的区别总结：
- 默认情况下，行内元素不会以新的一行开始，而块级元素会新起一行
  ```js
  <span style="background: #1e7e34">行内元素</span>
  <span style="background: #1e7e34">行内元素</span>
  <span style="background: #1e7e34">行内元素</span>
  <div style="background: #bbb">块级元素</div>
  <div style="background: #bbb">块级元素</div>
  <div style="background: #bbb">块级元素</div>
  ```
  ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/396276fd1d4647c085f7d4154c547e21~tplv-k3u1fbpfcp-watermark.image?)

  当行内元素在一行内排不下时才会换行，且其宽度随着元素的内容而变化；块级元素则宽度自动填满其父元素宽度

- 块级元素可以设置 `width`、`height` 属性，注意：块级元素即使设置了宽度，仍然是独占一行的；而行内元素设置 `width`、`height` 无效
  ```js
  <span style="background: #1e7e34; width: 200px; height: 200px;">行内元素</span>
  <span style="background: #1e7e34; width: 200px; height: 200px;">行内元素</span>
  <div style="background: #bbb; width: 100px; height: 50px;">块级元素</div>
  <div style="background: #bbb; width: 100px; height: 50px;">块级元素</div>
  ```
  ![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ca910403ecc2413a911e64b2e333b2aa~tplv-k3u1fbpfcp-watermark.image?)

- 块级元素可以设置 `margin`、`padding`；而行内元素水平方向的 `margin-left/margin-right`、`padding-right/padding-left` 都产生边距效果，但竖直方向的 `margin-top/margin-bottom`、`padding-top/padding-bottom` 均不会产生边距效果（即水平方向有效，竖直方向无效）
   ```js
  <span style="background: #1e7e34;">行内元素</span>
  <span style="background: #1e7e34; padding-top: 20px;">行内元素</span>
  <div style="background: #bbb; padding-top: 20px;">块级元素</div>
  ```
  ![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c241413e862f4bb082ec85dfce8757f8~tplv-k3u1fbpfcp-watermark.image?)

  > 给行内元素设置上下 `margin` 不会生效，设置上下 `padding` 会生效，但不会撑开父元素，相当于没有效果

- 块级元素可以包含块级元素和行内元素；行内元素不能包含块级元素。如：在 `div` 标签中包含 `span` 标签很常见，而 `span` 标签内包含 `div` 标签是不不被允许的

- 设置居中
  
  - 行内元素要想设置水平居中，只需 `text-align` 属性即可，这里设置的 `text-align` 是设置在外层 `div` 中，因为上面讲了行内元素设置宽高是无效的，所以需要居中的其实是将块级元素中的行内元素居中；而块级元素要想设置水平居中有很多方式，如设置 `margin` 即可
    ```js
    // 行内元素
    div {
      text-align: center; // div 中的行内元素均会水平居中
    }
  
    // 块级元素
    margin: 0 auto;
    ```
  - 行内元素设置垂直居中，设置外层行高为行内元素的高度即可；而块级元素要先设置外层 `div` 的高度，然后设置内层块级元素的样式，当然还有其他方法
    ```js
    // 行内元素
    hight: 30px;
    line-height: 30px;
    
    // 块级元素
    margin: 0 auto;
    hight: 30px;
    line-height: 30px;
    ```

### 二. src 和 href 的区别

`src` 是指向外部资源的位置，指向的内容会嵌入到文档中当前标签所在的位置
- 在请求 `src` 资源时会将其指向的资源下载并应用到文档内，如 JS 脚本、img 图片、frame 等元素
- 当浏览器解析到该元素时会`暂停其他资源的下载和处理`，直到将该资源加载、编译、执行完毕，所以一般 JS 脚本会放在底部而不是头部

`href` 是指向网络资源所在位置(的超链接)，用来建立和当前元素或文档之间的连接，当浏览器识别到它指向的文件时就会`并行下载资源`，不会停止对当前文档的处理

> 浏览器解析 `href` 不会阻塞对文档的处理（这就是官方建议使用 `link` 引入 `CSS` 而不是使用 `@import` 的原因）

### 三. HTML 语义化

`HTML5` 的核心思想就是`语义`，不管是什么标签就看表达的意思而不是看展现效果

`语义化`是指根据`内容结构化（内容语义化）`来`选择合适的标签（代码语义化）`，让⻚面具有`良好的结构与含义`，如 `<p>` 标签就代表段落， `<article>` 代表正文内容等

语义化的优点：
- 增强了可读性、减少差异化，方便团队开发和维护，与 CSS3 的关系更和谐
- 有利于 SEO，改进搜索引擎的优化，爬虫依赖`标签`来确定关键词的权重，因此可以和搜索引擎建立良好的沟通，帮助爬虫抓取更多的有效信息
- 在没有 CSS 的情况下，页面也能呈现出很好的内容结构、代码结构
- 一般来说可以`让 HTML 文件更小`
- 方便其他设备解析，如屏幕阅读器、盲人阅读器、移动设备等，以有意义的方式来渲染页面，（盲人）会根据结构来读页面
- 提升用户体验，如 `title` 和 `alt` 可以用于解释名称或解释图片信息，以及 `label` 标签的灵活运用

> 这对于简书、知乎这种富文本类的应用很重要，语义化对于其网站的内容传播有很大的帮助，但对于功能性的 web 软件的重要性大打折扣，如一个按钮、Skeleton 这种组件根本没有对应的语义，也不需要什么 SEO

让 `IE8` 支持 `HTML5`
- HTML5 是 HTML 最新的修订版本，于 2014 年 10 月由万维网联盟（W3C）完成标准制定，而 IE8 面世时间为 2009 年 3 月 19 日，时间相差如此之大，所以 IE8 作为较古老的浏览器不支持 HTML5 引入的语义化标签，如 header、nav、menu、section、article 等
  
- 虽然默认不支持，但可通过 `JS` 使用 `document.createElement` 来“欺骗” IE 的 CSS 引擎，让它知道某个标签的存在，既然元素默认都不支持，就更没有相关默认的样式了，所以还要加上一些重置样式
  ```js
  article, aside, details, figcaption, figure, footer, header, hgroup, main, menu, nav, section, summary {
    display: block;
  }
  ```

- 可借助 `html5shiv.js` 让 IE8 支持更多的 HTML5 特性
  ```
  不只是 IE8，IE6-9、Safari 4.x（以及 Iphone3.x）、FireFox3.x 等对 HTML5 的支持都不完善，因此有个库 html5shiv.js 来统一处理（shiv 实际上是个拼写错误，应该为 shim，在机械工程的专业释义中为垫片，如给那些老旧的浏览器加个垫片，让它们基本能用）
  ```
  ```js
  <!--[if lt IE 9]>
  <script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
  <![endif]-->
  ```

> 为什么只写 `HTML`，在浏览器中不同标签也有不同的样式？
> 
> 因为各个浏览器都自带有相应标签的默认样式，为了方便在没有设定样式的情况下友好的展示页面

### 四. HTML、XHTML、XML

`HTML(超文本标记语言)`：在 `html4.0` 之前 HTML 先有实现再有标准，导致 HTML 非常混乱和松散

`XML(可扩展标记语言)`：主要用于`存储数据和结构`且`可扩展`
```
JSON 有相似的作用，但更加轻量和高效，所以 XML 现在市场越来越小了
```

`XHTML(可扩展超文本标记语言)`：基于上面两者而来，W3C 为了解决 HTML 混乱问题而生，并基于此诞生了 `HTML5`，开头加入 `<!DOCTYPE html>` 就是`标准模式`，不加就是兼容混乱的 `HTML`
- XHTML 元素必须合理嵌套
- 元素必须要有一个相应的结束标记
- 所有标签的元素和属性的名字都必须使用小写
- 必须有根元素
- 给所有属性赋一个值
- 所有的属性值必须用引号 "" 括起来
- 把所有 < 和 & 特殊符号用编码表示
- 不要在注释内容中使“--”
- 图片必须有说明文字等

### 五. Doctype

`DOCTYPE` 是 `HTML5` 标准网⻚声明，必须声明在 HTML 文档的第一行，用来告知浏览器的解析器用什么文档标准解析这个文档
> 不同的渲染模式会影响到浏览器对于 CSS 代码甚至 JS 脚本的解析

文档解析模式有：
- `标准模式（CSS1Compat）`：浏览器使用 W3C 的标准解析渲染⻚面，排版和 JS 运作模式都是以该浏览器支持的最高标准运行
- `怪异模式（BackCompat）`：使用浏览器自己的方式来解析执行代码，因为不同浏览器解析执行的方式不一样（**若没有声明 DOCTYPE，默认就是这个模式**）
> IE8 还有一种介乎于上述两者之间的近乎标准的模式，此模式下会实施一种表单元格尺寸的怪异行为(与 IE7 前的单元格布局方式一致)， 除此之外符合标准定义，基本淘汰了

浏览器标准模式/怪异模式的区别：
- 在怪异模式下，盒模型为怪异盒模型，其 `width` 和 `height` 包括 `padding` 和 `border`
- `inline` 元素和 `table-cell` 的垂直对齐方式默认值是 `bottom` 不是 `baseline`，因此在图片底部会出现几像素的缝隙空间
- 怪异模式下可以给 `inline` 元素定义宽高
- **元素中的字体**：`CSS` 中 `font` 属性都是可以继承的。怪异模式下对于 `table` 元素，某些元素不能从其他封装元素继承中得到字体属性，特别是 `font-size` 属性
- **元素的百分比高度**：当一个元素使用百分比高度时，标准模式下高度取决于内容变化；怪异模式下，百分比被准确应用
- **元素溢出处理**：标准模式下 `overflow` 取值默认值为 `visible`；怪异模式下这个溢出会被当作扩展 `box` 对待，即元素的大小由内容决定，溢出不会裁剪，元素框自动调整，包含溢出内容

浏览器解析时到底使用标准模式还是怪异模式，与网页中的 `DTD` 声明直接相关，DTD 声明定义了标准文档的类型（标准模式解析），会使浏览器使用相应的方式加载网页并显示，忽略 DTD 声明或在 DOCTYPE 前加入 XML 声明，将使网页进入怪异模式

`DOCTYPE` 三种标准模式写法如下，当还是 HTML 时一般用第三种，但现在一般直接用第一种写法（第一种是 HTML5 规范的标准写法）
```js
<!DOCTYPE html>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

**`HTML5` 为什么只需要写 `<!DOCTYPE html>` ？**

- `HTML5` 不基于 `SGML`，因此不需要对 DTD 进行引用，但需要 doctype 来规范浏览器的行为（让浏览器按照它们应该的方式来运行）
- 而 `HTML 4.01` 基于 `SGML`，所以需要对 DTD 进行引用才能告知浏览器文档所使用的文档类型
> SGML：标准通用标记语言（Standard Generalized Markup Language），是现时常用的超文本格式的最高层次标准，是可以定义标记语言的元语言，甚至可以定义不必采用<>的常规方式
> 
> 但由于它的复杂及非常强大的适应性因而难以普及。HTML 和 XML 同样派生于它：XML 可以被认为是它的一个子集，而 HTML 是它的一个应用，因此需用 DTD 来指定使用哪种规范  -- 维基百科
> 
> `DOCTYPE (Document Type Declaration)`用于声明文档类型和 `DTD (Document Type Definition)`规范， 确保不同浏览器以相同的方式解析文档，以及执行相同的渲染模式
> 
> `DTD` 就是一种标记符的语法规则，保证 SGML 和 XML 文档格式的合法性

### 六. HTML 5

#### 为 HTML5 建立的一些规则

- 新特性应该基于 HTML、CSS、DOM 以及 JS
- 减少对外部插件的需求，如 `Flash`
- 更优秀的错误处理（优化错误处理的功能点）
- 更多取代脚本的标记
- HTML5 应该独立于设备
- 开发进程应对公众透明

#### HTML5 新特性
- 新增语义化标签：`nav`、`header`、`footer`、`aside`、`section`、`article`...
- 音频、视频标签：`audio`、`video`
- 数据存储，对本地离线存储的更好的支持：`localStorage`、`sessionStorage`
- `canvas（画布）`、`geolocation（地理定位）`、`websocket（通信协议）`、`webworker`
- `input` 新增标签属性：`placeholder`、`autocomplete`、`autofocus`、`required`
- 新的表单控件，如 `calendar`、`date`、`time`、`email`、`url`、`search`
- history API：`go`、`forward`、`back`、`pushstate`

#### HTML5 新增标签

`Header`、`Footer`、`Article -> div`、`Section -> p`、`Nav`、 `Aside`、`Svg`、`Canvas`、`Audio`、`Video`、`自定义标签: 行级元素` 等

#### HTML5 新增属性

- `Contenteditable`：用户能否修改页面上的内容
- `Draggable`：支持拖放
- `Hidden`：隐藏
- `Contextmenu`：为元素设定快捷菜单
- `data-*`：自定义属性
  - HTML 的数据属性，用于**将数据储存于标准的 HTML 元素中作为额外信息**，可以通过 `JS` 访问并操作它来达到操作数据的目的
  - 这些属性集可通过对象的 `dataset` 属性获取，不支持该属性的浏览器可通过 `getAttribute` 方法获取
  - 注：`data-`后的以连字符分割的多个单词组成的属性，获取时使用`驼峰`风格，所有主流浏览器都支持 `data-*` 属性

#### 如何区分 HTML 和 HTML5？　

- `DOCTYPE` 声明、新增的结构元素、功能元素等

#### HTML5 的离线存储

在用户与因特网**失连时可以正常访问站点或应用**，在用户与因特网**连接时更新用户机器上的缓存文件**

使用离线缓存技术一般是为了让用户在：
- 离线状态也能正常访问
- 提高访问速度：已经缓存的资源加载得更快
- 减轻服务器响应压力：减少服务器负载，浏览器将只从服务器下载更改过的资源

**方案一：利用 `manifest` 属性实现 App Cache**
> - 一般具有 `window.applicationCache` 对象的浏览器才支持该特性
> - **注意**：manifest 文件需要配置正确的 `MIME-type`，即 `text/cache-manifest`，必须在 web 服务器上进行配置

原理：
- `HTML5` 的离线存储是基于一个新建的 `.appcache` 文件的缓存机制(不是存储技术)
- 通过该文件上的`解析清单`离线存储资源，这些资源就会像 `cookie` 一样被存了下来
- 之后当网络在处于离线状态下时浏览器会通过被离线缓存的数据进行页面展示

如何使用？
- `HTML` 头部加入一个 `manifest` 的属性
  ```js
  <html manifest="example.appcache"> 
    ...
  </html>
  ```

- 在 `example.manifest` 文件编写离线存储的资源，用于描述如何启动缓存
  ```js
  // 下面是一个完整缓存清单
  // 缓存清单：这些文件将在首次下载后进行缓存，无论用户何时与因特网断开连接，这些资源依然是可用的
  CACHE MANIFEST
  #v0.1 // 以 # 号开头的是注释，一般会在第二行写个版本号，用来在缓存的文件更新时，更新 manifest 以实现浏览器重新下载新的文件，这可以是版本号、时间戳或 md5 码等
  CACHE:
  index.html
  style.css
  logo.gif

  // 缓存白名单：表示在它下面列出来的资源只有在在线的情况下才能访问，他们不会被离线存储，所以在离线情况下无法使用这些资源 
  // 使用通配符”*”则会进入白名单的 open 状态，指示所有其他资源/文件都需要因特网连接
  // 这种状态下所有不在相关 Cache 区域出现的 url 都默认使用 HTTP 相关缓存头策略
  NETWORK:
  resourse/logo.png

  // 定了一个后备页面，当资源无法访问时，浏览器会使用该页面
  // 该段落的每条记录都列出两个 URI：第一个 URI 是资源，第二个是后备页 面，表示如果访问第一个资源失败，那么就使用第二个资源来替换他
  // 如下面这个文件表示的就是：若访问根目录下任何一个资源失败了则去访问 offline.html
  FALLBACK:
  / /offline.html
  ```
  > CACHE MANIFEST，NETWORK 和 FALLBACK 段落可以以任意顺序出现在缓存清单文件中，且每个段落可以在同一清单文件中出现多次

- `更新缓存`：缓存清单写后还需按时更新，否则一直使用缓存会导致界面内容老旧，更新缓存使用 `JS` 脚本来更新
  > 一旦应用被缓存，它就会保持缓存直到发生下列情况：
  > - 用户清空浏览器缓存
  > - manifest 文件被修改
  > - 通过 JS 操作

  在离线状态时操作 `window.applicationCache` 进行需求实现

注意事项：
- 浏览器对缓存数据的容量限制可能不太一样（某些浏览器设置的限制是每个站点  `5MB`）
- 若 `manifest` 文件，或内部列举的某一个文件不能正常下载，整个更新过程都将失败，浏览器继续全部使用老的缓存
- 引用 `manifest`的 `html` 必须与 `manifest` 文件同源，在同一个域下
- 在 `manifest` 中使用的相对路径，相对参照物为 `manifest` 文件
- `CACHE MANIFEST` 字符串应在第一行，且必不可少
- `FALLBACK` 中的资源必须和 `manifest` 文件同源
- 当一个资源被缓存后，该浏览器直接请求这个绝对路径也会访问缓存中的资源
- 站点中的其他页面即使没有设置 `manifest` 属性，请求的资源若在缓存中也从缓存中访问
- 当 `manifest` 文件发生改变时，资源请求本身也会触发更新

浏览器对 `HTML5` 的离线存储资源进行管理和加载
- 在线的情况下，浏览器发现 `HTML` 头部有 `manifest` 属性就会请求 manifest 文件
- 若是第一次访问 APP 则浏览器就会根据 manifest 文件的内容下载相应的资源且进行离线存储
- 已访问过 APP 且资源已离线存储了的，浏览器就会使用离线的资源加载页面，然后浏览器会**对比新旧 manifest 文件**，若文件没有发生改变则不做任何操作，若文件改变则会重新下载文件中的资源并进行离线存储
- 离线的情况下，览器就直接使用离线存储的资源

**方案二：Service Workers**

> 方案一看起来是个不错的方法，因为它可以很容易地指定需要离线缓存的资源。但它假定使用时会遵循诸多规则，若不严格遵循这些规则，它会把 APP 搞得一团糟，关于 APPCache 的更多详情，可查阅 Jake Archibald 的文章： [Application Cache is a Douchebag](https://link.csdn.net/?target=http%3A%2F%2Falistapart.com%2Farticle%2Fapplication-cache-is-a-douchebag)

使用的前提：
- 在支持 `service workers` 的浏览器中，很多特性可能默认是关闭的，若该浏览器支持该特性但相关代码不生效，需要先开启浏览器的相关设置。如 `chrom` 访问  `chrome://flags` 并开启 `experimental-web-platform-features`
- **此外出于页面安全考虑，`services workers` 要求必须在 `HTTPS` 协议下才能使用**

使用细节：
- `service worker` 有点类似于 `web worker`，代码也是在独立于主线程的`worker` 中运行
- 若 `'serviceWorker' in navigator` 说明浏览器支持 `Service Worker`，使用该特性一般需要：
  - **注册 worker**：`navigator.serviceWorker.register`
  - **安装和激活**：定义缓存文件，使用 `install` 事件进行安装监听，该事件会在注册之后触发
  - **劫持请求**：当页面使用到缓存的资源时会触发 `fetch` 事件，这时就可以告诉`Service worker` 该如何使用该资源，可以在请求发起前定义响应内容，这也是`Service Worker` 的精细之处，可以返回缓存到的资源也可以重新发起网络请求而不使用缓存，或网络不可用时返回一些准备好的意外页
  - **更新缓存**：简单的使用版本编号就可以控制缓存版本
  - **删除旧缓存**：还有个 `activate` 事件，当之前版本还在运行时，一般被用来做些会破坏它的事情，如摆脱旧版的缓存
  
> [使用 Service Worker](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API/Using_Service_Workers)  
> [借助Service Worker和cacheStorage缓存及离线开发 - 张鑫旭](https://www.zhangxinxu.com/wordpress/2017/07/service-worker-cachestorage-offline-develop/)

#### HTML5 的优点与缺点

优点：
- 网络标准统一，HTML5 本身是由 W3C 推荐出来的
- 多设备、跨平台
- 即时更新
- 提高可用性和改进用户的友好体验
- 有几个新的标签，这将有助于开发人员定义重要的内容
- 可以给站点带来更多的多媒体元素(视频和音频) ...

缺点：
- `安全`：之前 Firefox4 的 websocket 和透明代理的实现存在严重的安全问题，同时 webstorage、websocket 这样的功能很容易被黑客利用来盗取用户的信息和资料
- `完善性`：许多特性各浏览器的支持程度不一样
- `技术门槛`：HTML5 简化开发者工作的同时代表了有许多新的属性和 API 需要开发者学习，像 webworker、websocket、webstorage 等新特性，后台甚至浏览器原理的知识
- `性能`：某些平台上的引擎问题导致 HTML5 性能低下
- `浏览器兼容性`：最大缺点，IE9 以下浏览器几乎全军覆没

### 七. 优雅降级、渐进增强

`优雅降级`：
- Web 站点在所有新式浏览器中都能正常工作，若用户使用的是老式浏览器则代码会检查以确认它们是否能正常工作
- 由于 IE 独特的盒模型布局问题，针对不同版本的 IE 的 hack 实践过优雅降级，为那些无法支持功能的浏览器增加候选方案，使之**在旧式浏览器上以某种形式降级体验却不至于完全失效**

`渐进增强`：
- 从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能
- 向页面增加无害于基础浏览器的额外样式和功能，当浏览器支持时它们会自动地呈现出来并发挥作用

### 八. 对 WEB 标准及 W3C 的理解与认识

- 标签闭合
- 标签小写
- 不乱嵌套
- 提高搜索机器人搜索机率
- 使用外链 css 和 js 脚本
- 结构、行为、表现分离
- 文件下载与页面速度更快
- 内容能被更多的用户所访问
- 内容能被广泛的设备所访问
- 更少的代码和组件
- 容易维护、改版方便，不需要变动页面内容
- 提供打印版本而不需要复制内容
- 提高网站易用性

...











