### Activity

> [生命周期](#生命周期)、[设备旋转](#设备旋转)、[Activity的启动](#Activity的启动)、[Activity的数据传输](#Activity的数据传输)、[Tips](#Tips)

#### 生命周期

- onCreate()
- onStart()
- onResume()
- onPause()
- onStop()
- onDestroy()



#### 设备旋转

设备旋转时，Activity的实例会被系统销毁，然后创建一个新的实例。在`res/layout-land/`目录下创建Activity的水平布局。

可以重写`onSaveInstanceState(Bundle)`方法保存数据到Bundle中，在onCreate()方法中可以恢复Bundle中保存的数据



#### Activity的启动

使用`Intent(Context packageContext, Class<?> cls)`告知ActivityManager改启动哪个Activity。

1. 显示启动

   同一应用中启动Activity使用显示启动。

   ```java
   Intent i=new Intent(this,DemoActivity.class);
   startActivity(i);
   ```

2. 隐式启动

   在一个应用中，启动另一个应用的Activity，可通过创建隐式intent来处理。



#### Activity数据传输

1. 使用intent extra在activity之间传输数据

   `Intent.putExtra()`方法有多种形式，第一个参数是key，第二个参数可以是多种数据类型。

   获取Extra中的数据，使用`getInstent().getExtra()`。

2. 从子activity中获取返回的结果

   使用`startActivityForResult(Intent intent,int requestCode)`启动子activity，在子activity中设置`setResult()` ，可以重写父activity中的`onResult()`方法中获取子activity中的数据，

   ​

   通常来说result code可以是以下两个中的任意一个

   - Activity.RESULT_OK
   - Activity.RESULT_CANCELED



#### Tips

-  [使用LocalActivityManager实现Activity嵌套Activity](http://blog.csdn.net/dyc333236081818/article/details/7519602)