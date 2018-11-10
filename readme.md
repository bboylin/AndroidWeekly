AndroidWeekly : 每周更新值得推荐的技术文章
---

技术积累是一个工程师的底蕴，大学时期我也经常看技术文章，但是看过之后，时间久了就忘记了，一是没有运用场景实践，二是没有总结和记录。工作以后业余时间没有大学那么多了，所以更应该好好利用。
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

