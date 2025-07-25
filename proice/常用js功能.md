---
icon: screwdriver-wrench
permalink: /codeEssence/tenjss.html
pageInfo: ["Author", "Date", "Original", "Date", "Word"]
breadcrumbIcon: share
index: true
sticky: true
date: 2025-02-09
category: + 常用js代码
tag: + 生成随机颜色
  + 数组重排序
  + 复制到剪切板
  + 检测暗色主题
  + 滚动到顶部 
  + 检测元素是否在屏幕中
  + 检测设备
  + 从 URL 中获取参数
  + 等待函数
star: true
---
# 常用js代码

## 生成随机颜色

你的网站是否需要生成随机颜色？下面一行代码就可以实现。

```javascript
const generateRandomHexColor = () => `#${Math.floor(Math.random() * 0xffffff).toString(16)}`

console.log(generateRandomHexColor())
```

## 数组重排序

对数组的元素进行重新排序是一项非常重要的技巧，但是原生 Array 中并没有这项功能。

```javascript
const shuffle = (arr) => arr.sort(() => Math.random() - 0.5)

const arr = [1, 2, 3, 4, 5]
console.log(shuffle(arr))
```

## 复制到剪切板

复制到剪切板是一项非常实用且能够提高用户便利性的功能。

```javascript
const copyToClipboard = (text) => navigator.clipboard && navigator.clipboard.writeText && navigator.clipboard.writeText(text)

copyToClipboard("Hello World!")
```

## 检测暗色主题

暗色主题日益普及，很多用的都会在设备中启用案模式，我们将应用程序切换到暗色主题可以提高用户体验度。

```javascript
const isDarkMode = () => window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches;

console.log(isDarkMode())
```

## 滚动到顶部

将元素滚动到顶部最简单的方法是使用 scrollIntoView。设置 block 为 start 可以滚动到顶部；设置 behavior 为 smooth 可以开启平滑滚动。

```javascript
const scrollToTop = (element) => 
  element.scrollIntoView({ behavior: "smooth", block: "start" });
```

## 滚动到底部

与滚动到顶部一样，滚动到底部只需要设置 block 为 end 即可。

```javascript
const scrollToBottom = (element) => 
  element.scrollIntoView({ behavior: "smooth", block: "end" });
```

## 检测元素是否在屏幕中

检查元素是否在窗口中最好的方法是使用 IntersectionObserver。

```javascript
const callback = (entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      // `entry.target` is the dom element
      console.log(`${entry.target.id} is visible`);
    }
  });
};

const options = {
  threshold: 1.0,
};
const observer = new IntersectionObserver(callback, options);
const btn = document.getElementById("btn");
const bottomBtn = document.getElementById("bottom-btn");
observer.observe(btn);
observer.observe(bottomBtn);
```

## 检测设备

使用 navigator.userAgent 来检测网站运行在哪种平台设备上。

```javascript
const detectDeviceType = () =>
  /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
    navigator.userAgent
  ) ? "Mobile" : "Desktop";

console.log(detectDeviceType());
```

## 隐藏元素

我们可以将元素的 style.visibility 设置为 hidden，隐藏元素的可见性，但元素的空间仍然会被占用。如果设置元素的 style.display 为 none，会将元素从渲染流中删除。

```javascript
const hideElement = (el, removeFromFlow = false) => {
  removeFromFlow ? (el.style.display = 'none')
  : (el.style.visibility = 'hidden')
}
```

## 从 URL 中获取参数

JavaScript 中有一个 URL 对象，通过它可以非常方便的获取 URL 中的参数。

```javascript
const getParamByUrl = (key) => {
  const url = new URL(location.href)
  return url.searchParams.get(key)
}
```

## 深拷贝对象

深拷贝对象非常简单，先将对象转换为字符串，再转换成对象即可。

```javascript
const deepCopy = obj => JSON.parse(JSON.stringify(obj))
```

除了利用 JSON 的 API，还有更新的深拷贝对象的 structuredClone API，但并不是在所有的浏览器中都支持。

```javascript
structuredClone(obj)
```

## 等待函数

JavaScript 提供了 setTimeout 函数，但是它并不返回 Promise 对象，所以我们没办法使用 async 作用在这个函数上，但是我们可以封装等待函数。

```javascript
const wait = (ms) => new Promise((resolve)=> setTimeout(resolve, ms))

const asyncFn = async () => {
  await wait(1000)
  console.log('等待异步函数执行结束')
}

asyncFn()
```
