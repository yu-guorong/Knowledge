### Fragment

> [生命周期](#生命周期)、[FragmentManager](#fragmentmanager)

#### 生命周期

- onAttach()
- onCreate()
- onCreateView()
- onActivityCreated()
- onStart()
- onResume()
- onPause()
- onStop()
- onDestroyView()
- onDestroy()
- onDetach()

#### FragmentManager

考虑到低版本兼容问题，一般使用v4包中的Fragment，使用`getSupportFragmentManager()`获取FragmentManager。

- 通过资源ID获取Fragment

  ```java
  fm.findFragmentById(R.id.fragment);	//容器视图资源id
  ```

  ​


#### Fragment数据传递

- 在Fragment中加入`newInstance(Data data)`方法，创建Fragment时不使用原来的构造方法创建。

- 类似于Activity的`startActivityForResult()`，Fragment可以使用`setTargetFragment(Fragment fragment, int requestCode)`来通知是哪一个Fragment在返回数据。

  在目标Fragment中使用`getTargetFragment().onActivityResult()`传递数据