AndroidWeekly : 每周更新值得推荐的技术文章
---

技术积累是一个工程师的底蕴，大学时期我也经常看技术文章，但是看过之后，时间久了就忘记了，一是没有去结合运用场景实践，二是没有总结和记录。工作以后业余时间没有大学那么多了，也更应该好好利用。
在这个库我会把自己业余所看到的不错的技术博客总结记录下来，长此以往，相信会一步一步看到自己的进步。收录博客主要涉及源码解析，设计模式，架构，新技术等方面,有不错的博客推荐欢迎提issue或者pr，点watch每期更新的时候都能收到提醒。

纸上得来终觉浅，绝知此事要躬行。

### 第一期：2018/11/5-2018/11/11

* [Android leak pattern: subscriptions in views](https://medium.com/square-corner-blog/android-leak-pattern-subscriptions-in-views-18f0860aa74c)

概要：匿名内部类持有外部实例引用的泄漏case。`onFinishInflate`一直会调用，但是`onAttachedToWindow`的调用：addView的时候parent view有window会立即调用，没有window会等parent attach to 一个window的时候调用。而且，View.onAttachedToWindow() is called on the first view traversal, sometime after Activity.onStart()
* [A small leak will sink a great ship](https://medium.com/square-corner-blog/a-small-leak-will-sink-a-great-ship-efbae00f9a0f)

概要：Dalvik VM（Android 5.0以前）在当前message被消耗又没有新的message入队的时候不会gc掉这个message，AlertDialog的onClickListener会入消息队列，被message持有，message发送的时候是copy了一份，最初的message并没有被发送，所以永远不会被回收，如果listener持有外部activity引用会造成内存泄漏。解决办法：clearOnDetach/send an empty message
*  [Advocating Against Android Fragments](https://medium.com/square-corner-blog/advocating-against-android-fragments-81fd0b462c97)

概要：square tech leader PY重度使用fragment后的总结。1. Most of our difficult crashes were related to the fragment lifecycle.
2. We only need views to build a responsive UI, a backstack, and screen transitions.
* [支付宝客户端架构解析：Android 客户端启动速度优化之「垃圾回收」](https://juejin.im/post/5be1077d518825171140dbfa)

概要：支付宝通过抑制GC提升启动速度的大致思路：取消 softlimit 检测，取消 GC 线程的唤醒，取消 GC 例程函数，OOM 停止 GC 抑制。
* [
LiveData Overview](https://developer.android.com/topic/libraries/architecture/livedata#java)

概要：使用Android官方live-data组件赋予data感知UI生命周期的能力。常出现在viewmodel中，主要有onActive(),onInactive(),setValue()几个重要方法。
* [Android安全防护之旅—只需要这几行代码让Android程序项目变得更加安全](http://www.520monkey.com/archives/1263)

概要：1.混淆。2.防hook。3.防抓包。4.防调试。5.签名校验。6.加固。

### 第二期：2018/11/12-2018/11/18

* [在 Chrome DevTools 中调试 JavaScript 入门](https://developers.google.com/web/tools/chrome-devtools/javascript/?hl=zh-cn)
* [从一段奇怪代码开始说](https://zhuanlan.zhihu.com/p/24720906)

概要：fresco中封装的`OOMSoftReference<T>`中持有3个相同的`SoftReference<T>`，原因是Dalvik每次GC的时候会把排在偶数位的SoftReference当成WeakReference来处理（如果它的引用不是GC Roots可达），如果GC for alloc之后仍没有足够内存分配 ，所有的SoftReference都会被clear。这意味着只要某对象有一个SoftReference活着，那它所有的SoftReference都活着，所以利用两个连续的SoftReference就能保证不会被GC，为了保险这里使用了三个。确保了只有在抛OOM之前OOMSoftReference在会被回收。
* [Forget RxJava: Kotlin Coroutines are all you need. Part 1/2](https://proandroiddev.com/forget-rxjava-kotlin-coroutines-are-all-you-need-part-1-2-4f62ecc4f99b)

概要：RxJava vs kotlin coroutines

| RxJava | kotlin coroutines |
| --- | --- |
| Performance overhead 操作符生成大量对象 | 较少对象 |
| Unreadable stacktrace | Unreadable stacktrace |
| The learning complexity & Readability | higher Readability |
kotlin coroutines 写起来很像js的async await，非常接近同步写法了。

* [The Android Lifecycle cheat sheet — part II: Multiple activities](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-ii-multiple-activities-a411fd139f24)

* [The Android Lifecycle cheat sheet — part III : Fragments](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-iii-fragments-afc87d4f37fd)

* [R8, the new code shrinker from Google, is available in Android studio 3.3 beta](https://android-developers.googleblog.com/2018/11/r8-new-code-shrinker-from-google-is.html)

概要：R8 does all of shrinking, desugaring and dexing in one step. When comparing to the current code shrinking solution, Proguard, R8 shrinks the code faster while improving the output size.

### 第三期：2018/11/19-2018/11/25