```
├───calculator 手写算式计算器
├───recognization 手写数字识别
└────train   模型训练
```
因为一直加不上vs的tools for ai就直接用pytorch+onnx了。
* train  
  模型训练使用的数据集是mnist+[哈工大周雄,钟宇宏,杨帆,吴沛钢](https://blog.csdn.net/qq_34919953/article/details/81112313)大作业的数据集。这里我把他们的数据和mnist合并，并重新shuffle了一遍。但是数据集的质量不太高，有很多噪点。模型是一个简单的CNN，训练20个epoch后导出onnx格式。输入是一个叫"input"的(1,1,28,28)向量。
  
  损失函数为交叉熵损失函数。下图为训练和验证集的loss曲线（蓝色为验证集，图中两条曲线几乎重合了）。
  
  使用的网络：
  
  >CNN(
  >  (layer1): Sequential(
  >    (0): Conv2d(1, 16, kernel_size=(5, 5), stride=(1, 1), padding=(2, 2))
  >    (1): BatchNorm2d(16, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)
  >    (2): ReLU()
  >    (3): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  >  )
  >  (layer2): Sequential(
  >    (0): Conv2d(16, 32, kernel_size=(5, 5), stride=(1, 1), padding=(2, 2))
  >    (1): BatchNorm2d(32, eps=1e-05, momentum=0.1, affine=True, track_running_stats=True)
  >    (2): ReLU()
  >    (3): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  >  )
  >  (fc): Linear(in_features=1568, out_features=16, bias=True)
  >)
  
  最后测试集的交叉熵损失为-23.2985, 准确率为17733/17762 (100%)
  
  验证集的交叉熵损失为 -23.3086，准确率为14951/15086 (99%)
  
  ![9e0de659-763c-4daf-86c0-5f7de8815db4](asset/9e0de659-763c-4daf-86c0-5f7de8815db4.png)
  
* recognization  
  在官方教程“手写数字识别”的基础上稍微修改了一下。效果如下：  
  <img src="asset\20211231172137.jpg" width = "300" height = "200" alt="2" /> <img src="asset\20211231172154.jpg" width = "300" height = "200" alt="+" />  <img src="asset\20211231172626.jpg" width = "300" height = "200" alt="+" />  
  虽然训练效果不错，但是实际使用时效果不是很好（比如1,+）  
  使用vs编译或者执行目录下exe文件可使用
  
* calculator
   在官方教程“手写算式计算器”的基础上稍微修改了一下。效果如下:
    <img src="asset\example.jpg"  height = "200" alt="2" />  
  使用vs编译或者执行目录下exe文件可使用