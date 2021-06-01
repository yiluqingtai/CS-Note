## 5月28日

1、[webRTC的标准与发展 (juejin.cn)](https://juejin.cn/post/6967159163633795103)

（1）浏览器将音视频处理和传输的复杂性的大部分从三个主要API中抽象出来：

`MediaStream`：获取音频和视频流

`RTCPeerConnection`：音频和视频数据的通信

`RTCDataChannel`：任意应用程序数据的通信

（2）WebRTC通过UDP传输其数据。但是，UDP只是一个起点。要使浏览器中的实时通信成为现实，它需要花费比原始UDP多得多的费用。

（3）WebRTC体系结构由十几种不同的标准组成，涵盖了应用程序和浏览器API，以及使其工作所需的许多不同的协议和数据格式：

Web实时通信（WEBRTC）W3C工作组负责定义浏览器API。

Web浏览器中的实时通信（RTCWEB）是IETF工作组，负责定义协议，数据格式，安全性和所有其他必要方面，以实现浏览器中的对等通信。

（4）实现低延迟，对等传输是一项不平凡的工程挑战：NAT遍历和连接性检查，信令，安全性，拥塞控制以及无数其他细节需要处理。

2、[硬货专栏 ｜深入浅出 WebRTC AEC（声学回声消除） (qq.com)](https://mp.weixin.qq.com/s/iq6EWCQHoYTtAwZBzs8tYA)

（1）音频方面熟知的 3A 算法（AGC: Automatic gain control; ANS: Adaptive noise suppression; AEC: Acoustic echo cancellation）。

（2）文章结构：回声的形成，回声消除的本质，信号处理流程，线性滤波，非线性滤波，延时调整策略，总结与优化方向。

（3）回声如何形成和回声消除的本质的讲得比较详细，配合图观看。

（4）后面滤波部分较复杂，还没来得及仔细看。

## 6月1日

1、[新的Google Lyra音频编解码器对实时视频流意味着什么？ (juejin.cn)](https://juejin.cn/post/6968264795787100174)

（1）介绍了一种新的音频编解码格式Lyra，能在3kbps的码率下提供可通信的音频流。

（2）Duo是谷歌开发的一款视频聊天应用，不过好像不太流行。

（3）通过将算法处理限制在300hz到18khz之间的全部或部分声波频率，新旧语音编解码器都比支持人类可听到的全范围声音的音频编解码器具有更高的带宽效率。

（4）视频流中使用最广泛的音频编解码器——高级音频编码(AAC)，通常覆盖0至96 kHz的频率范围，通过使用低频增强(LFE)、用于环绕声和其他高级声学中使用的低音箱馈源，可将频率范围扩展至120khz。

（5）AAC被纳入H.264/AVC标准，在使用48 kHz编码采样率的典型立体声设置时消耗带宽为96 kbps，尽管纯音乐应用程序通常以更高的采样率使用AAC，码率一直延伸到512 kbps。相比之下，在WebRTC流媒体通信（包括Duo的）中使用最广泛的下一代语音编解码器Opus，仅以32 kbps的速度就能近乎完美地复制语音，并以低至6 kbps的码率提供可行的语音通信。

（6）包括 Lyra 和 Opus 在内的许多语音编解码器在带宽受到严重限制下，可以通过将声音复制限制在300hz到8khz甚至500hz到3khz的低频范围内。即使是听起来很糟糕的语音，也足以传达可理解的内容。这些频率范围可以将可理解语音使用的最小码率降低到3 kbps以下水平。

（7）Red5 pro是一款流媒体服务器，支持RTMP, RTSP, HLS, Websocket等协议。