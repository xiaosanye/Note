#  Android命名规范：[待修改]

Java命名规范 参考 阿里巴巴Java 开发手册


## 一、类文件的命名规范

### 1.1、包的命名规范：

建议采用如下规则：【com】.【公司名/组织名】.【项目名称】.【模块名】
比如：com.jacksen.mvp.demo。然后在这个目录下根据业务逻辑进行分层。

常见的包分层结构如下：

|包名|简介|
|:----:|:----:|
com.xxx.xxx.view | 自定义view 或者是View接口
com.xxx.xxx.activities | activity类
com.xxx.xxx.fragments | fragment类
com.xxx.xxx.adapter | 适配器相关
com.xxx.xxx.utils | 公共工具类
com.xxx.xxx.bean | 实体类
com.xxx.xxx.service | service服务
com.xxx.xxx.broadcast | 广播接收器
com.xxx.xxx.db | 数据库操作类
com.xxx.xxx.persenter | 中间对象
com.xxx.xxx.model | 数据处理类


### 1.2、类的命名规范
Android中类的命名与JAVA开发采用一致的规范即可（大驼峰命名法，即所有单词首字母大写。）。【看阿里巴巴Java开发手册】

|类别|命名举例|
|:----:|:-----:|
|Activity | xxxActivity.java
Application | xxxApplication.java
Fragment | xxxFragment.java
Service | xxxService.java
BroadcastReceiver | xxxBroReceiver.java
ContentProvider | xxxProvider.java
Adapter | xxxAdapter.java
Handler | xxxHandler.java
接口 | xxxInter.java
接口实现类 | xxxImpl.java
Persenter | xxxPersenter.java
公共父类 | BaseActivity.java、BaseFragment.java、- BaseAdapter.java等
util类 | LogUtil.java
数据库类 | BaseSQLiteDBHelper.java

### 1.3、变量的命名规范
>采用小驼峰

Java普通变量：
>resultString、userBean、loginPresenter

android控件变量：
>loginBtn、inputPwdEt、showNameTv

**常用控件的缩写：**

|控件 |	布局文件中缩写 |	代码中缩写|
|:-------:|:---------------------:|:------------:|
LinearLayout |	xxx_layout |	xxxLLayout
RelativeLayout | 	xxx_layout   |	xxxRLayout 
FrameLayout  |	xxx_layout  |	xxxFLayout
TextView  |	xxx_tv   |	xxxTv
EditText  |	xxx_et   |	xxxEt
Button   |	xxx_btn  |	xxxBtn
ImageView  |	xxx_iv   |	xxxIv
CheckBox  |	xxx_chk 	 | xxxChk
RadioButton   |	xxx_rbtn  |	xxxRbtn
ProgressBar   |	xxx_pbar | xxxPbar
ListView  |	xxx_lv   |	xxxLv
WebView  |	xxx_wv  |	xxxWv
GridView  |	xxx_gv 	|  xxxGv

**常见单词的缩写：**

单词 | 缩写
|:------:|:-----:|
icon  | 	ic
background  | 	bg
foreground  | 	fg
initial  | 	init
information  | 	info
success  | 	succ
failure  | 	fail
error |  	err
image  | 	img
library  | 	lib
message  | 	msg
password  | 	pwd
length  | 	len
buffer |  	buf
position   |   pos


### 1.4 常量命名规范：
>全部单词采用大写，每个单词之间用“_”分割。
```java
public static final String API_BASE_URL = "http://hailer.news";
```

### 1.5、方法的命名规范【主要看阿里巴巴Java开发手册】
>与java开发类似，采用驼峰命名规则。首单词首字母小写，其余单词首字母大写。尽量不要使用下划线。

举例：
setxxx()、getxxx()、loginxxx()、onCreate()、onDestory()、isxxx() ->【返回值是boolean类型】、checkxxx()


## 二、资源文件的命名规范
###  2.1、layout 布局文件的命名规范
#### 2.1.1、布局文件名的命名规范
**举例：**

|布局文件的命名规范|
|:-------------------------:|
| activity_login.xml | |
|fragment_first_tab.xml | |
|  item_choose_city.xml | |
| dialog_choose_city.xml | |
| common_footer.xml | |
|  popup_xxx.xml | |

#### 2.1.2 控件ID的命名规范
见上面的表格


### 2.2 drawable目录下的命名规范
>全部单词小写，单词之间采用下划线分割。

|类别|一般式|举例|
|:-----------:|:----------------:|:----:|
| 图标 |  ic_xxx.png | ic_logo.png
|背景图 | bg_xxx.jpg | bg_splash.jpg
|选择器|  selector | selector_login_btn.xml |
|图形| shape | shape_login_btn.xml |
|图片状态 | |bg_login_btn_pressed.jpg  、   bg_login_btn_unpressed.jpg

### 2.3 anim目录下的命名规范
>单词全部小写，单词之间采用下划线分割。

|举例|
|:-----:|
|  fade_in.xml |  |
|  fade_out.xml |
|  slide_in_from_left.xml |
|   slide_in_from_top.xml |
|   slide_out_to_right.xml |
|   slide_out_to_bottom.xml |

## 其他需要注意的地方
1、【重要】代码中尽量不要出现中文。注释除外。代码中通过strings.xml引用来显示中文。

2、控件声明放在activity级别，这样在activity其他地方可以使用。

3、在一个View.OnClickListener中处理所有的点击事件逻辑，这样看起来很集中和直观。

4、strings.xml中使用%1sd等实现字符串的通配。

5、布局文件中的字体大小，都定义在dimens.xml中。

6、有关margin和padding的值也都放在dimens.xml中。

7、界面之间传值尽量使用intent方式。少用全局变量。

8、不建议在布局文件中添加点击事件。

9、数据类型转换一定要校验。

10、使用常量代替枚举。

11、实体不要在不同模块间共享，但是可以在统一模块下的不同页面共享。

12、业务稍微复杂一些，都有可能提炼一个BaseActivity或BaseFragment出来做为公共父类。

13、类注释一定要写，方法也一定要写方法注释。常量尽量写注释。



## 三、MVP 代码结构
目前是按照功能划分包