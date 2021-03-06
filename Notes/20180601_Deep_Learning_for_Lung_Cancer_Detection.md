# [深度学习在医疗中的应用--肺结点检测]()

__肺结节检测，就是利用大数据驱动的人工智能于肺癌早期诊断中，让计算机自动、快速、准确的从病人肺部CT扫描序列中发现疑似结节位置和估计肺结节大小，提高检测速度和检测的准确率，以降低肺癌早期筛查的成本，从而挽救更多患者的生命。__

![](https://pic3.zhimg.com/80/v2-aa94817f9b0b8bc24f98b64953f8abe4_hd.jpg)

据国家癌症中心公布数字显示，_中国2013年恶性肿瘤发病率为270.59/10万，死亡率为163.83/10万，而肺癌在所有恶性肿瘤发病及死亡中均占首位——我国每年约59.1万人死于肺癌_。而肺癌生存率与首次确诊时的疾病阶段高度相关：由于早期肺癌多无明显症状，导致肺癌临床确诊时往往已达中晚期，治疗费用高但效果不佳。因此，对肺癌的早期检测和早期诊断就显得尤为重要。胸部CT放射影像技术，是肺癌早期筛查的有效手段。但是由于CT扫描影像数量多（一次CT扫描影像通常在200张以上），医生诊断所需时间长，加上工作量巨大，容易疲劳，人工误差不可避免； __当前，大数据与人工智能等前沿技术在医疗领域应用已经成为一种趋势，将大数据驱动的人工智能应用于肺癌早期诊断中，不仅可以挽救无数患者的生命，而且对于缓解医疗资源和医患矛盾也有重大意义——人工智能成为新的选择__。

#### 挑战及突破
基于人工智能的肺结节检测方法，存在一些列的挑战：__结节模态多，早期的结节小（小于10mm），跟周围血管组织区别小，传统手动特征+机器学习的方法和用于自然图像的深度学习网络通常难以凑效__。

后来，有学者把深度学习算法应用到肺结节检测算法中，检测性能获得了明显提升。这类算法通常分为两步：__先通过分割或检测模型生成包含大量假阳性结果的候选集；再通过分类的方法降低假阳性率__。但是这类两步算法训练过程超参数多，训练繁琐。

iDST-VC团队创新性地采用了单步流程：__使用单个深度神经网络对病人的CT序列进行处理，直接输出检测到的肺结节位置和大小__。相比与两步流程，单步流程有三个优点：
1. 单步流程的整个模型可以实现端到端的训练，更加符合现代深度学习的思想，从而效果更优；
2. 基于单步流程的系统更加简单快速，无论是模型的训练还是预测，速度都要远远快于基于两步流程的方法；
3. 单步流程涉及到超参数更少，系统更加鲁棒，对样本的适应性更强。

具体到模型结构设计上：_针对CT切片特性，采用多通道、异构三维卷积融合算法、有效地利用多异构模型的互补性来处理和检测在不同形态上的肺结节CT序列；同时使用了带有反卷积结构的网络，提高对不同尺度肺结节的敏感性。最后还采用了多任务学习的训练策略，模型组合等策略，最终提高了检测的准确度和效率_。

#### 如何做肺结节检测？
1. 数据准备——大量经过影像科医生标注的肺结节CT影像图片来训练算法，标注出可疑位置，大小，良恶性以及可能的预后情况，影像图片背后的患者基础信息，例如性别，年龄，基础疾病，家族史，吸烟史等也能用于提高算法的能力。
2. 智能算法——使用大量经过影像科医生标注的CT影像图片训练肺结节检测模型，通过深度学习算法学习肺结节的内在特性，经过肺部区域提取、肺结节分割和肺结节分类等步骤，系统自动给出肺结节的位置，大小和置信度。
3. 数据应用——该辅助诊断模块应用于院内PACS系统，医生工作站，Dicom阅读器等，实时为医生诊断提供智能辅助，同时根据该患者在院内后续的检查／治疗（例如病理切片结果，手术预后等）结果，不断自我纠正，备注，以及学习，以积累更多的“经验”。

从肿瘤的发生规律来看，原发的肿瘤以单个多见，所以多发的结节恶性的风险比单个的结节要小，但这并不代表就没有恶性的概率。事实上，通过X光胸片基本发现不了早期肺癌，目前对肺癌最精准的筛查方法是低剂量高分辨螺旋CT。

#### 相关比赛
##### LUNA16比赛冠军
LUNA16（https://luna16.grand-challenge.org）比赛是国际上权威的肺结节检测比赛，大赛要求我们对888份肺部CT样本进行分析，寻找其中的肺结节。但是LUNA16比赛的CT影像层厚都不超过2.5mm，而现实场景中5mm和10mm层厚的CT影像大量存在，对技术提出了更大的挑战。我们还在继续优化CT肺结节智能检测引擎，进行算法创新，让肺结节检测技术能更好的用于实际场景中。

