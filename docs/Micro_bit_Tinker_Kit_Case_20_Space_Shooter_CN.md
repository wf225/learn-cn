你是否厌倦了复杂的现代游戏？你更想要在micro:bit 5x5分辨率的屏幕上玩游戏，而不是在一个4K分辨率的屏幕上玩？那么尽情地享受micro:bit上的太空大战游戏吧！ 这篇教学博客里面的代码是用JavaScript编写的。你需要敲写很多代码哦！


## 目的  
---

在这个项目中，我们将会创建一个简单的太空射击游戏。在游戏中，你可以试着射击和躲避坠落的飞行物。


## 所需材料：  
---

- 1 x [BBC micro:bit](http://www.elecfreaks.com/estore/micro-bit-board.html)
- 1 x USB线
- 1 x [扩展板](http://www.elecfreaks.com/estore/elecfreaks-micro-bit-breakout-board.html)
- 1 x [ADKeypad](http://www.elecfreaks.com/estore/octopus-adkeypad.html)

![](http://www.elecfreaks.com/estore/download/spaceshooter-1.jpg)

**温馨提示: 如果你想要以上所有这些元器件，你可以购买我们的[micro:bit小小发明家套件](https://item.taobao.com/item.htm?spm=a230r.7195193.1997079397.9.z3IMPf&id=564707672256&abbucket=5)。**


## 目标  
---

- 学习ADKeyboard的使用。
- 学习基本的游戏编程。
- 学习更多关于Javascript的编程。


### 步骤 1 – 元器件连接  

![](http://www.elecfreaks.com/estore/download/spaceshooter-2.jpg)

首先，将ADKeypad插入到扩展板上。确保线的颜色和扩展板上引脚的颜色一致，并记住你所插入的引脚，因为它将和后面的内容有关。


### 步骤 2 – 编程  

![](http://www.elecfreaks.com/estore/download/spaceshooter-5.png)

在这个项目中，我们将用Javascript来编程。所以，首先，在页面顶部切换到Javascript模式。

![](http://www.elecfreaks.com/estore/download/spaceshooter-6.png)

在我们代码的开头，我们将需要初始化我们将要使用的变量：playerscore（玩家当前的得分）、noalien（存储当前屏幕上有无外星人）、hi（目前的高分）、gamestart（追踪游戏当前的状态）、destroyedpos（用于存储玩家撞上外星人的数列）、shots（用于存储玩家射出的子弹位置）、aliens（存储外星人的位置）、pos（追踪玩家当前的位置）、toprow（存储当前外星人是否在顶排的每个位置），以及一些临时变量。稍后，我们将需要用到所有这些变量。

![](http://www.elecfreaks.com/estore/download/spaceshooter-7.png)

函数unrendership会熄灭代表我们的飞船的LED灯。我们将用它来将飞船四处移动。

![](http://www.elecfreaks.com/estore/download/spaceshooter-8.png)

函数rendership会点亮代表我们的飞船的LED灯。在使用unrendership之后，我们可以更新玩家的位置，然后用rendership来改变飞船的位置。 

![](http://www.elecfreaks.com/estore/download/spaceshooter-9.png)

函数unrendershots会熄灭代表玩家射出的子弹的LED灯。同样，我们将会用这个函数来更新子弹的位置。 

![](http://www.elecfreaks.com/estore/download/spaceshooter-10.png)

函数rendershots会点亮代表玩家射出的子弹的LED灯。和unrendership与rendership一样，在使用unrendershots之后，我们可以更新子弹的位置，然后用rendershots来改变所有的已射出的子弹位置。

![](http://www.elecfreaks.com/estore/download/spaceshooter-11.png)

函数checkcollision会检查两种类型的碰撞：玩家和外星人，以及外星人和玩家发射的子弹。

首先，对于玩家和外星人之间的碰撞，因为我们飞船的形状，我们需要检查飞船中间一列的底部或者倒数第二排是否有外星人，以及底排到飞船中间的左边或者右边是否有外星人。注意：在Javascript中，&& 代表“和”， ||代表“或”。如果在这些位置确实有外星人，我们将会把destroyedpos设置到这个外星人和飞船碰撞的地方，并且将gamestart的值变为2来象征游戏结束。

接下来，对于外星人和玩家发射的子弹之间的碰撞，因为它们每个只占了一个LED，所以我们只需要检查它们的实际位置是否一致。但是，因为这里可能会有多次射击或者多个外星人，我们需要为每个外星人循环每次射击，并检查它们是否在同一个位置。如果它们在同一个位置，我们就熄灭那个位置的LED灯。如果外星人在toprow（顶排），我们将toprow（顶排）那一列的数值设置为0，来代表那一列的顶排没有外星人。然后，我们将子弹的高度设置为-1，外星人的高度设置成5，并将它们两者移出屏幕，也就是我们稍后需要删除它们的地方。最后，如果玩家击中了一个外星人，我们就将玩家的得分加1。

![](http://www.elecfreaks.com/estore/download/spaceshooter-12.png)

现在我们已经写完了所有需要用到的函数，我们终于可以开始将它们连接起来了！你可能已经熟悉了在blocks编程中的forever函数。
在Javascript中，我们通过输入basic.forever(() => {Code to run forever here}来使用它。
首先，如果gamestart的数值为0，我们就会在屏幕上显示当前的高分。
接着，如果gamestart的数值等于2，这就意味着玩家的游戏结束。我们将玩家和外星人碰撞的那个位置的LED等闪烁3次，让玩家知道哪里发生了碰撞。然后，如果玩家获得了一个新的高分，就显示一个笑脸；如果没有的话，就显示一个哭脸。 
之后，我们会显示玩家的得分，并将gamestart的数值重新设置为0。

![](http://www.elecfreaks.com/estore/download/spaceshooter-13.png)

为了开始游戏，我们需要检测玩家是否按下了ADKeypad上的按钮A以及gamestart的数值是否为0。如果玩家按下了ADKeypad上的按钮A，我们需要将gamestart的数值设置为1（这代表游戏已经开始），重置玩家的位置为居中，将玩家的得分设置为0，关闭屏幕上所有的LED灯，然后将我们之前编写的函数运用到飞船上。

![](http://www.elecfreaks.com/estore/download/spaceshooter-14.png)

最后，如果gamestart的数值等于1，就说明玩家正在玩游戏哦！在每个循环的开始，我们熄灭玩家射出的每颗子弹的LED灯，因为他们需要向前移动一个位置。 我们用函数Math.random() 随机判断我们是否应该生成一个外星人外形。你可以将这个数字设低一些，使游戏变得更难；或者将这个数字设高一些，使游戏变得更加简单。在这里，我们使用的数值是15，这意味着一个外星人在每个循环中生成的机会只有1/15。但是，我们需要检查我们想要生成外星人的那一列的顶排没有被占用，否则很多外星人就会重叠在一起哦！ 接着，我们循环经过外星人，并让它们每次在forever运行5次之后向下移动1个位置。如果一个外星人到达了顶排，我们将那一列的顶排的数值设置为1，并且如果外星人离开顶排，我们就将这个数值设置为0。

![](http://www.elecfreaks.com/estore/download/spaceshooter-15.png)

然后，我们需要检查每个外星人是否位于屏幕的外面。如果外星人位于屏幕之外，我们就将它从我们外星人的数列中删除。最后，如果屏幕上没有外星人，我们就生成一个外星人，尽管只有1/15的机会。

![](http://www.elecfreaks.com/estore/download/spaceshooter-16.png)

在更新了外星人的位置之后，我们需要检查碰撞，然后更新子弹的位置。接着，如果玩家按下了ADKeypad上的的按钮D，我们就生成一个子弹。之后，我们需要把屏幕之外的子弹删了。

![](http://www.elecfreaks.com/estore/download/spaceshooter-17.png)

最后，我们需要检查玩家是否按下了ADKeypad上的按键C或者E，并相应地更新飞船的位置。在这之后，我们设置玩家发射的子弹，然后给每个循环设置0.08秒的暂停时间，以便游戏以可玩的速度进行。

你可以通过下面这个链接下载程序的完整代码：

[https://makecode.microbit.org/_euRV3uHYJAfx](https://makecode.microbit.org/_euRV3uHYJAfx)

或者，你也可以从下面这个页面下载代码：

<div style="position:relative;height:0;padding-bottom:70%;overflow:hidden;"><iframe style="position:absolute;top:0;left:0;width:100%;height:100%;" src="https://makecode.microbit.org/#pub:88941-65098-41980-28805" frameborder="0" sandbox="allow-popups allow-forms allow-scripts allow-same-origin"></iframe></div>


### 步骤 3: 玩游戏 

![](http://www.elecfreaks.com/estore/download/spaceshooter-18.jpg)

这个游戏玩起来非常简单。你只需要按下ADKeypad上的按钮A来启动游戏，按下按钮C和E来移动你的飞船，按下按钮D来射击外星人。


### 步骤 4 – 成功!  

太棒啦！是时候享受你的新太空大战游戏带来的经典乐趣了！你的最高分将会是多少呢？


## 常见问题
---


## 相关阅读  
---

[Micro:bit小小发明家课程01:音乐播放器](/Micro_bit_Tinker_Kit_Case_01_Music_Machine_CN/)                        
[Micro:bit小小发明家课程02:智能灯](/Micro_bit_Tinker_Kit_Case_02_Smart_Light_CN/)   
[Micro:bit小小发明家课程03:电子琴](/Micro_bit_Tinker_Kit_Case_03_Electro_Theremin_CN/)   
[Micro:bit小小发明家课程04:报警装置](/Micro_bit_Tinker_Kit_Case_04_Simple_Alarm_Box_CN/)   
[Micro:bit小小发明家课程05:土壤湿度检测](/Micro_bit_Tinker_Kit_Case_05_Plant_Monitoring_Device_CN/)   
[Micro:bit小小发明家课程06:入侵检测](/Micro_bit_Tinker_Kit_Case_06_Intruder_Detection_CN/)   
[Micro:bit小小发明家课程07:喂鱼器](/Micro_bit_Tinker_Kit_Case_07_Fish_Feeder_CN/)  
[Micro:bit小小发明家课程08:运动检测](/Micro_bit_Tinker_Kit_Case_08_Motion_Detector_CN/)  
[Micro:bit小小发明家课程09:测谎仪](/Micro_bit_Tinker_Kit_Case_09_Lie_Detector_CN/)   
[Micro:bit小小发明家课程10:乒乓球游戏](/Micro_bit_Tinker_Kit_Case_10_PADDLEBALLSUPERSMASHEM_CN/)   
[Micro:bit小小发明家课程11:躲避小行星](/Micro_bit_Tinker_Kit_Case_11_Avoid_Asteroids_CN/)   
[Micro:bit小小发明家课程12:遥控小车](/Micro_bit_Tinker_Kit_Case_12_Remote_Control_Everything_CN/)  
[Micro:bit小小发明家课程13:micro:bit小车](/Micro_bit_Tinker_Kit_Case_13_Micro_Bit_Car_CN/)   
[Micro:bit小小发明家课程14:抛煎饼游戏](/Micro_bit_Tinker_Kit_Case_14_Flipping_Pancakes_CN/)   
[Micro:bit小小发明家课程15:跑迷宫游戏](/Micro_bit_Tinker_Kit_Case_15_Maze_Runner_CN/)   
[Micro:bit小小发明家课程16:速算游戏](/Micro_bit_Tinker_Kit_Case_16_QUICK_MATHS_CN/)   
[Micro:bit小小发明家课程17:猜音调游戏](/Micro_bit_Tinker_Kit_Case_17_Pitch_Perfect_CN/)   
[Micro:bit小小发明家课程18:手指灵敏度游戏](/Micro_bit_Tinker_Kit_Case_18_Finger_Dexterity_CN/)   
[Micro:bit小小发明家课程19:电子水平仪](/Micro_bit_Tinker_Kit_Case_19_Electric_Spirit_Level_CN/)   
[Micro:bit小小发明家课程21:飞行的小鸟游戏](/Micro_bit_Tinker_Kit_Case_21_Flappy_Bird_CN/)   
[Micro:bit小小发明家课程22:摩尔斯代码信息传输](/Micro_bit_Tinker_Kit_Case_22_Wire_Transmission_CN/)   
[Micro:bit小小发明家课程23:贪吃蛇游戏](/Micro_bit_Tinker_Kit_Case_23_Snake_Game_CN/)   
