## 基于 5GNR 的室内无线动作感知的端到端解决方案

现有的无线感知研究主要聚焦于WiFi，而基于5GNR的研究的感知demo则非常少。据我了解，目前在权威期刊中发表的利用5GNR进行人体活动感知的论文仅有IEEE的一篇文章，且相关的代码与实现并未开源。

为了可以充分利用5GNR的灵活、多天线特点以及探究未来通感一体化的发展，本项目基于OpenAirInterface5G的RAN，构建了一套使用SRS信号进行室内人体活动感知的方法，可以实现10ms以内的实时人体活动感知，在六分类任务中达到了99.9%以上的识别准确率。

本项目的开源部分的代码遵循MIT协议，任何人都可使用、转发、商业用途。以下是本项目的部分实际运行时的展示：

- 跌倒检测的展示。在这个Demo中，SRS-Front的可视化平台中右侧部分显示的内容为跌倒/非跌倒的状态指示，绿色的标记即为非得到，红色的警铃符号则为跌倒。该Demo展示了在多个角度、不同跌倒方式都可被准确识别。

<video controls src="https://github.com/Dafeigy/5GNR-indoor-sensing/raw/refs/heads/main/videos/FallDetect.mp4" title="跌倒检测"></video>


- 用于动作游戏中的动作识别演示。在这个demo中，人物将执行出拳、左右移动、下蹲、踢腿、精致战力的动作，以对应格斗游戏中的人物操作。

<video controls src="https://github.com/Dafeigy/5GNR-indoor-sensing/raw/refs/heads/main/videos/ActionControl-SFV.mp4" title="SFV-control"></video>


同样的还有在驾驶游戏中使用其他自定义的动作进行训练并进行感知的demo，在这里选择了赛博朋克2077进行展示：

<video controls src="https://github.com/Dafeigy/5GNR-indoor-sensing/raw/refs/heads/main/videos/2077.mp4" title="2077"></video>

感知算法是有效的。我们在H3C的基站上应用了相同的算法，也可实现对应的动作识别，如下所示：


本项目的相关工作荣获索尼2023年 IISC Ownership Award奖项，并接受了中央电视台旗下的中国国际电视台的[采访](https://news.cgtn.com/news/2023-11-21/Sony-stays-bullish-on-China-amidst-global-uncertainties-1oTehGgblBe/index.html)：


![本人接受CGTN采访](/imgs/interview.jpg)


该项目正在与国内的大型基站设备生产商进行合作，感知算法已成功和商用基站产品接轨，并在进一步扩展、探究感知的范围与精度以及考虑新一代的基站产品研发。

本项目的工作是我在参与索尼中国研究院的横向项目中作为主导开发者进行开展的，大型会议室场景、教室场景的数据采集以及感知算法测试均在索尼中国研究院进行，除作者本人外其余测试人员均为索尼中国研究院员工。在不违背相关合作利益以及知识产权归属的条件下，仅开源如下内容：

- FreqBlock/FreqNet的代码实现。参考[SRS-Front](https://github.com/Dafeigy/FreqNet)。

- OpenAirInterface5G+Free5GC+商用UE的连接方法。参考本人[博客](https://oai.cybercolyce.cn/)文章。

- 二次开发的OAI代码。请注意OAI代码的相关使用条款。[代码仓库](https://github.com/Dafeigy/OAI-Pose)。

- 信道估计SIMD加速的实现。请查看[仓库链接](https://github.com/Dafeigy/SIMD-Learn)中的`OAI-test`分支。你可以根据你自己使用的子载波数以及UE连接时的天线配置进行对应的修改。

- Windows平台中实现“体感控制”游戏的控制的[MINI-KM](https://github.com/Dafeigy/miniKM)。

- 可视化平台[SRS-Front](https://github.com/Dafeigy/SRS-front)。

- 感知数据集中的“作者本人”的相关数据。由于数据量庞大，若需要使用作者本人的数据可联系作者：[cybersh1t@126.com](mailto:cybersh1t@126.com)。开源链接仅提供少量的数据供读者查看数据集样式；

- 基于[OAI采集CSI数据](https://github.com/Dafeigy/NR_ACTION)、[数据采集处理脚本](https://github.com/Dafeigy/NR-ACTION-data)等杂项内容。

请注意：本文工作一开始并未有开源计划，因此commit多有不规范不恰当之处，请多多包涵。作者不再通信领域进行研究，因此决定把这些工作公开以帮助后续研究人员加速相关研究，促进通信事业的发展，但相应的作者不会维护这些代码。如果有需要更进一步了解本项目的商业合作或参观考察，可联系索尼中国研究院(北京)进行洽谈。在此感谢索尼中国研究院的诸位领导与同事的支持与合作。

## 如果要复现本文工作需要怎么做？

本项目分为三个阶段进行：

- 搭建Free5GC（或其他核心网）+ OAI RAN + 商用UE的实验平台。参考本人[博客](https://oai.cybercolyce.cn/)文章：[OAI环境配置](https://oai.cybercolyce.cn/OAI-Intro-and-setup/)、[Free5GC](https://oai.cybercolyce.cn/Free5GC-installation-guide/)、[Free5GC+OAI RAN部署](https://oai.cybercolyce.cn/free5gc+OAI-gNB+OAI-nrUE/)。

- 修改OAI RAN的相关代码。

- 在实验场地中收集数据并训练模型，并使用数据处理脚本对数据进行处理。

- 在SRS-Front加载感知模型并进行相应的推理，或使用MINI-KM对游戏进行“体感控制”。

## 关于我

本科就读于天津大学通信工程专业，硕士就读于北京科技大学信息与通信工程专业。伪全栈工程师，熟练使用C/C++/C#/Python/Matlab/R/Vue/Flask/TailwindCSS，目前正在学习Rust/Golang/WASM。开源平台收获近百Stars，PR超20。业余兴趣是高性能计算与分布式系统的架构设计，以及工业设计、嵌入式软硬件开发。参与过多个项目的工程实现，列举部分：

- 广州某私募基金，量化交易系统开发。负责高并发的交易请求的核心处理模块的架构设计、核心代码编写以及测试。

- 广州某私募基金，量化策略研发。根据2007年至2024年9月国内全部交易所的市场行情分析构建钓鱼单策略。

- 索尼中国研究院，通信感知一体化demo研发（本项工作）。

- 索尼中国研究院，通信感知一体化某专利代码实现（未公开工作）。

- xx省电力设计研究院，xx大数据平台数据分析与xx运行报告自动化生成。

