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

