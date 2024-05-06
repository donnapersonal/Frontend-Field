# script 标签 defer 与 async

![JS 加载.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e22634c4e40843448f67bafc980557e3~tplv-k3u1fbpfcp-watermark.image)

### 普通 script 标签

`JS` 可能会修改 `HTML` 和 `CSS`，因此 JS 的下载执行过程不能和 HTML/CSS 并行

`HTML` 解析过程中若碰到`外联的 JS`会**暂时中止 HTML 的解析流程**，等脚本下载和解析完成后再继续进行之前中断掉的 HTML 解析流程

这样就导致了 script 标签外联 JS 加载有这样的缺点：
- 影响整个页面效率，一旦网速不好整个网站将等待 JS 加载而不进行后续渲染
- 而由于中断了 HTML 解析流程，所以导致页面空白等，影响体验

```
以前的常用写法：将 script 标签写在 body 最后面，等 DOM 全部解析完成后才加载 JS，HTML5 标准有另一套异步加载 JS 的方法
```

### defer

在 `script` 标签的行间写一个 `defer=“defer”` 或直接写 `defer` 就可让这个 script 外联的 JS 变成异步加载

`HTML` 解析流程中若碰到外联 JS 时会**开辟新线程**来下载脚本，下载完成后不会立即解析，因此**不会阻塞 HTML 的解析流程**，等到 HTML 解析完毕后（不包括下载完里面的资源），`DOMContentLoaded` 事件调用前再进行相应脚本的执行解析
```
DOMContentLoaded 事件会等待 defer 的脚本执行完后才触发
```

这种方式可以在 script 标签里面写代码

注意：
- 该方法只有 `IE` 和一些高版本的 `firefox` 和 `chrome` 可以用
- `IE6` 和 `IE7` 的异步加载`最多只能有 2 个`，超过两个时必须等前两个加载完才会加载第三个
- **所有 defer 的 JS 代码都`保证按照顺序执行`**

### async

`async` 是 `asynchronous` 的缩写，是 `HTML5` 标准

`HTML` 解析流程中若碰到外联 JS 时会**开辟新线程**来下载脚本，下载完成后立即解析执行，且**解析流程会中断 HTML 解析流程**，等到脚本执行完成后才会继续进行之前中断掉的 HTML 解析流程

注意：
- 这种方法除了 `IE6 ～ IE8` 其他的浏览器都好用
- 该方式不能把代码写在 script 标签里，只能引用外部脚本（虽然标准是这么写的，但现在随着内核升级 async 的 script 标签里也可以写代码，在没有 src 情况下）
- **`async` 的 JS 代码`不能保证按顺序执行`，按照 `race` 的方式哪个脚本先下载完就先解析哪个脚本**

```
defer 和 async 这两个属性不能一起使用

若同时使用 async 和 defer 属性，defer 不起作用，浏览器行为由 async 属性决定
```

### 兼容性写法

**方法一**：直接写两个 script 标签，一个是 defer 一个是 async
```
缺陷：IE 高版本会加载两遍引起冲突；有些浏览器两个属性都没有，一个都加载不出来
```

**方法二**：通过动态添加 script 标签，W3C 的标准规定动态添加的 script 标签是异步的

`src` 部分的下载是`异步`的，不会阻塞后面的代码执行，即可一边把 script 插入到 DOM 中一边下载资源
```js
// 注：readyState 的 if-else 一定要写在 script.src = url 和 appendChild 之前
// script.readyState：这是一个属性，用来检查脚本的加载状态
// script.onreadystatechange：这是一个事件处理器，用于在 readyState 属性改变时触发
// 因电脑速度可能会很快，导致刚走到 src = url 部分就已经加载完毕资源, 此时 readyState 已变成 loaded，后面就不会触发 onreadystatechange 事件
// 若回调函数是写在需要加载进来的文件里的方法，需要把该方法放到匿名函数里，这样在语法解析时才不会因为函数未声明而报错

<script>
  function loadScript(url, callback) {
    const script = document.createElement("script");
    script.type = "text/javascript";
    if (script.readyState) { // IE 和高版本的 chrome、firefox
      script.onreadystatechange = function() {
        if (script.readyState == "loaded" || script.readyState === "complete") {
          script.onreadystatechange = null;
          callback && callback();
        }
      }
    } else {
      script.onload = function() { // safari chrome opera firefox
        callback && callback();
      }
    }
    script.src = url;
    document.body.appendChild(script);
  }
</script>


```