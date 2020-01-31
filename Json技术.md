1. JavaScript中为什么要用JSON.parse来替代eval()?

   因为如果现在传回来的是一个json数据，然后正常的情况下是不会出现问题的，比如现在的json是这样:

   ```json
   {"animal":"cat"}
   ```

   然后javaScript通过下面的代码来获取json然后中调用他

   ```javascript
   var jsonString='{"animal":"cat"}';//一般都是去请求第三方服务器来获取json
   var myObject=eval("("+jsonString+")");
   //注意：由于json对象是用{}括起来的，在javascript中会被当成语句块处理，所以必须将其强制转换成表达式，所以在jsonStr的两边要加上()
   alert(myObject.animal)
   ```

   然后他是会弹出一个显示cat的弹窗,这是没问题的，但是如果现在的jsonString变量的值变成了

   ```json
   alert("json文件被其他人修改了")//比如现在这个json数据被别人劫持然后修改成了恶意的js代码
   ```

   然后evel函数执行的时候就会直接弹出一个对话框显示**"json文件被其他人修改了"**，所以这就是为什么解析json的时候不要用eval。
   
   用JSON.parse()的时候他是单纯的解析json，并不会执行任何的脚本，这样就算json被篡改了，也不会出现上面的情况。