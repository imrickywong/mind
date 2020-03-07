# axios避免重复请求

## A. 独占性提交

只允许同时存在一次提交操作，并且直到本次提交完成才能进行下一次提交。

##  B. 贪婪型提交

无限制的提交，但是以最后一次操作为准；亦即需要尽快给出最后一次操作的反馈，而前面的操作结果并不重要。

适用于点赞场景，用户觉得有误触操作后立即取消触发第二次请求。

## C. 节制型提交

无论提交如何频繁，任意两次有效提交的间隔时间必定会大于或等于某一时间间隔；即以一定频率提交。

如果客户发送每隔100毫秒发送过来10次请求，此模块将只接收其中6个（每个在时间线上距离为150毫秒）进行处理。

采用`throttle`，类似场景有resize，scroll，mousemove。

## D. **懒惰型提交**

任意两次提交的间隔时间，必须大于一个指定时间，才会促成有效提交。

> 知乎草稿举例，当在编辑器内按下 ctrl + s 时，可以手动保存草稿；如果你连按，程序会表示不理解为什么你要连按，只有等你放弃连按，它才会继续。

## E. 记忆型

对于同样的参数，其返回始终结果是恒等的——每次都将返回同一对象

## F. 累积型

连续的多次提交合并为一个提交

## B+C

> 搜索场景下
>
> * 当用户快速输入文本时（特别是打字能手），可以 throttle keypress 事件处理函数，以指定时间间隔来提取文本域的值，然后立即进行新的查询
> * 当新的查询需要发送，但上一个查询还没返回结果时，可以 abort 未完成的查询，并立即发送新查询

## C+D

> * 游戏中你捡到一把威力强大的高速武器，为了防止你的子弹在屏幕上打成一条直线，可以 throttle 来控制频率
> * 在弹幕型游戏里，为了防止你把射击键夹住来进行无脑游戏，可以用 debounce 来控制频率




