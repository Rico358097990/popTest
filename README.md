# popTest

这是facebook开放在github上面的网址：https://github.com/facebook/pop.   介绍了安装方法和一些基本用法和类的介绍，

官方的不全，所以我在这个里面放了一个例子，别人写的，代码非常全面，我自己下载下来后又新了pod，也没了黑边，还有和这个例子配套的讲解都在Zip文件里面。

pop最核心的代码：

-(void)performAnimation
{
  //移除layer上的所有动画

  [self.popCircle.layer pop_removeAllAnimations];

  //创建一个动画

  POPDecayAnimation *anim = [POPDecayAnimation animationWithPropertyNamed:self.animationType];

  //作者自己写的一个方法，配置动画的一些属性

  [PDAnimationManager decayObject:self.popCircle.layer configAnimation:anim WithType:self.animationType andAnimated:self.animated andVelocitySlider:self.velocitySlider];

  //这也是设置一个属性

  anim.deceleration = self.decelerationSlider.value;

  self.animated = !self.animated;

  //动画完成后继续调用此方法

  anim.completionBlock = ^(POPAnimation *anim, BOOL finished) {
    if (finished) {

     [self performAnimation];
    }
  };

  //必要的代码，key是描述这个动画的

  [self.popCircle.layer pop_addAnimation:anim forKey:@"Animation"];
}
