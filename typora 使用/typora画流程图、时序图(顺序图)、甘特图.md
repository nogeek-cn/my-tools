1. 横向流程图源码格式：

   \```mermaid

   graph LR

   A[方形] -->B(圆角)

   ​    B --> C{条件a}

   ​    C -->|a=1| D[结果1]

   ​    C -->|a=2| E[结果2]

   ​    F[横向流程图]

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=2466ec608935e5dd902ca5df46c7a7f5/bd3eb13533fa828bcdba91d1f11f4134970a5a62.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=1)

2. 

   竖向流程图源码格式：

   \```mermaid

   graph TD

   A[方形] -->B(圆角)

   ​    B --> C{条件a}

   ​    C -->|a=1| D[结果1]

   ​    C -->|a=2| E[结果2]

   ​    F[竖向流程图]

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=b77421d7a16eddc426e7b4fb09dbb6a2/eac4b74543a98226767c24158682b9014a90eb47.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=2)

3. 

   标准流程图源码格式：

   \```flow

   st=>start: 开始框

   op=>operation: 处理框

   cond=>condition: 判断框(是或否?)

   sub1=>subroutine: 子流程

   io=>inputoutput: 输入输出框

   e=>end: 结束框

   

   st->op->cond

   cond(yes)->io->e

   cond(no)->sub1(right)->op

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=8ff1d0ed7ac6a7efb926a826cdfbafe9/a71ea8d3fd1f4134ffea704c291f95cad1c85e26.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=3)

4. 

   标准流程图源码格式（横向）：

   \```flow

   st=>start: 开始框

   op=>operation: 处理框

   cond=>condition: 判断框(是或否?)

   sub1=>subroutine: 子流程

   io=>inputoutput: 输入输出框

   e=>end: 结束框

   

   st(right)->op(right)->cond

   cond(yes)->io(bottom)->e

   cond(no)->sub1(right)->op

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=d901f51be7c4b7453494b716fffc1e78/03087bf40ad162d92187112e1ddfa9ec8a13cd93.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=4)

5. 

   UML时序图源码样例：

   \```sequence

   对象A->对象B: 对象B你好吗?（请求）

   Note right of 对象B: 对象B的描述

   Note left of 对象A: 对象A的描述(提示)

   对象B-->对象A: 我很好(响应)

   对象A->对象B: 你真的好吗？

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=1acff8b5dca20cf44690fedf46094b0c/3b292df5e0fe9925ff7c166238a85edf8db1718b.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=5)

6. 

   UML时序图源码复杂样例：

   \```sequence

   Title: 标题：复杂使用

   对象A->对象B: 对象B你好吗?（请求）

   Note right of 对象B: 对象B的描述

   Note left of 对象A: 对象A的描述(提示)

   对象B-->对象A: 我很好(响应)

   对象B->小三: 你好吗

   小三-->>对象A: 对象B找我了

   对象A->对象B: 你真的好吗？

   Note over 小三,对象B: 我们是朋友

   participant C

   Note right of C: 没人陪我玩

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=df59a9dfeb1190ef01fb92dffe1b9df7/32fa828ba61ea8d3a7730d369b0a304e251f58aa.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=6)

7. 

   UML标准时序图样例：

   \```mermaid

   %% 时序图例子,-> 直线，-->虚线，->>实线箭头

     sequenceDiagram

   ​    participant 张三

   ​    participant 李四

   ​    张三->王五: 王五你好吗？

   ​    loop 健康检查

   ​        王五->王五: 与疾病战斗

   ​    end

   ​    Note right of 王五: 合理 食物 <br/>看医生...

   ​    李四-->>张三: 很好!

   ​    王五->李四: 你怎么样?

   ​    李四-->王五: 很好!

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=c028fc1be7c4b7453494b716fffc1e78/03087bf40ad162d938ae182e1ddfa9ec8a13cd44.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=7)

8. 

   甘特图样例：

   \```mermaid

   %% 语法示例

   ​        gantt

   ​        dateFormat  YYYY-MM-DD

   ​        title 软件开发甘特图

   

   ​        section 设计

   ​        需求                      :done,    des1, 2014-01-06,2014-01-08

   ​        原型                      :active,  des2, 2014-01-09, 3d

   ​        UI设计                     :         des3, after des2, 5d

      	未来任务                     :         des4, after des3, 5d

   

   ​        section 开发

   ​        学习准备理解需求                      :crit, done, 2014-01-06,24h

   ​        设计框架                             :crit, done, after des2, 2d

   ​        开发                                 :crit, active, 3d

   ​        未来任务                              :crit, 5d

   ​        耍                                   :2d

   ​    

   ​        section 测试

   ​        功能测试                              :active, a1, after des3, 3d

   ​        压力测试                               :after a1  , 20h

   ​        测试报告                               : 48h

   \```

   [![typora画流程图、时序图(顺序图)、甘特图](https://imgsa.baidu.com/exp/w=500/sign=f971363a00d79123e0e094749d355917/fcfaaf51f3deb48fbfa5c7ecfc1f3a292df57837.jpg)](http://jingyan.baidu.com/album/48b558e3035d9a7f38c09aeb.html?picindex=8)

 