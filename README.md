# opencv-samples
### 《OpenCV 3 计算机视觉：Python语言实现》示例代码注释版

# 思维导图
![OpenCV](https://github.com/baiwen1979/opencv-samples/raw/master/images/OpenCV.png)

# 内容笔记
## 深度估计与分割
### 深度估计
* 使用立体图像和普通摄像头
    * 极几何

            跟踪从摄像头到图像上每个点的虚线，然后在第二张图像做同样的操作，并根据同一个物体对应的线的交叉来计算距离
    * 立体视觉

            从同一物体的两张不同图像提取三维信息
    * StereoSGBM算法
* 使用深度摄像头
    * 深度图（灰度）
    * 点云图（彩色）
        * B对应x(右)
        * G对应y(上)
        * R对应z(深度)
    * 视差图（灰度）
    * 有效深度掩模
### 图像分割
* GrabCut算法
    * 步骤
        * 1）在图片中定义含有物体的矩形
        * 2）矩形外的区域被自动认为是背景
        * 3）对于用户定义的矩形区域，用背景中的数据来区别它里面的前景和背景区域
        * 4）用高斯混合模型（GMM）对背景和前景建模
        * 5）图像中的每个像素都被看作通过虚拟边与周围像素相连接，而每条边都有一个属于前景或背景的概率，这基于它与周围像素颜色上的相似性
        * 6）每一个像素与一个前景或背景节点连接
        * 7）节点完成连接后，若节点之间的边属于不同终端（前景或背景），则会切断它们之间的边，这就能将图像各部分分割出来
* Watershed分水岭算法
## 图像处理
### 简单形状检测
* 线段检测
* 圆检测
### 傅立叶变换
* 高通滤波器（High Boost Filter, HPF）
* 低通滤波器（Low Pass Filter, LPF）
### 边缘检测
* 边缘检测滤波函数
    * Laplacian(), 拉普拉斯调和滤波器
    * Sobel(), 索贝尔边缘检测滤波器
    * Scharr()滤波器
* 模糊滤波函数
    * blur(), 简单算术平均模糊
    * medianBlur, 中值模糊
    * GaussianBlur, 高斯模糊
* Canny边缘检测
### 色彩空间
* 灰度
* HSV
* BGR
### 轮廓检测
* 边界框
* 最小矩形区域
* 最小闭圆
* 凸轮廓
### 卷积核
* 即权值矩阵：决定如何通过临近像素点来计算新的像素点
* 即卷积矩阵：对一个区域的像素做调和（mix up）或卷积运算
## 神经网络
### 人工神经网络(ANN)
    ANN是一个统计模型。
    统计模型是一对元素：空间S（观测数据集）和概率P，其中P是S的近似分布
    ，该分布函数可以产生一组与S非常相似的观测结果
    ANN模型来自复杂的现实，简化该模型，并推导出函数，进而以数学的形式（近似）表示现实的统计模型
* 神经元
        最基本的运算单元或节点，每个神经元都能够“近似”生成输入的函数。
* 感知器
        感知器就是一个接受许多输入并输出一个值的函数
    * 输入神经元

            各层神经元之间彼此连接。
    * 权重

            每个神经元的权重（数值参数）定义了与其他神经元连接的强度。
            权重是“自适应”的，可以根据学习算法及时调整
    * Sigmoid函数

            Sigmoid函数用来指示该函数输出的值为0或1。
            判断条件为一个阈值，如果输入的权重和大于某一阈值，感知器输出1，否则为0
* 网络结构
    * 输入层
    * 隐藏层
    * 输出层
* 学习算法
    * 监督学习（分类）
    * 非监督学习（聚类）
    * 强化学习
* 示例：动物分类
* 训练周期
        训练周期表示训练数据的一次迭代，然后对数据进行分类测试，若预测的正确率不够，则调整网络参数，进行下一轮迭代，直到训练收敛。
        所谓收敛，是指增加迭代次数不再（显著）提高结果的准确性
### 手写数字识别
* 1、定制训练数据
    * 单个数字图像
    * 灰度图像
    * 大小相同
    * 训练样本与预期分类同步
* 2、设置初始参数
    * 输入层（28X28个输入节点）
    * 隐藏层（50～60个节点）

            根据数据量的大小来增加隐藏层的大小，但超过一定程度，增加大小没有优势。
            隐藏层神经元越多，网络训练时间越长
    * 输出层（10个节点，对应10个数字）
* 3、迭代次数
* 4、激活函数：Sigmoid
* 5、训练算法：弹性反馈
        弹性反馈，即Resilient Back Propagation，RPROP）
* 6、终止条件(TermCriteria)：迭代次数20次
## 人脸检测和识别
### 人脸检测
* 基于Haar的人脸检测
    * 特征
        * 级联的尺度不变性
        * 描述相邻图像的对比模式
            * 边
            * 顶点
            * 线
    * Haar分类器
    * Haar跟踪器
### 人脸识别
* 先训练后识别
* 置信度
* 过程
    * 1. 生成人脸识别样本图像（训练集）
        * 样本图像是灰度格式，后缀为.pgm
        * 样本图像形状为正方形
        * 图像大小要一样，如200x200
    * 2.选择算法
        * Eigenfaces算法

                通过PCA识别某个训练集上（人脸数据库）的主成分，并计算出训练集相对于数据库的发射程度，并输出一个值。该值即为人脸数据库和检测到人脸之间的差别，0为完全匹配
        * Fisherfaces算法

                基于PCA，更复杂，计算量更大，但更准确
        * Local Binary Pattern Histogram（LBPH）算法

                LBPH粗略地将检测到的人脸分成小单元，并将其与模型中的对应单元进行比较，对每个区域的匹配值产生一个直方图。LBPH是唯一允许模型样本人脸和检测到的人脸在形状、大小上可以不同的人脸识别算法。
    * 3. 准备样本数据（CSV文件）
    * 4. 加载数据并识别人脸
## 图像检索
### 特征检测算法
* Harris：用于检测角点
* SIFT：用于检测斑点
        SIFT是DoG和SIFT的组合
* SURF：用于检测斑点
        SURF是快速Hession和SURF的结合
* FAST：用于检测角点
        FAST：Features from Accelerated Segment Test
        FAST算法会在像素周围绘制一个圆，该圆包括16个像素，然后，FAST会将每个像素与加上一个阈值的圆心像素进行比较，若有连续、比加上一个阈值的圆心的像素值还亮或暗的像素，则可认为圆心是角点
* BRIEF：用于检测斑点
        BRIEF：Binary Robust Independent Elementary Features
        BRIEF不是特征检测算法，它只是一个描述符
        关键点描述符是图像的一种表示，可以作为特征匹配的一种方法
* ORB：带方向的FAST和旋转不变性的BRIEF算法
    * 向FAST增加一个快速、准确的方向分量
    * 能高效计算带方向的BRIEF特征
    * 基于带方向的BRIEF特征的方差分析和相关性分析
    * 在旋转不变性条件下学习一种不相关的BRIEF特征
### 特征匹配算法
* Brute-Force：暴力匹配算法
        暴力匹配方法是一种描述符匹配算法，该方法会比较两个描述符，并产生匹配结果的列表。
        该算法基本上不进行优化，只是将第一个描述符的所有特征和第二个描述符的特征进行比较，每次比较都会给出一个距离值，而最好的比较结果会被认为是一个匹配
* KNN：K-最近邻匹配算法
* FLANN：近似最近邻快速库
        FLANN：Fast Library for Approximate Nearest Neighbors
### 特征定义
    特征即有意义的图像区域，该区域具有独特性或易于识别性。
    角点及高密度区域是好特征，而大量重复的模式或低密度区域则不是好的特征
    边缘可以将图像分为两个区域，因此也可以看作好的特征
    斑点，与周围有很大差别的图像区域，也是有意义的特征
### OpenCV特征检测
* cornerHarris()函数
        是一个角点检测函数，其第三个参数限定了Sobel算子的中孔，定义了角点检测的敏感度，其取值必须是介于3和31之间的奇数。Sobel算子通过对图像行、列的变化来检测边缘，Sobel算子会通过核（kernel）来完成检测。
* SIFT对象：SIFT_create()
        SIFT：即尺度不变特征变换（Scale-Invariant Feature Transform），是一种与图像比例无关的角点检测算法，该函数会对不同的图像尺度（尺度不变特征变换）输出相同的结果。
        SIFT本身并不检测关键点，而是通过一个特征向量来描述关键点周围区域的情况。
        SIFT对象使用DoG检测关键点，并对每个关键点周围的区域计算特征向量
* SURF对象：SURF_create()
        SURF采用快速Hessian算法检测关键点，并提取特征
* BFMatcher对象
        Brute-Force暴力匹配方法
## 目标检测与识别
### 目标检测
    目标检测：确定图像的某个区域是否含有要识别的对象
* 创建目标检测器
    * SVM

            SVM：支持向量机。给支持向量机提供一组特征，就可以使用复杂算法来分类训练数据，该模型能预测新输入的数据属于哪一类
    * BOW

            BOW：Bag Of Word, 即词袋，用来在一系列文档中计算每个词出现的次数，然后，用这些次数构成向量来重新表示文档
        * 实现步骤
            * 1、 取一个样本数据集
            * 2、 对数据集中的每幅图像提取描述符（SIFT，SURF等）
            * 3、 将每一个描述符都添加到BOW训练器中
            * 4、将描述符聚类到K簇中（K-means聚类）
        * 视觉单词
* 训练目标检测器
    * 训练步骤
        * 1、给定训练图像，提取特征
        * 2、基于这些特征到最近簇心的距离实现量化，以形成直方图
        * 3、识别视觉单词并在图像中对其定位
    * BagOfWordsKMeansTrainer
* 示例：汽车检测
        扫描图像，并用矩形框住检测到的汽车
    * 执行过程
        * 1、获取一个训练数据集
        * 2、 创建BOW训练器并获得视觉词汇
        * 3、 采用词汇训练SVM
        * 4、尝试对测试图像的图像金字塔采用滑动窗口进行检测
        * 5、对重叠的矩形使用非最大抑制
        * 6、 输出结果
    * 项目结构
        * SVM训练的模型
        * 非最大抑制函数
        * 图像金字塔
        * 滑动窗口函数
### 主要技术
* 梯度直方图(Histogram of Oriented Gradient)
        HOG是一个特征描述符。HOG不是基于颜色值而是基于梯度来计算直方图的。HOG所得到的特征描述符能够为特征匹配和目标检测提供重要信息。
    * 特征提取

            1、将图像分成16X16的像素块的小单元
            2、每个单元按八个方向（N，NW，W，SW，S，SE，E和NE）所计算的颜色梯度进行视觉表示
            3、每个单元的八个值就为直方图
            4、将直方图外推（extrapolation）成描述符
                 (1) 计算每个单元的局部直方图
                 (2) 将这些单元合成较大的块(block)
                 (3) 按块构成特征向量，便于归一化，同时减少光照和阴影的影响
    * 两个问题
        * 尺度问题(Scale)
        * 位置问题(Position)
* 图像金字塔(Image  Pyramid)
        图像金字塔是图像的多尺度表示，有助于解决不同尺度下的目标检测问题。
        此外，还要通过训练得到目标分类器，训练所用的图像数据库由正匹配和负匹配构成
    * 构成过程
        * 1、获取图像
        * 2、使用任意尺度的参数来调整（缩小）图像的大小
        * 3、平滑图像（高斯模糊）
        * 4、若图像比最小尺寸还大，重复（1～4）
    * 级联分类器
* 滑动窗口(Sliding Window)
        滑动窗口：包括图像中要移动部分的检查以及使用图像金字塔对各部分进行检测。
        为了在多尺度下检测对象
        滑动窗口通过扫描较大图像的较小区域来解决定位问题，进而在同一图像的不同尺度下重复扫描
        需要将每幅图像分解成多个部分，然后丢掉那些不太可能包含对象的部分，并对剩余部分进行分类
    * 区域重叠问题
    * 非最大抑制问题

            非最大抑制算法：
            （1）一旦建立图像金字塔，为了检测目标，可采用滑动窗口来搜索图像
            （2）收集当前所有含有目标的窗口，并得到有最高响应的窗口W
            （3）消除所有与W有明显重叠的窗口
            （4）移动到下一个有最高响应的窗口，在当前尺度下重复上述过程
    * SVM：支持向量机
## 目标跟踪
    目标跟踪是对摄像头视频中的移动目标进行定位的过程。
### 检测移动目标
    即识别视频帧中那些可能包含移动目标的区域
### 基本运动检测
    计算帧之间的差异，或考虑“背景”帧与其他帧之间的差异
### 背景分割器
    背景分割器(BackgroundSubstractor)是一个功能完全的类，该类不仅执行背景分割，而且能构通过机器学习的方法提高背景检测效果，并提供将分类结果保存到文件的功能
    BackgroundSubstractor专门用于视频分析，该类会对每帧的环境进行“学习”，可按时间推移方法提高运动分析的结果
    BackgroundSubstractor可以计算阴影
* KNN (K-Nearest Neighbors)
* MOG2 (Mixture Of Gaussians)
* GMG (Geometric Multigid)
### 均值漂移(MShift)
    即Meanshift，是一种目标跟踪算法，该算法寻找概率函数离散样本的最大密度（感兴趣的图像区域），并且重新计算在下一帧中的最大密度，该算法给出了目标移动的方向
    重复进行该计算，直到与原始中心匹配，或者在连续迭代计算后中心保持不变，，即收敛
    均值漂移在跟踪视频中感兴趣区域时非常有用，可以动态地开始跟踪（和停止跟踪）视频的某些区域。
    如，采用训练好的SVM进行目标检测，然后开始使用均值漂移跟踪检测到的目标
* 彩色直方图(calcHist函数)
        彩色直方图是指图像的颜色分布。其X轴是色彩值，Y轴是相应色彩值的像素数量
* 直方图反向投影(calcBackProject)
        直方图反向投影(calcBackProject)	可计算直方图，并将其投影到一幅图像上，其结果是概率，即每个像素属于起初那幅生成直方图的图像的概率。
        因此，calcBackProject给出的是一个概率估计：一幅图像等于或类似于模型图像(model image)的概率
### 连续自适应均值漂移(CAMShift)
### 卡尔曼滤波器
    卡尔曼滤波器会对含有噪声的输入数据流进行递归操作，并产生底层系统状态（如视频流中的位置）在统计意义上的最优估计
* 卡尔曼算法的两个阶段
    * 预测阶段

            在此阶段，卡尔曼滤波器使用由当前点计算的协方差来估计目标的新位置
    * 更新阶段

            此阶段，卡尔曼滤波器记录目标的位置，并为下一次循环计算修正协方差
### 示例：行人跟踪

