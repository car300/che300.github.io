# View绘制

1、绘制动作在activity的声明周期的哪个过程触发，如何触发？
2、绘制进行前的准备流程，绘制过程中的注意点，绘制相关API的理解
3、绘制提交后由谁负责处理，surface与surfaceFinger的关系
4、surfaceview和普通view的区别，优缺点，使用注意点。
5、surface详解

---
Activity启动
> ActivityThread.java

    /**
     * Extended implementation of activity launch. Used when server requests a launch or relaunch.
     */
    @Override
    public Activity handleLaunchActivity(ActivityClientRecord r,...,Intent customIntent) {
        ...
        WindowManagerGlobal.initialize();// 内部拿到了WMS

        final Activity a = performLaunchActivity(r, customIntent);
        ...
    }
    
    /**  Core implementation of activity launch. */
    private Activity performLaunchActivity(ActivityClientRecord r, Intent customIntent) {
        ...
        Activity activity = null;
        try {
            java.lang.ClassLoader cl = appContext.getClassLoader();
            activity = mInstrumentation.newActivity(
                    cl, component.getClassName(), r.intent);
        ...
        Application app = r.packageInfo.makeApplication(false, mInstrumentation);
        ...
        activity.attach(...);
        ...
        if (r.isPersistable()) {
            mInstrumentation.callActivityOnCreate(activity, r.state, r.persistentState);
        } else {
            // Activity#onCreate
            mInstrumentation.callActivityOnCreate(activity, r.state);
        }
    }
    
> Activity.java

    final void attach(...) {
        ...
        mWindow = new PhoneWindow(this, window, activityConfigCallback);
        // 初始化PhoneWindow
        ...
    }
    
> PhoneWindow.java

    @Override
    public void setContentView(int layoutResID) {
        installDecor();// 创建DecorView
        ...
        mLayoutInflater.inflate(layoutResID, mContentParent);// inflate view & addView
    }    

===
View绘制

> ActivityThread.java

    @Override
    public void handleResumeActivity(...) {
        ...
        // TODO Push resumeArgs into the activity for consideration
        final ActivityClientRecord r = performResumeActivity(token, finalStateRequest, reason);
        ...
        ViewManager wm = a.getWindowManager();// 实现类WindowManagerImpl
        ...
        wm.addView(decor, l);// #3868
        ...
    }
        

 > WindowManagerGlobal.java
    
    public void addView(View view, ...) {
        ...
        // 创建ViewRootImpl
        root = new ViewRootImpl(view.getContext(), display);
        ...
        // do this last because it fires off messages to start doing things
        try {
            root.setView(view, wparams, panelParentView);
        } catch (RuntimeException e) {
           ...
        }
    } 
    
> RootViewImpl.java
    
    public void setView(View view,...) {
        // Schedule the first layout -before- adding to the window
        // manager, to make sure we do the relayout before receiving
        // any other events from the system.
        requestLayout();// 绘制第一帧，最终调用了this.performTraversals()方法
        
        ...
        view.assignParent(this);// DecorView
        // 给view变量mParent赋值，View的requestLayout和invalidate等才可以生效
        ...
    } 
    
    private void performTraversals() {
        ...
        // Ask host how big it wants to be
        performMeasure(childWidthMeasureSpec, childHeightMeasureSpec);// #2274
        // 测量模式...
        ...
        performLayout();// #2320
        ...
        performDraw();// #2485
        // 过渡绘制...
        ...
    }
 
> 一个Activity对应着一个PhoneWindow对象，是一对一的关系。

> PhoneWindow同时管理着ActionBar和下面的内容主题，setContentView()方法是用来设置内容主体的，而setTitle()等其他方法就是操作ActionBar的，Window中定义的requestFeature()等方法，有很多与ActionBar属性相关的设置。

> PhoneWindow并不是一个视图（View），它的成员变量mDecor才是整个界面的视图，mDecor是在generateLayout()的时候被填充出来的，而actionBar和contentParent两个视图都是通过findViewById()直接从mDecor中获取出来的。 
    
    

    


