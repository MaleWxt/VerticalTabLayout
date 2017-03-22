# VerticalTabLayout
一个垂直竖向的Android TabLayout    
![](https://github.com/qstumn/VerticalTabLayout/blob/master/demo.png?raw=true)  

## Change Log
```
v1.2.1
1、修复在onCreate中调用setTabSelected时Indicator没有正确移动的BUG
2、修复使用setupWithFragment时偶尔会造成无法正确添加Fragment的BUG
3、对项目包结构进行微调、重构TabView，去除了构造TabTitle时的Context参数要求，增加setTabBadge、getBadgeView等方法
4、添加了全新的Badge，依赖于https://github.com/qstumn/BadgeView，提供可以高度自由化定制的Badge，调整TabAdapter结构适配新Badge
```  
![](https://github.com/qstumn/VerticalTabLayout/blob/master/demo_gif.gif?raw=true)

### 一些特性
* 支持自定义Indicator大小

* 支持自定义Indicator位置

* 支持Indicator设置圆角

* 支持Tab设置Badge

* 支持Adapter的方式创建Tab

* 多种Tab高度设置模式

* 很方便的和ViewPager结合使用

* 很方便的和Fragment结合使用

## how to use:
### 1. gradle
```groovy
	compile 'q.rorbin:VerticalTabLayout:VERSION_CODE'
```
VERSION_CODE : [here](https://github.com/qstumn/VerticalTabLayout/releases)
### 2. xml
```xml
    <q.rorbin.verticaltablayout.VerticalTabLayout
        android:id="@+id/tablayout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="#EDEDED"
        app:indicator_color="#FFFFFF"
        app:indicator_gravity="fill"
        app:tab_height="50dp"
        app:tab_mode="scrollable" />
```    

### 3. 属性说明

xml | code | 说明
---|---|---
app:indicator_color | setIndicatorColor | 指示器颜色
app:indicator_width | setIndicatorWidth | 指示器宽度
app:indicator_gravity | setIndicatorGravity | 指示器位置
app:indicator_corners | setIndicatorCorners | 指示器圆角
app:tab_mode | setTabMode | Tab高度模式
app:tab_height | setTabHeight | Tab高度
app:tab_margin | setTabMargin | Tab间距

### 4. 创建Tab的方式
- 普通方式创建
```java
	tablayout.addTab(new QTabView(context))
	tablayout.addOnTabSelectedListener(new VerticalTabLayout.OnTabSelectedListener() {
            @Override
            public void onTabSelected(TabView tab, int position) {
                
            }

            @Override
            public void onTabReselected(TabView tab, int position) {

            }
        });
```
- Adapter方式创建			
```java
	tablayout.setTabAdapter(new TabAdapter() {
            @Override
            public int getCount() {
                return 0;
            }

            @Override
            public TabView.TabBadge getBadge(int position) {
                return null;
            }

            @Override
            public TabView.TabIcon getIcon(int position) {
                return null;
            }

            @Override
            public TabView.TabTitle getTitle(int position) {
                return null;
            }

            @Override
            public int getBackground(int position) {
                return 0;
            }
	     });
```   
	按照自己的需要进行返回相应的值即可，不需要的返回0或者null
	也可以选择使用SimpleTabAdapter，内部空实现了TabAdapter的所有方法
	TabBadge、TabIcon、TabTitle使用build模式创建。
  
- 结合ViewPager使用
```java
	tablayout.setupWithViewPager(viewpager);
```
	ViewPager的PagerAdapter可选择实现TabAdapter接口
      
- 结合Fragment使用
```java
	tabLayout.setupWithFragment(FragmentManager manager, int containerResid, List<Fragment> fragments, TabAdapter adapter)
```
### 5. 设置badge
```java
	int tabPosition = 3;
	int badgeNum=55;
	tablayout.setTabBadge(tabPosition,badgeNum);
	Badge badge = tablayout.getTabAt(position).getBadgeView();
	
	Badge使用方法请移步https://github.com/qstumn/BadgeView
```

# LICENSE
```
Copyright 2016, RorbinQiu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
