#Android性能优化最佳实践

###lint推荐的性能优化点：

1. handler的不良使用造成的内存泄漏。handler使用包裹了目标对象的一个弱引用，避免内存泄漏。
2. layout属性weight的不良使用，应该在weight的方向上设置尺寸为0dp。避免多次计算
3. view的绘制代码部分内存的不良分配，不要在ondraw方法中new新的对象
4. 布局嵌套，减少布局的层次结构。布局的内部view元素也不可以数量太多。移除useless的布局，使用textview的topdrawable替代原先的布局等。include、merge、viewstub标签的使用等。include布局重用，merge替换framelayout减少布局层次，viewstub布局的延迟加载。merge替换framelayout，当根布局是framelayout并且没有背景色，可以考虑使用merge标签替换framelayout；weight属性不能嵌套使用，会导致测量计算次数指数增长。
5. 移除无用的资源
6. 过度绘制，尤其是背景色，应用指定了默认的背景色，不必再指定某些空间的背景色
7. 移除不必要的布局属性，比如linearlayout的alignparent、layout_centerVertical等，会导致view的过度计算//TODO:view绘制过程中，参数的问题
8. 忘记调用close方法：cursor及时释放.close，避免内存泄漏，typedarray应该recycle来释放资源。
9. 关闭linearlayout的baselineAligned属性。当linearlayout被用来分配两个嵌套布局之间的空间的时候，baselinealighed属性应该被关闭以保证计算更加快速。When a LinearLayout is used to distribute the space proportionally between nested layouts, the baseline alignment property should be turned off to make the layout computation faster
10. StringBuilder用于多个字符串拼接有利，如果数量比较少的字符串拼接，使用String就可以了，拼接的时候Stringbuilder不要和string混合使用。
11. hashmap可以用sparsearray替换
12. 包装类的使用通常不是直接new一个对象，要使用包装类提供的工厂方法。Integer.valueOf();
13. 4.0版本以前view的setTag方法是把tag保存在一个静态的hashmap中的，如果tag包含了其他长生命周期的引用，可能会导致内存泄漏。


##一、管理你的应用的内存
###共享内存

###分配和重用内存
###限制应用的内存
###转换APP