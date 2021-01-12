On the safari browser of iPhone, when you slide up and down, the browser address bar will show and hide, which will cause element jitter

Because trigger hook is set to 0.5 by default, which is the center of the screen, the change of page height will cause the change of starting position

We can set triggerhook as a percentage or a fixed value. When it is 0-1, it is a percentage. When it is greater than 1, it is a fixed value

1. On triggerHook function, 

val = Math.max(0, Math.min(parseFloat(val), 1)); //  make sure its betweeen 0 and 1

=>

val = Math.max(0, parseFloat(val));//  make sure its greater than 0


2. On updateScrollOffset

if (_controller && _options.triggerElement) {
// take away triggerHook portion to get relative to top
_scrollOffset.start -= _controller.info("size") * _options.triggerHook;
}

=>

if (_controller && _options.triggerElement) {
  // take away triggerHook portion to get relative to top
  if( _options.triggerHook <= 1) {
     _scrollOffset.start -= _controller.info("size") * _options.triggerHook;
   }
   else
   {
     _scrollOffset.start -= _options.triggerHook;
    }
}






