# facebookPopTest
关于facebook开源动画库Pop的练习实例


### 运行效果图

<img src="https://github.com/wujunyang/facebookPopTest/blob/master/1.gif" width=400px height=600px></img>


### 一：关于Poping一些使用知识点

#### 5 使用Poping只要简单五步就可以实现

```objective-c
  // 1. Pick a Kind Of Animation //  POPBasicAnimation  POPSpringAnimation POPDecayAnimation
  POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];

  // 2. Decide weather you will animate a view property or layer property, Lets pick a View Property and pick kPOPViewFrame
  // View Properties - kPOPViewAlpha kPOPViewBackgroundColor kPOPViewBounds kPOPViewCenter kPOPViewFrame kPOPViewScaleXY kPOPViewSize
  // Layer Properties - kPOPLayerBackgroundColor kPOPLayerBounds kPOPLayerScaleXY kPOPLayerSize kPOPLayerOpacity kPOPLayerPosition kPOPLayerPositionX kPOPLayerPositionY kPOPLayerRotation kPOPLayerBackgroundColor
  basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewFrame];

  // 3. Figure Out which of 3 ways to set toValue
   //  anim.toValue = @(1.0);
  //  anim.toValue =  [NSValue valueWithCGRect:CGRectMake(0, 0, 400, 400)];
  //  anim.toValue =  [NSValue valueWithCGSize:CGSizeMake(40, 40)];
  basicAnimation.toValue=[NSValue valueWithCGRect:CGRectMake(0, 0, 90, 190)];

  // 4. Create Name For Animation & Set Delegate
   basicAnimation.name=@"AnyAnimationNameYouWant";
   basicAnimation.delegate=self

  // 5. Add animation to View or Layer, we picked View so self.tableView and not layer which would have been self.tableView.layer
  [self.tableView pop_addAnimation:basicAnimation forKey:@"WhatEverNameYouWant"];
```



#### Step 1 Pick Kind of Animation


### POPBasicAnimation
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionLinear];
// kCAMediaTimingFunctionLinear  kCAMediaTimingFunctionEaseIn  kCAMediaTimingFunctionEaseOut  kCAMediaTimingFunctionEaseInEaseOut
```

### POPSpringAnimation
```objective-c
POPSpringAnimation *springAnimation = [POPSpringAnimation animation];
springAnimation.velocity=@(1000);       // change of value units per second
springAnimation.springBounciness=14;    // value between 0-20 default at 4
springAnimation.springSpeed=3;     // value between 0-20 default at 4
```

### POPDecayAnimation
```objective-c
POPDecayAnimation *decayAnimation=[POPDecayAnimation animation];
decayAnimation.velocity=@(233); //change of value units per second
decayAnimation.deceleration=.833; //range of 0 to 1
```

### Example
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
```


#### Step 2 Decide if you will animate a view property or layer property

### View Properties
##### Alpha - kPOPViewAlpha
##### Color - kPOPViewBackgroundColor
##### Size - kPOPViewBounds
##### Center - kPOPViewCenter
##### Location & Size - kPOPViewFrame
##### Size - kPOPViewScaleXY
##### Size(Scale) - kPOPViewSize


### Layer Properties
##### Color - kPOPLayerBackgroundColor
##### Size - kPOPLayerBounds
##### Size - kPOPLayerScaleXY
##### Size - kPOPLayerSize
##### Opacity - kPOPLayerOpacity
##### Position - kPOPLayerPosition
##### X Position - kPOPLayerPositionX
##### Y Position - kPOPLayerPositionY
##### Rotation - kPOPLayerRotation
##### Color - kPOPLayerBackgroundColor

### Example
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
```

#### Note: Works on any Layer property or any object that inherits from UIView such as UIToolbar | UIPickerView | UIDatePicker | UIScrollView |  UITextView | UIImageView | UITableViewCell | UIStepper | UIProgressView | UIActivityIndicatorView | UISwitch | UISlider | UITextField | UISegmentedControl | UIButton | UIView | UITableView



#### Step 3 Find your property below then add and set .toValue

### View Properties
##### Alpha - kPOPViewAlpha
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewAlpha];
basicAnimation.toValue= @(0); // scale from 0 to 1
```

##### Color - kPOPViewBackgroundColor
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPViewBackgroundColor];
basicAnimation.toValue= [UIColor redColor];
```

##### Size - kPOPViewBounds
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewBounds];
basicAnimation.toValue=[NSValue valueWithCGRect:CGRectMake(0, 0, 90, 190)]; //first 2 values dont matter
```

##### Center - kPOPViewCenter
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewCenter];
basicAnimation.toValue=[NSValue valueWithCGPoint:CGPointMake(200, 200)];
```

##### Location & Size - kPOPViewFrame
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewFrame];
basicAnimation.toValue=[NSValue valueWithCGRect:CGRectMake(140, 140, 140, 140)];
```

##### Size - kPOPViewScaleXY
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewScaleXY];
basicAnimation.toValue=[NSValue valueWithCGSize:CGSizeMake(3, 2)];
```

##### Size(Scale) - kPOPViewSize
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewSize];
basicAnimation.toValue=[NSValue valueWithCGSize:CGSizeMake(30, 200)];
```
### Layer Properties
##### Color - kPOPLayerBackgroundColor
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerBackgroundColor];
basicAnimation.toValue= [UIColor redColor];
```

##### Size - kPOPLayerBounds
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerBounds];
basicAnimation.toValue= [NSValue valueWithCGRect:CGRectMake(0, 0, 90, 90)]; //first 2 values dont matter
```

