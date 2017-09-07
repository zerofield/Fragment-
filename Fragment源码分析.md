# Fragment源码分析
由于Fragment的独立性和灵活性，在App中拥有广泛的使用。然而，如果使用不当就会造成一些奇怪的BUG发生。本文将对Fragment源码进行分析，从而更好的理解Fragment的使用。由于笔者水平有限，分析的不正确之处还望指出。

## 本文主要分析的内容
- Fragment的使用
- Activity与Fragment之间的关系
- 一次Transaction发生了什么
- Fragment.startActivityForResult过程
- Fragment的恢复机制

## 本文不会涉及到的内容

- Transition
- Fragment与Loader

## Fragment的使用

以下代码片段展示了Fragment的基本使用方式，对于其中的一些特殊处理会在稍后分析。

```Java
public class MainActivity extends FragmentActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //在Activity的恢复过程中，Fragment的恢复将由FragmentManager管理
        //如果不进行判断，直接创建MyFragment并添加到FraggmentManager中界面上将会有两份Fragment
        MyFragment myFragment = (MyFragment) getSupportFragmentManager().findFragmentById(R.id.container);

        if (myFragment == null) {
            myFragment = new MyFragment();
            //myFragment被设置为保留实例，当屏幕发生旋转时，Fragment将不会发生销毁、重建
            myFragment.setRetainInstance(true);
            getSupportFragmentManager()
                    .beginTransaction()
                    .add(R.id.container, myFragment)
                    .commit();
        }
    }

    //Fragment在MainActivity.java中定义时必须声明为静态内部类
    //MyFragment必须拥有无参构造方法
    //在Fragment的恢复部分将会介绍为什么会有这些限制
    public static class MyFragment extends Fragment {
        // ...
    }
}

```

## Activity与Fragment之间的关系


## 一次Transaction发生了什么

## Fragment.startActivityForResult过程

## Fragment的恢复机制


### 总结
