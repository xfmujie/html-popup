# Popup.js
超轻量网页弹窗Popup.js, 利用&lt;dialog>标签实现常用模态弹窗显示

![弹窗显示效果预览](https://ali.mu-jie.cc/img/popup-preview.png)

# 使用示例

## 引入Popup.js
在线引入
```html
<script src="https://ali.mu-jie.cc/js/Popup.js"></script>
```

本地引入(推荐)
```html
<script src="./Popup.js"></script>
```

## 实例化对象
```js
var popup = new Popup();
```

## 示例1: 提示弹窗
```js
popup.alert('这是一个提示弹窗');
```

## 示例2: 确认弹窗
```js
popup.confirm('是否确认？')
  .then(isEnter => {
    // 确定返回true  取消返回false
    if (isEnter) console.log('你点击了确定');
    else console.log('你点击了取消');
  });
```

## 示例3: 文本输入弹窗
```js
popup.prompt('请输入文本')
  .then(inputText => {
    // 确定返回输入的字符串  取消返回null
    if (inputText) console.log(`你输入的内容是: ${inputText}`);
    else console.log('你点击了取消');
  });
```

## 示例4: 消息弹窗
该方法有3个参数, 分别为**提示文字**, **自动关闭弹窗时间**(可选, 缺省值:1, 单位:秒), **回调函数**(可选), 详细用法见示例5
```js
popup.msg('这是一个消息弹窗 可设定时间自动关闭');
```

## 示例5: 消息弹窗的另一种用法
**使用场景**: 提示用户正在等待任务完成

**使用逻辑**: 当弹窗显示超时(超过自动关闭弹窗时间)时, 弹窗关闭并执行传入的回调函数; 如任务已在设定时间内完成, 调用.msgClose()方法关闭弹窗, 此时回调函数不会执行

**请求场景示例:**
```js
popup.msg('正在请求……', 5, function(){
  console.log('请求超时！');
});
fetch('https://api.mu-jie.cc/stray-birds')
  .then(Response => Response.text())
  .then(data => {
    // 请求完成，关闭弹窗
    popup.msgClose();
    console.log(data);
  });
```