##### Size - kPOPLayerScaleXY
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerScaleXY];
basicAnimation.toValue= [NSValue valueWithCGSize:CGSizeMake(2, 1)];//increases width and height scales
```

##### Size - kPOPLayerSize
```objective-c
POPBasicAnimation *basicAnimation = [POPBasicAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPLayerSize];
basicAnimation.toValue= [NSValue valueWithCGSize:CGSizeMake(200, 200)];
```

##### Opacity - kPOPLayerOpacity
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerOpacity];
basicAnimation.toValue = @(0);
```

##### Position - kPOPLayerPosition
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerPosition];
basicAnimation.toValue= [NSValue valueWithCGRect:CGRectMake(130, 130, 0, 0)];//last 2 values dont matter
```

##### X Position - kPOPLayerPositionX
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerPositionX];
basicAnimation.toValue= @(240);
```

##### Y Position - kPOPLayerPositionY
```objective-c
POPSpringAnimation *anim = [POPSpringAnimation animation];
anim.property=[POPAnimatableProperty propertyWithName:kPOPLayerPositionY];
anim.toValue = @(320);
```

##### Rotation - kPOPLayerRotation
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerRotation];
basicAnimation.toValue= @(M_PI/4); //2 M_PI is an entire rotation
```
#### Note: Property Changes work for all 3 animation types - POPBasicAnimation POPSpringAnimation POPDecayAnimation
### Example
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName: kPOPLayerRotation];
basicAnimation.toValue= @(M_PI/4); //2 M_PI is an entire rotation
```

#### Step 4 Create Name & Delegate For Animation
```objective-c
basicAnimation.name=@"WhatEverAnimationNameYouWant";
basicAnimation.delegate=self;
```
##### Declare Delegate Protocol `<POPAnimatorDelegate>`

### Delegate Methods
`
<POPAnimatorDelegate>
`
```objective-c
- (void)pop_animationDidStart:(POPAnimation *)anim;
```
```objective-c
- (void)pop_animationDidStop:(POPAnimation *)anim finished:(BOOL)finished;
```
```objective-c
- (void)pop_animationDidReachToValue:(POPAnimation *)anim;
```


### Example
```objective-c
POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewFrame];
basicAnimation.toValue=[NSValue valueWithCGRect:CGRectMake(0, 0, 90, 190)];
basicAnimation.name=@"WhatEverAnimationNameYouWant";
basicAnimation.delegate=self;
```


#### Step 5 Add animation to View
```objective-c
 [self.tableView pop_addAnimation:basicAnimation forKey:@"WhatEverNameYouWant"];
```
### Example
```objective-c
  POPSpringAnimation *basicAnimation = [POPSpringAnimation animation];
  basicAnimation.property = [POPAnimatableProperty propertyWithName:kPOPViewFrame];
  basicAnimation.toValue=[NSValue valueWithCGRect:CGRectMake(0, 0, 90, 190)];
  basicAnimation.name=@"SomeAnimationNameYouChoose";
  basicAnimation.delegate=self;
  [self.tableView pop_addAnimation:basicAnimation forKey:@"WhatEverNameYouWant"];
```

### 二：关于Poping一些注意点

1：组动画的效果实现，同时写就会同时进行，就有组的效果

```objective-c
    POPSpringAnimation *Annimation1 = [POPSpringAnimation animationWithPropertyNamed:kPOPViewScaleXY];
    Annimation1.springSpeed = 40.0f;
    Annimation1.springBounciness = 30.0f;
    Annimation1.fromValue = [NSValue valueWithCGPoint:CGPointMake(0.3, 0.3)];
    Annimation1.toValue = [NSValue valueWithCGPoint:CGPointMake(1, 1)];
    POPSpringAnimation *Annimation2 = [POPSpringAnimation animationWithPropertyNamed:kPOPViewCenter];
    Annimation2.springSpeed = 40.0f;
    Annimation1.springBounciness = 30.0f;
    Annimation2.toValue = [NSValue valueWithCGPoint:CGPointMake(100, 100)];
    [_Subview pop_addAnimation:Annimation1 forKey:@"Scale"];
    [_Subview pop_addAnimation:Annimation2 forKey:@"Move"];
```

2：关于连续动画的效果

```objective-c
 anim.completionBlock = ^(POPAnimation *anim, BOOL finished) { 
  if (finished) {
     NSLog(@"Animation finished!");
     //加入新的动画
     }};
```

3：可以实现委托POPAnimatorDelegate关于动画前后的一些操作处理

```objective-c
- (void)pop_animationDidStart:(POPAnimation *)anim;
```
```objective-c
- (void)pop_animationDidStop:(POPAnimation *)anim finished:(BOOL)finished;
```
```objective-c
- (void)pop_animationDidReachToValue:(POPAnimation *)anim;
```

4：POPBasicAnimation提供四种timingfunction(很熟悉，对不对? 就是Core Animation中那些)

```objective-c

kCAMediaTimingFunctionLinear

kCAMediaTimingFunctionEaseIn

kCAMediaTimingFunctionEaseOut

kCAMediaTimingFunctionEaseInEaseOut

```


<img src="https://github.com/wujunyang/facebookPopTest/blob/master/2.png" width=500px height=400px></img>

<img src="https://github.com/wujunyang/facebookPopTest/blob/master/3.png" width=500px height=400px></img>

<img src="https://github.com/wujunyang/facebookPopTest/blob/master/4.png" width=500px height=400px></img>

<img src="https://github.com/wujunyang/facebookPopTest/blob/master/5.png" width=500px height=400px></img>