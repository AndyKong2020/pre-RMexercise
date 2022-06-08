# 课程设计
## 程序介绍  
  在RoboMaster比赛中，存在步兵、哨兵、英雄、工程等多个兵种，并且使用裁判系统进行自动的比赛判决，现在需要你编写一个程序，完成一个基础的裁判系统。  
  对于所有的机器人，都应该具有编号、所属队伍、血量三个基本信息，除此以外步兵和哨兵还具有17mm发射机构热量属性、英雄具有42mm发射机构热量属性，在每局比赛中，上述数据需要被存储于内存中，每个兵种具体属性如下表。  
|属性|步兵|哨兵|英雄|工程|
|:---:|:---:|:---:|:---:|:---:|
|血量|100|200|200|200|
|17mm热量上限|200|300|0|0|
|42mm热量上限|0|0|300|0|  
  
在比赛过程中，裁判系统会从标准输入读取指令，每条指令占一行，指令格式同“命令字 参数1 参数2 参数3”，具体的指令如下表所示。  
  
|命令字|参数1|参数2|参数3|示例|
|:---:|:---:|:---:|:---:|:---:|
|A 新建机器人|R/B（所属队伍）|B\S\Y\G （兵种类型） 兵种拼音第一个字母|编号 每个机器人对应一个唯一的无符号数编号|A R B 3 新建一个红方的编号为3的步兵|
|F 攻击（伤害量为负时加血）|R/B（所属队伍）|机器人编号|伤害量|F R 3 100 扣除红方3号100点血量|
|H 发射 发射弹丸为负数时视为枪口冷却，降低热量|R/B（所属队伍）|机器人编号|发射弹丸数目|H R 3 2 红方3号发射两发弹丸，每发18mm弹丸增加15点热量，每发42mm弹丸增加30点热量|  
  
  为了优化机器人生成效率，新建机器人指令加入要生成的数量这个参数，形如 A 3 R B 1 B Y 2 R G 3 ，A 后的3，代表了将创建3个机器人，后面每三个参数一组，就对应参数1 参数2 参数3  
  
  当机器人血量为0时，视为其已死亡，所有属性立即归零。  
  当机器人枪口热量超过上限时，将机器人血量归零，视为死亡。  
  在收到E指令时结束比赛，并以表格形式在标准输出输出每台机器人的各项信息。  
  
## 程序结构  
### 机器人类  
  有父类Robot，四个兵种都继承自Robot。父类Robot有以下属性：
  1. 所属队伍  采用枚举类型，红队值为0，蓝队值为1
  2. 编号  无符号整型
  3. 血量上限  整型
  4. 剩余血量  整型
  5. 武器口径  采用枚举类型，17mm值为15，42mm值为30，就是对应的热量值
  6. 热量上限  整型
  7. 目前热量  整型  
  并有以下行为：  
  1. 攻击
  2. 发射
  3. 信息输出  
  都为虚函数，在子类中定义  
  
### 裁判系统类
  裁判系统有以下属性，用于管理生成的机器人：  
  1. 机器人数量
  2. 存放
  
