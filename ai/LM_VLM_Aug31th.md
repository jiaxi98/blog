# Asymmetry of the human perceptral system
*31st Aug, 2025*

人类的认知系统具有高度的不对称性：人类生活中绝大多数的**信息获取(input)**来自于视
觉信号，但是人类主要的**信息输出(output)**方式则是oral和text-based。更准确的说
oral-based输出绝大多数出现在人与人的交流中，并且可以视作另一种形式的text-based
输出。为什么人类没有选择这种传输信息密度更高的图像作为信息输出的主要途径呢？

回顾人类文字发展的历史，其实早期的人类文字恰恰采取了图像的形式(象形文字)。文字进化
的路线也是在不断化繁为简，把原始图像里的信息逐渐抽象成越来越简洁容易书写
的特征(这似乎也是某种人力的feature selection?)。所以我们是否可以理解为，
text-based相较于image-based的信息有着信噪比高的优势，最终成为了人类智能的载体。

*Claude:人的大脑是一个很强的decoder，所以encoder只需要发送高度压缩抽象的信号即可完成通信；这也反映出来一个信号所包含的信息量等于decoder所含信息量和其本身信息量的总和。另一个比较重要的概念是可组合性，它涉及信息的编码效率和计算复杂度。text的可组合性远远大于image，从编码效率上看：避免了大量的重复信息(如视频中不变的背景)，这正是Kolgomorov complexity的重要体现；而从传输效率来看，文字的离散性和组合规则提供了自然的纠错机制---接收者可以用语法和语义约束来推断正确信息。人类自然语言的进化机制恰恰满足了minimal desciption length(MDL)的原理。*

另一方面，text-based和image-based的区别导致了二者数据量的显著区别(这一点或许在
AIGC时代有所减弱？)，也进而造就了现阶段Language Molel (LM)和Vision
Languange Model (VLM)不同的发展速度---LM的reasoning已经达到了
[IMO金牌](https://arxiv.org/abs/2507.15855)的级别，但是VLM的reasoning连一些基本的
视频问答还不能尽如人意，当然从目前VLM的generative model和reasoning model
截然不同的框架也可窥见。同时，目前大火的AI Agent几乎完全是基于text-based tool
interface，譬如web search、bash command等等，很难想象一个pure VLM如何通过图
片来进行tool call。

但正如人类语言的发展完全是人类的偏好选择的产物，或许VLM的研究能帮助人类design出一
种信噪比高于自然图片的文字系统(这让我想起了《降临》的故事)？
