## 学习计划表生成器（艾宾浩斯计划表）

- 修改复习计划：在 `index.html` 中找到类似于如下的代码，每一行表示一次复习，`weekday + i + n` 的 `n` 表示第几天后复习。

``` html
for (var i = 0,l=plan.length; i < l; i++) {
  calendar.children().eq(weekday+i+1).append("<br>*"+book+" "+plan[reverse?l-i-1:i])
  calendar.children().eq(weekday+i+4).append("<br>*"+book+" "+plan[reverse?l-i-1:i])
  calendar.children().eq(weekday+i+10).append("<br>*"+book+" "+plan[reverse?l-i-1:i])
};
```

- 注意修改了复习计划后要调整下生成的日期数，位置在 `index.html` 中的 `maxExtraDay` 变量，例如上面的复习最大间隔为 `10`，就应该把 `maxExtraDay` 设置为 `10`。不修改的话日程表最后会有一些空白日期。

``` html
var calendar=$("#calendar").empty();
var reverse=$("#reverse").prop("checked");
var maxExtraDay=10;

$("h1").text($("#plan").val())
for (var i = 0,l=totalList/listPerDay+maxExtraDay+weekday; i<l; i++) {
  currentDay=new Date(firstLineSunday-0+i*86400000);
  calendar.append("<div>"+(currentDay.getMonth()-0+1)+"/"+currentDay.getDate()+"</div>")
};
```

- 修改默认值：修改以下部分：

``` html
<form id="sidebar">
 	<table>
 		<tbody><tr><th>计划名</th><td><input id="plan" value="Review Plan"></td></tr>
 		<tr><th>List 名</th><td><input id="book" value=""></td></tr>
 		<tr><th>开始日期</th><td><input id="startDate" type="date"></td></tr>
 		<tr><th>每天 List 数</th><td><input id="listPerDay" value="1"></td></tr>
 		<tr><th>List 总数</th><td><input id="totalList" value="30"><br></td></tr>
 		<tr><th>是否逆序</th><td><input id="reverse" type="checkbox"></td></tr>
 		<tr><th></th><td><button id="generate">点击这里生成</button><button type="button" onclick="javascript:window.print()">打印</button></td></tr>
 	</tbody></table>
	<br>
</form>
```