# Android状态栏微技巧，带你真正理解沉浸式模式
# 什么是沉浸式？

先来分析一下叫错的原因吧，之所以很多人会叫错，是因为根本就不了解沉浸式是什么意思，然后就人云亦云跟着叫了。那么沉浸式到底是什么意思呢？

根据百度百科上的定义，沉浸式就是要给用户提供完全沉浸的体验，使用户有一种置身于虚拟世界之中的感觉。

比如说现在大热的VR就是主打的沉浸式体验。

那么对应到Android操作系统上面，怎样才算是沉浸式体验呢？这个可能在大多数情况下都是用不到的，不过在玩游戏或者看电影的时候就非常重要了。因为游戏或者影视类的应用都希望能让用户完全沉浸在其中，享受它们提供的娱乐内容，但如果这个时候在屏幕的上方还显示一个系统状态栏的话，可能就会让用户分分钟产生跳戏的感觉。

比如说我现在新建了一个空项目，然后修改布局文件中的代码，在里面加入一个ImageView，如下所示：

<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:src="@drawable/bg"
        android:scaleType="centerCrop" />
</RelativeLayout>
# 真正的沉浸式模式

虽说沉浸式导航栏这个东西是被很多人误叫的一种称呼，但沉浸式模式的确是存在的。那么我们如何才能实现像海岛奇兵以及爱奇艺那样的沉浸式模式呢？

首先你应该确定自己是否真的需要这个功能，因为除了像游戏或者视频软件这类特殊的应用，大多数的应用程序都是用不到沉浸式模式的。
当你确定要使用沉浸式模式，那么只需要重写Activity的onWindowFocusChanged()方法，然后加入如下逻辑即可：

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        super.onWindowFocusChanged(hasFocus);
        if (hasFocus && Build.VERSION.SDK_INT >= 19) {
            View decorView = getWindow().getDecorView();
            decorView.setSystemUiVisibility(
                View.SYSTEM_UI_FLAG_LAYOUT_STABLE
                | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_LAYOUT_FULLSCREEN
                | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION
                | View.SYSTEM_UI_FLAG_FULLSCREEN
                | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY);
        }
    }

}

原创地址：http://blog.csdn.net/guolin_blog/article/details/51763825

博  客：http://blog.csdn.net/xiaole0313

GitHub：https://github.com/xiaole0310
