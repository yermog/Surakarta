# 第二阶段报告

'''cpp
代码主要实现————尹堃
少部分代码实现及报告撰写————方言诚
Finished on 2024.4.17
'''

## 1. QT项目优点简介

1. 代码具有极好的封装性与可扩展性
   - 在进入游戏与游戏过程中，我们采用了**多线程处理**，将AI/Gamer的信号通过信号槽的方式进行传递
    > **chess_window**文件中，我们通过**QThread**类创建了**mygamethread**线程，用于处理AI/Gamer的信号
   - 代码各部分结构清晰，通过**chess_window**文件将所有封装的程序执行块链接与执行
   - 后续代码的更新可以通过添加信号槽来与游戏程序链接实现

2. 代码具有极好的可读性
   - 代码中使用了大量的**中文注释**，（~~二年级的小朋友也看得懂~~）使得代码可读性极佳
   - 代码中精妙使用了**QT**的信号槽机制，使得代码执行方向与信号传递清晰，可读性好
   - 分块的代码格式与良好的封装性也使得代码可读性提高

3. **多线程处理**使得该代码有优秀的联网能力
   - 服务器端的信号可以直接通过信号槽来进行游戏计算，与客户端相独立
   - 由于信号槽的存在，信号的交换与传递十分便捷

4. 代码满足了该大作业的核心要求
   - 图形化界面设计的十分合理，界面美观，操作简单
   - 本地的PVP可以顺利进行，我们甚至也实现了**PVE,EVE**部分
   - 将其他的AI自动行棋文件加入到代码中时，代码可以通过**shared_ptr**直接运行，，对接性极强
   - 代码中使用了**多线程处理**，使得代码具有优秀的联网能力
   - 代码中使用了**QT**的信号槽机制，使得代码执行方向与信号传递清晰，可读性好
   - 代码实现了对**计时与超时**系统的自设定实现
   - 代码到处都运用了类的各项性质与优势 ~~充分证明了这是程序设计二的大作业~~

- - -
## 2. 项目内容分析

'''cpp
   概述：
   项目在上一阶段对**Surakarta**游戏规则的开发基础上进行了图形化实现，具体包括：
     - 主菜单窗口实现
     - 游戏模式选择窗口实现（**PVP or PVE or EVE**）
     - 游戏进行窗口及游戏内容实现
'''

### 2.1 主菜单窗口实现

    仅插入了一个菜单图片和自制按钮，无需多言

### 2.2 游戏模式选择窗口实现

  - 游戏模式选项分为**PVP,PVE,EVE**三种模式
  - 我们对三个按钮进行了信号槽的连接，使得三个按钮可以实现信号的传递与游戏模式的切换
  - 信号槽最终会使得我们构造的**共享指针**指向不同的玩家性质（AI or GAMER），进而实现游戏模式的选择
  
### 2.3 游戏进行窗口及游戏内容实现

1. 棋盘内容绘制
   - 使用了QT自带的Painter类
   - 通过**QPainter**类中的**drawRect**和**drawArc**绘制了棋盘
   - 棋盘通过循环绘制，如果要改为其他更大的棋盘，只需要更改循环的次数，十分便捷
   - 棋子采用了**QPixmap**类进行绘制，真实舒适

2. 规则实现及运行
   - 接入了前一阶段中设计的游戏规则
   - 通过**QTimer**来实现可调节的计时器
   - 独立写了**mygamethread**的新类，用于实现**多线程处理**
     - 解决了**PVP**模式下，**GAMER**同时进行游戏计算的问题
     - 完成了两玩家之间切换的合法性
     - 使代码具有良好的封装性
   - 各部分代码通过**QT**的信号槽机制进行连接