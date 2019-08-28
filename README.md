# Auxiliary

[![](https://jitpack.io/v/FMJZHF/Auxiliary.svg)](https://jitpack.io/#FMJZHF/Auxiliary)

Android开发辅助工具
 *****
## Setup

### Step 1. Add it in your root build.gradle at the end of repositories:
```
allprojects {
  repositories {
    ...
    maven { url 'https://jitpack.io' }
  }
}

```
### Step 2. Add the dependency
```
dependencies {
    implementation 'com.github.FMJZHF:Auxiliary:版本号'
}
```
## 1.实现TextView部分文字的点击事件
### 先看效果图
![TextView部分文字的点击事件效果图](https://raw.githubusercontent.com/FMJZHF/Auxiliary/master/img_folder/textview.png)

### 使用方法
```
/**
 * kotlin 语言
 */
class NoUnderLineTextActivity : AppCompatActivity(), I_ClickableSpan {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_no_under_line_text)

        var text = "我已阅读并同意用户协议和隐私政策\n以及官网认证服务条款"

        // PairEntity("点击部分文字"，"区分文字的点击事件")
        val pairEntity1 = PairEntity("用户协议", "1")
        val pairEntity2 = PairEntity("隐私政策", "2")
        val pairEntity3 = PairEntity("官网认证服务条款", "3")

        /**
         * 设置点击文字没有下划线
         * @param noUnderLineTextTv TextView 控件
         * @param text 显示的文字
         * @param Color.parseColor("#3BAC6A") 点击文字的字体色值
         * @param PairEntity 设置点击文字的文案
         */
        NoUnderLineTextUtil.setTextNoUnderLine(this,
            noUnderLineTextTv,
            text,
            Color.parseColor("#3BAC6A"),
            pairEntity1 , pairEntity2, pairEntity3
        )

        /**
         * 设置点击文字含有下划线
         * @param underLineTextTv TextView 控件
         * @param text 显示的文字
         * @param Color.parseColor("#3BAC6A") 点击文字的字体色值
         * @param pairEntity1 设置点击文字的文案
         */
        NoUnderLineTextUtil.setTextUnderLine(
            this,
            underLineTextTv,
            text,
            Color.parseColor("#3BAC6A"),
            pairEntity1
        )
    }

    /**
     * 不同类型的点击事件
     */
    override fun OnSpanClick(pairEntity: PairEntity) {

        var type = pairEntity.clickType
        if (type == "1") {
            showHint("点击了："+pairEntity.clickText)
        } else if (type == "2") {
            showHint("点击了："+pairEntity.clickText)
        } else if (type == "3") {
            showHint("点击了："+pairEntity.clickText)
        } else {
            showHint("未设置点击事件")
        }

    }

    private fun showHint(text: String) {
        Toast.makeText(this, text, Toast.LENGTH_SHORT).show()
    }
}
```
## 2.Android 选择器
### 先看效果图
![Android 选择器效果图](https://github.com/FMJZHF/Auxiliary/blob/master/img_folder/wheelpicker.png)

### 使用方法
#### 自定义属性
```
xmlns:app="http://schemas.android.com/apk/res-auto"
	
app:canLoop="true"    <!-- 是否循环滚动 -->
app:centerTextColor="#404040"   <!-- 选择字体的颜色 -->
app:drawItemCount="7"  <!-- 总展示数量(包含分割线) -->
app:initPosition="3"  <!-- 初识显示数量 -->
app:lineColor="#999999"  <!-- 分割线的颜色 -->
app:textSize="18sp"   <!-- 字体大小 -->
app:topBottomTextColor="#cccccc"    <!-- 上下文字的颜色 -->
```
#### 具体使用方法
```
wheelPickerYear.setDataList(mYearList)
wheelPickerYear.setInitPosition(yearPos) // 默认选中的年份
//年份滚动选择
wheelPickerYear.setLoopListener(object : WheelPickerScrollListener {
    override fun onItemSelect(item: Int) {
        yearPos = item
        Log.e("选择的年：", mYearList[item])
        titleView.text = mYearList[yearPos] + "-" + mMonthList[monthPos] + "-" + mDayList[dayPos]
    }
})	
```
## 3.时间操作类 [DateTime](https://github.com/FMJZHF/Auxiliary/blob/master/auxiliaryjar/src/main/java/com/zhf/auxiliaryjar/date/DateTime.kt)
## 4.SharedPreferences存放数据操作类 [SharedPreferencesUtil](https://github.com/FMJZHF/Auxiliary/blob/master/auxiliaryjar/src/main/java/com/zhf/auxiliaryjar/sharedPreferences/SharedPreferencesUtil.kt)
## 5.获取本机手机号码及运营商 [SIMCardInfoUtil](https://github.com/FMJZHF/Auxiliary/blob/master/auxiliaryjar/src/main/java/com/zhf/auxiliaryjar/simCard/SIMCardInfoUtil.kt)
```
<!-- 获取手机号码 -->
SIMCardInfoUtil(this).getPhoneLocalEncry(true)
<!-- 获取运营商 -->
SIMCardInfoUtil(this).providersName
```
## 6.操作状态栏 [StatusBarNavigationBarUtil](https://github.com/FMJZHF/Auxiliary/blob/master/auxiliaryjar/src/main/java/com/zhf/auxiliaryjar/statusBar/StatusBarNavigationBarUtil.kt)
```
在Activity or Fragment onCreate 方法中进行调用
// 默认状态栏字体为白色
StatusBarNavigationBarUtil.immersiveStatusBarNavigationBar(this, statusBar = true, navigationBar = true)
StatusBarNavigationBarUtil.setLightStatusBar(this, false)
```
