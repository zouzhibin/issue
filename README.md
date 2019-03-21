## 今天在做项目中碰到一个问题，在iOS系统上 点击输入框，输入法正常弹出输入框，但当点击输入框完毕之后，会发现有一片空白的地方，也会导致输入框在的焦点聚不到输入框中

### 例如
![图片例子](./321.png)

- 这是因为在ios系统上键盘会往上顶
1、 需求是页面底部有一个按钮 点击弹出一个弹窗 呼出（input同理）弹起键盘，然后收起界面就上移（如下图）
```
$("input").blur(function(){
    $(window).scrollTop(0);
});

```
2、第二个需求就是弹窗出来的文本框（input等）弹起键盘底部文本框被键盘遮挡显示不出来
> 解决方案：核心思路还是控制一下滚动条
```
// 解决input获取焦点键盘遮挡
$('input,textarea').focus(function() {
        var Height =  document.body.clientHeight;
    	$(".popup-box").css({"position":"absolute","height":Height});
    	$(window).scrollTop(Height / 3);
}).blur(function(){
        $(".popup-box").css({"position":"fixed","height":"auto"});
})
```


