##view事件分发机制
*事件分发需要View的三个重要方法：<br>
1.public boolean dispatchTouchEvent(MotionEvent event)<br>
它就是事件分发的重要方法。那么很明显，如果一个MotionEvent传递给了View，那么dispatchTouchEvent方法一定会被调用！
返回值：表示是否消费了当前事件。可能是View本身的onTouchEvent方法消费，也可能是子View的dispatchTouchEvent方法中消费。返回true表示事件被消费，本次的事件终止。返回false表示View以及子View均没有消费事件，将调用父View的onTouchEvent方法。<br>
2.public boolean onInterceptTouchEvent(MotionEvent ev)<br>
事件拦截，当一个ViewGroup在接到MotionEvent事件序列时候，首先会调用此方法判断是否需要拦截。特别注意，这是ViewGroup特有的方法，View并没有拦截方法
返回值：是否拦截事件传递，返回true表示拦截了事件，那么事件将不再向下分发而是调用View本身的onTouchEvent方法。返回false表示不做拦截，事件将向下分发到子View的dispatchTouchEvent方法。<br>
3.public boolean onTouchEvent(MotionEvent ev)<br>
真正对MotionEvent进行处理或者说消费的方法。在dispatchTouchEvent进行调用。
返回值：返回true表示事件被消费，本次的事件终止。返回false表示事件没有被消费，将调用父View的onTouchEvent方法。<br>

```java
Class Activity：
    public boolean dispatchTouchEvent(MotionEvent ev) {
        if (ev.getAction() == MotionEvent.ACTION_DOWN) {
            onUserInteraction();
        }
        if (getWindow().superDispatchTouchEvent(ev)) {//事件分发并返回结果
            return true;//事件被消费
        }
        return onTouchEvent(ev);//没有View可以处理，调用Activity onTouchEvent方法
    }
```
跟进第二个if<br>
```java
Window类说明
/**
 * Abstract base class for a top-level window look and behavior policy.  An
 * instance of this class should be used as the top-level view added to the
 * window manager. It provides standard UI policies such as a background, title
 * area, default key processing, etc.
 *
 * <p>The only existing implementation of this abstract class is
 * android.view.PhoneWindow, which you should instantiate when needing a
 * Window.
 */
Class Window:
//抽象方法，需要看PhoneWindow的实现
public abstract boolean superDispatchTouchEvent(MotionEvent event);
```