<!--
 * @Author: your name
 * @Date: 2020-07-31 20:45:36
 * @LastEditTime: 2020-08-10 22:56:02
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \electron-learn\README.md
-->

# 当前所在是 `master分支`

## 运行

1. `main.js`
2. 主进程创建渲染进程
3. 样式布局
4.

```js
// 您可以把应用程序其他的流程写在在此文件中
// 代码 也可以拆分成几个文件，然后用 require 导入。
// app 负责管理Electron 应用程序的生命周期 electron的引用
// BrowserWindow 创建窗口引用
const { app, BrowserWindow } = require("electron");

let mainWindow = null; // 主窗口
function createWindow() {
  // 创建浏览器窗口
  mainWindow = new BrowserWindow({
    // 设置打开的窗口大小
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
  });

  // 加载index.html文件  加载哪个页面
  mainWindow.loadFile("index.html");
  // 打开开发者工具
  // win.webContents.openDevTools();
}

// Electron会在初始化完成并且准备好创建浏览器窗口时调用这个方法
// 部分 API 在 ready 事件触发后才能使用。
app.whenReady().then(createWindow);

//当所有窗口都被关闭后退出
app.on("window-all-closed", () => {
  // 在 macOS 上，除非用户用 Cmd + Q 确定地退出，
  // 否则绝大部分应用及其菜单栏会保持激活。
  if (process.platform !== "darwin") {
    app.quit();
  }
});

app.on("activate", () => {
  // 在macOS上，当单击dock图标并且没有其他窗口打开时，
  // 通常在应用程序中重新创建一个窗口。
  if (BrowserWindow.getAllWindows().length === 0) {
    createWindow();
  }
});

app.on("ready", () => {
  require("./main/menu");
});
```

## 调试

```json
"scripts": {
    "start": "electron .",
    "inspect": "electron --inspect=1212",
    "packager": "electron-packager ./ electron-learn --all --out ./outApp  --overwrite --icon=./app/img/icon/icon.ico"
  },
```
