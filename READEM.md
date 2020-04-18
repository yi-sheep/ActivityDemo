# ActivityDemo

这是将Android第一行代码第二版翻译成kotlin的第一个项目，是从第二章开始的，当前项目使用kotlin演示了Toast提示、Menu菜单、摧毁当前活动。

Toast提示:

在布局中添加一个button用作点击显示toast提示。

对应的kotlin代码，在MainActivity这个类中。
```kotlin
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.Menu
import android.view.MenuItem
import android.widget.Toast
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        // 在kotlin中使用控件很方便，因为kotlin将我们加入布局中的控件以id为名生成了全局常量
        // 这里使用了按钮的点击事件，这个点击事件需要写一个匿名函数接收一个唯一的参数view:View
        // 当匿名函数只接收唯一的一个参数的时候，需要传入匿名函数的那个方法就可以去掉()变为{}
        // {}的范围就表示匿名函数的范围，在这个范围内it就表示接收的唯一参数
        buttonToast.setOnClickListener{
            // 当点击这个按钮的时候，在屏幕上显示一个Toast提示
            // 用法和java差不多
            // 第一个参数：context这里传入this就行
            // 第二个参数：提示的内容
            // 第三个参数：显示时长，有两个常量，Toast.LENGTH_LONG 长 LENGTH_SHORT 短
            // 最后别忘了调用.show() 显示出来
            Toast.makeText(this,"Hello Toast!",Toast.LENGTH_SHORT).show()
        }
    }
}
```

Menu菜单:

在res目录下右键->Android Resource File 在Resource type:选项上选择Menu,然后就是要创建菜单布局文件的名字。我这里文件名字为main。
然后就会在res目录下生成一个menu的文件夹里面有一个名加main.xml的布局文件。
接下来我们就编辑这个文件，还是以拖拽的形式，拖两个或三个MenuItem，我这里拖了三个到布局中，id分别为item_1、item_2、item_finish,还可以设置他们的title，就是显示在页面上的文字。

下面是关键了，在MainActivity类中加载菜单:
```kotlin
/**
 * 加载菜单
 * 重写onCreateOptionsMenu函数
 * 这个函数带有一个Menu类型的参数
 * 返回值类型为Boolean，true表示将菜单显示出来，false则反之
 */
override fun onCreateOptionsMenu(menu: Menu?): Boolean {
    menuInflater.inflate(R.menu.main,menu)
    // 在java中需要这个月写 getMenuInflater().inflate(R.menu.main,menu)
    // 对比可以看到kotlin很精简
    // 它将getMenuInflater()函数和一个常量绑定起来，直接使用这个常量就行
    return true // 这里返回一个true表示将菜单显示出来，false则反之
}
```

在MainActivity类中找到对应的MenuItem,并设置点击事件
```kotlin
/**
 * 给对应菜单item设置时间
 * 重写onOptionsItemSelected函数
 * 这个函数带有一个MenuItem类型的参数，通过这个参数可以找到加入到菜单中的每一个item
 * 返回值类型为Boolean true表示使用，false则反之
 */
override fun onOptionsItemSelected(item: MenuItem): Boolean {
    // 在kotlin中没有switch这个判断语句代替它的是when语句，具体写法如下
    when (item.itemId) {
        R.id.item_1 -> {
            // 这里我们还是使用Toast提示
            Toast.makeText(this, "This is item 1", Toast.LENGTH_SHORT).show()
        }
        R.id.item_2 -> {
            Toast.makeText(this, "This is item 2",Toast.LENGTH_SHORT).show()
        }
    }
    return true
}
```

摧毁一个活动:

在设置MenuItem点击事件的那个方法里,给id为item——finish的MenuItem设置点击事件，调用finish()函数
```kotlin
/**
 * ....
 */
override fun onOptionsItemSelected(item: MenuItem): Boolean {
    ...
    when (item.itemId) {
        ...
        R.id.item_finish->{
            // 和java一样调用finish()当前摧毁当前活动
            finish()
        }
    }
    return true
}
```

到整理这个demo就结束了，其中的内容不难，难就难在不太会kotlin，多看看，自己写一遍或改一改，慢慢体会。

