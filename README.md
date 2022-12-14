# [尚未完成] ThrottleStop 使用指南

**警告：**

* **超频有风险，超频时的不当操作可能会导致死机、蓝屏，严重可能会导致部件虚焊、烧毁，请考虑好再超频，超频造成的一切后果本人概不负责。**

**提示：**

* 本文使用的是ThrottleStop 9.5版本，可能与老版本界面布局不一致。
* 如有界面显示不全，请点击右下角 + 号按钮
* 每次重启都需要打开ThrottleStop来启用超频，嫌麻烦可以写一个任务计划

## 首次下载安装

[ThrottleStop下载](https://www.techpowerup.com/download/techpowerup-throttlestop/)

下载完解压到一个文件夹，双击ThrottleStop.exe启动。

首次运行会弹出警告，再次提醒超频后果自负

![警告](./img/Warning.png)

运行时会生成一个ThrottleStop.ini文件，这是程序的配置文件。

如果在超频时出现问题，或者想恢复原始设置，您可以尝试重命名或删除ThrottleStop.ini文件。

## 主界面

![主界面](./img/Main.png)

主界面可以简单看作左右两栏，我将从左栏 从上往下介绍：

### 主界面 - 左侧

| 界面元素           | 功能                                               | 说明                                                                                                                                                                                                                                            |
| ------------------ | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ◉  ◯  ◯  ◯  | 性能配置文件                                       | 用于在不同的使用场景中快速切换配置。                                                                                                                                                                                                            |
| ▢High Performance | 电源计划                                           | 选中后启用对应的Windows的电源计划。<br />* 自定义电源计划因中文名称会乱码。所以不要点右边的加号                                                                                                                                                 |
| ▢Clock Mod        | Clock Modulation<br />时钟频率百分比               | 使CPU或芯片组以百分比频率运行。<br />* 非必要，一般用于降频省电                                                                                                                                                                                 |
| ▢Set Multiplier   | CPU倍频                                            | 老旧功能，调整CPU倍频，在[SST](#术语)启用时不可用。<br />* 在启用SST时应该去FIVR -> Turbo Ratio Limits调整                                                                                                                                         |
| ▢Speed Shift EPP  | [Speed Shift Technology (SST)](#术语) <br />变速技术 | 右侧数字可以修改为 0-255 之间的值，其中 0 表示首选最高频率运行（受其他因素限制，如禁用睿频），255 表示首选以最低频率运行。<br />注意：某些主板需要在Bios中启用。启用“Speed Shift”后，右侧会显示绿色的SST字样。<br />* 启用时无法设置CPU倍频。 |
| ▢Power Saver      | 节能: 降频                                         | 仅当禁用睿频时可用，启用后会使CPU空闲时的时钟频率降至最低                                                                                                                                                                                       |
| ▢Disable Turbo    | 禁用睿频                                           | 选中时将禁用 CPU 的睿频。在限制功耗和温度的时候非常管用。                                                                                                                                                                                       |
| ▢BD PROCHOT       | Bi-directional Processor Hot<br />温度墙           | CPU、显卡或其他硬件过热（例如超过100 或 105C）时触发的紧急限制，降低倍频防止电脑过热烧毁，一般不建议禁用。<br />* 可能会导致CPU 低温降频                                                                                                        |
| ▢C1E              | C1 Enhanced State<br />节能: C1增强状态            | 当您的PC低负载时，它会降低频率和电压，从而减少功耗和热量。<br />* 某些人声称关闭此选项能略微提高CPU和SSD的性能                                                                                                                                  |
| ▢Task Bar         | 缩小到任务栏                                       | 缩小到任务栏，而不是隐藏到任务栏图标。                                                                                                                                                                                                          |
| ▢Log File         | 启用日志文件                                       | 将运行日志写入到文件中，以便于在日志中分析性能限制因素。                                                                                                                                                                                        |
| ▢More Data        | 更多数据                                           | 更快的数据采样，从每秒 1 次加快到每秒 8 次。                                                                                                                                                                                                  |

### 主界面 - 右侧

* **上方**显示的是CPU信息，分别为**电压**、**倍频x外频**、**频率**
* **中间**表格显示的是所有CPU核心的信息
  * 从上到下分别为第1~8个核心
  * 从左往右分别是倍频、负载、最大频率百分比、核心温度、Max最高温度)/Min(最低温度)
* **下方**
  * 第一行是CPU的平均负载、平均温度、最高温度
  * 第二行是封装的实时功耗、最大功耗
  * 第三行 Limits 菜单，右侧在撞温度墙后会显示红色HOT、PROCHOT 97°C字样
  * 最后一行是FIVR菜单、TPL菜单、C State菜单，以及Clear按钮(清除统计数据)

### 主界面 - 最下方一排

| 界面元素         | 功能     | 说明                                                                   |
| ---------------- | -------- | ---------------------------------------------------------------------- |
| Save             | 保存     | 将当前配置保存到ThrottleStop.ini                                       |
| Options          | 选项     | 配置ThrottleStop界面选项                                               |
| Turn Off/Turn On | 开关     | 开关ThrottleStop，点击Turn Off关闭ThrottleStop功能                     |
| TS Bench         | 测试     | 简单的跑分测试，时间越短越好                                           |
| Battery          | 电池监视 | 在Option中勾选Battery Monitoring启用，监视电池信息，点击切换监视的数据 |
| GPU              | 显卡监视 | 在Option中勾选Nvidia GPU/AMD GPU启用，监视显卡信息，点击切换监视的数据 |

## 术语

1. SST - Speed Shift Technology - SpeedStep® 技术：允许系统动态调整处理器电压和内核频率，从而降低平均功耗和热量产生。

## 参考文献

1. [ThrottleStop Guide](https://www.ultrabookreview.com/31385-the-throttlestop-guide/ "ThrottleStop指南")
2. [What does Intel Speed Shift do?](https://forums.tomshardware.com/threads/what-does-intel-speed-shift-do.3574107/ "英特尔Speed Shift是用来干什么的？")
3. [What is &#34;C1E support&#34; on my AMD CPU?](https://superuser.com/questions/184569/what-is-c1e-support-on-my-amd-cpu "我AMD CPU上的&quot;C1E 支持&quot;是什么？")
4. [Processor states](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface#Processor_states "C States")
