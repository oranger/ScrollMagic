在safari浏览器中，当地址栏隐藏或显示时，会造成trigger的跳动，体验效果不好。

经测试发现trigger是取了可视高度的百分比，这个百分比是通过triggerHook来进行设置（0-1），我们可以修改代码，将这个地方修改为值是0-1时按照百分比，大于1时设置为绝对值，

//将代码
val = Math.max(0, Math.min(parseFloat(val), 1)); 
改为
val = Math.max(0, parseFloat(val)); 


同时 updateScrollOffset 方法中
_scrollOffset.start -= _controller.info("size") * _options.triggerHook;

修改为

if( _options.triggerHook <= 1) {
   _scrollOffset.start -= _controller.info("size") * _options.triggerHook;
}
else{
  _scrollOffset.start -= _options.triggerHook;
}

这样就可以了，获取页面高度，直接设置为定数就可以了。




如果想查看辅助线需要将debug.addIndicators.js中的this._indicators.updateTriggerGroupPositions方法

该行
pos = group.triggerHook * Controller.info("size");

修改为
if(group.triggerHook>1){
   pos = group.triggerHook;
}
else{
   pos = group.triggerHook * Controller.info("size");
}

