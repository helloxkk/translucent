
### app沉浸式的封装（兼容4.4，以下效果都是4.4版本）
### 如何使用
添加依赖
	

step1、项目gradle中
```
allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```
step2、app gradle中


```
	dependencies {
	        compile 'com.github.livesun:translucent:v1.0'
	}

```
设置AppTheme为NoActionBar
例如：
```
    <style>
	<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorAccent</item>
        <item name="colorAccent">@color/colorAccent</item>
     
    </style>

```
注意：如果xml布局中写了这个属性，需要删除掉
```
fitsSysytemWindows=“true"
```


1、继承BaseTranslucentActivity。

```
 MainActivity extends BaseTranslucentActivity
```

2、纯颜色调用setStatusColor(),在setContentView之后。
```
setContentView(R.layout.activity_main);
LinearLayout title= (LinearLayout) findViewById(R.id.title);
//需要沉浸的标题栏，可以是Toolbar，LinearLayout，等等
//参数二，为颜色id
//参数三，石否开启手动隐藏展示状态栏和导航栏
setStatusColor(title,R.color.colorPrimary,false);

```
开启手动隐藏和展示的效果，可以通过改方式实现全屏效果

![steep_toggel2](https://user-images.githubusercontent.com/27534854/27220469-d8ab2496-52b7-11e7-97de-84ad6185338b.gif)


3、图片沉浸效果，调用setStatusPicture();


```
setContentView(R.layout.activity_main);
LinearLayout title= (LinearLayout) findViewById(R.id.title);
//需要沉浸的标题栏，可以是Toolbar，LinearLayout，等等
//参数二，为图片id
//参数三，石否开启手动隐藏展示状态栏和导航栏
setStatusPicture(title,R.drawable.demobg,false);

```

效果如下

![steep03](https://user-images.githubusercontent.com/27534854/27220517-01729a6c-52b8-11e7-9c23-e39f06599deb.png)


4、标题栏和状态栏颜色一致，调用 setStatusAndNaviagtion()，并且需要重载setNavigationBarisTranslucent方法为true


```
/**
     * 是否设置导航条为透明，默认返回false。
     * @return
     */
    @Override
    protected boolean setNavigationBarisTranslucent() {
        return true;
    }

setContentView(R.layout.activity_main);
LinearLayout title= (LinearLayout) findViewById(R.id.title);
//参数一，需要沉浸的标题栏，可以是Toolbar，LinearLayout，等等
//参数二，展示的navigation的view，4.4版本需要手动在xml布局写死。
//参数三，为颜色id
 setStatusAndNaviagtion(title,nivagtion,R.color.colorPrimary);
 
 
 
 4.4 xml布局需要这样
 
 <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/root"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

   <LinearLayout
       android:id="@+id/title"
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="250dp"
       android:gravity="center"
       >
      <TextView
          android:text="ddddddddd"
          android:textSize="15sp"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content" />
   </LinearLayout>


   <View
       android:layout_alignParentBottom="true"
       android:id="@+id/nivagtion"
       android:layout_width="match_parent"
       android:layout_height="0.1dp"/>
</RelativeLayout>
 
```
效果如下

![steep04](https://user-images.githubusercontent.com/27534854/27220577-364d156e-52b8-11e7-8a57-8a0999c7935f.png)


5、关于setNavigationBarisTranslucent方法，默认是不会把4.4版本到5.0版本设置为透明色。

如有需要可以重载该方法
```
 /**
     * 是否设置导航条为透明，默认返回false。
     * @return
     */
    @Override
    protected boolean setNavigationBarisTranslucent() {
        return true;
    }

```
效果如下
false的效果：
![ota za 5fvww1io2lb_k7hn](https://user-images.githubusercontent.com/27534854/27220690-a656d9c6-52b8-11e7-9704-93164c40ac88.png)

true的效果
![s k7hh8jv ux9_ 6 ugguw](https://user-images.githubusercontent.com/27534854/27220701-b2f76452-52b8-11e7-9bf9-24e34c71d6ae.png)

博客讲解地址：https://livesun.github.io/2017/06/16/translucent/
