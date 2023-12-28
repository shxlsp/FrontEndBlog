# Electron 是什么？

> Build cross-platform desktop apps with JavaScript, HTML, and CSS
>
> Electron 是一个使用 JavaScript、HTML 和 CSS 构建桌面应用程序的框架。 嵌入 [Chromium](https://www.chromium.org/) 和 [Node.js](https://nodejs.org/) 到 二进制的 Electron 允许您保持一个 JavaScript 代码代码库并创建 在 Windows 上运行的跨平台应用 macOS 和 Linux——不需要本地开发 经验。

# Electron 流程模型

Electron 是一个基于 Chromium 和 Node.js 的框架，它使用了一个称为 “渲染进程” 的独立进程来显示网页，而另一个进程则负责管理渲染进程，并与操作系统进行交互。

Electron 应用程序的主要流程如下：

1. 应用程序的主进程被启动，它负责创建浏览器窗口并加载你的应用。
2. 当你的应用加载后，Electron 会创建一个渲染进程来显示你的应用。
3. 你的应用被渲染到渲染进程中，并与操作系统进行交互。
4. 当你的应用不再需要时，Electron 会销毁渲染进程，并回收其所占用的内存。
   ![](https://github.com/shxlsp/FrontEndBlog/blob/master/Assets/Electron/electron进程图.jpeg)

# 主进程

提供 node 运行环境，能使用一切 node 相关的 api，但 node 版本根 electron 版本绑定。

electron 额外提供了一些系统层面的 api。例如：

- 本地文件系统
- 本地数据存储
- 本地网络
- 本地打印机
- 本地剪贴板
- 本地系统通知
- 本地计时器
- 本地进程间通信
- 本地用户界面
- 本地崩溃报告
- 本地崩溃恢复

## 加载一个网页

通过 BrowserWindowapi 可以创建出一个浏览器窗口，即渲染进程。

```js
// 在主进程中.
const { BrowserWindow } = require("electron");

const win = new BrowserWindow({ width: 800, height: 600 });

// Load a remote URL
win.loadURL("https://github.com");

// Or load a local HTML file
win.loadFile("index.html");
```

主进程可以为渲染进程提供 node 运行环境，但 electron 官方并不建议这么做。

> 为了方便开发，可以用完整的 Node.js 环境生成渲染器进程。 在历史上，这是默认的，但由于安全原因，这一功能已被禁用。

# 渲染进程

渲染进程是 Electron 应用程序的主要部分，它负责显示网页，并与操作系统进行交互。

渲染进程的主要工作是：

- 加载 HTML、CSS 和 JavaScript 文件
- 处理用户交互，如鼠标点击、键盘输入、窗口大小调整等
- 与主进程通信，如发送消息给主进程，或者从主进程接收消息

> 每个 Electron 应用都会为每个打开的 BrowserWindow ( 与每个网页嵌入 ) 生成一个单独的渲染器进程。 洽如其名，渲染器负责 渲染 网页内容。 所以实际上，运行于渲染器进程中的代码是须遵照网页标准的 (至少就目前使用的 Chromium 而言是如此) 。
>
> 因此，一个浏览器窗口中的所有的用户界面和应用功能，都应与您在网页开发上使用相同的工具和规范来进行攥写。
