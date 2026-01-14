---
permalink: /
title: "About Me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>


<style>
  .pub-tag {
    display: inline-block;
    padding: 3px 8px;
    margin-right: 8px;
    border-radius: 4px;
    font-size: 0.85em;
    font-weight: 600;
    color: white;
    vertical-align: middle;
    line-height: 1.2;
  }
  .pub-tag.streaming { background-color: #16a085; }
  .pub-tag.protocol  { background-color: #e67e22; }
  .pub-tag.arch      { background-color: #3498db; }
  
  #research-interests {
    margin-top: -1em; /* 关键！用负值抵消上方标题的下边距 */
  }
  #research-interests li {
    line-height: 1.5;   /* 调整列表项内部的行高 */
    margin-bottom: 0em; /* 调整列表项之间的间距 */
  }
</style>


***Assistant Professor (Special Research Assistant)*** \
Network Architecture and System Research Group (NASG), Network Research Center \
[Institute of Computing Technology, Chinese Academy of Sciences (ICT, CAS)](http://www.ict.ac.cn/) \
中国科学院计算技术研究所 · 网络技术研究中心 · 网络体系结构与系统课题组 \
助理研究员（特别研究助理）



---

He is currently an assistant professor (postdoctoral researcher) at ICT, CAS. He received his Ph.D. degree from ICT, CAS / [University of Chinese Academy of Sciences (UCAS)](https://www.ucas.ac.cn/) in 2024, advised by Prof. [Gaogang Xie](https://people.ucas.ac.cn/~_xie) and Prof. [Zhenyu Li](https://zhenyulee.github.io/), and his B.S. degree in Computer Science from [Hunan University (HNU)](https://www.hnu.edu.cn/) in 2016.

**Research Interest**: 
<div id="research-interests" markdown="1">
- Video Streaming: real-time communication <span class="pub-tag streaming">RTC</span>, adaptive bitrate  streaming <span class="pub-tag streaming">ABR</span>, live streaming <span class="pub-tag streaming">Live</span>, etc.
- Network Protocol: content over QUIC <span class="pub-tag protocol">QUIC</span>, multipath transmission <span class="pub-tag protocol">MP</span>, etc.
- Internet Architecture: content delivery network <span class="pub-tag arch">CDN</span>, edge collaboration <span class="pub-tag arch">Edge</span>, etc.
</div>

[[Tech Blog (In Chinese)](https://blog.csdn.net/LvGreat)] [[View of Technology (In Chinese)](https://mp.weixin.qq.com/s/XfRoXm49F5C85zWL2YsTRw?scene=2)]



## Recent News

<div style="border:1px solid #000; border-width:2px; border-color:RoyalBlue; background-color:#D2E1FF; color:#424242; border-radius: 8px; padding-right: 8px;">
  <ul>
      <li>[2026-01] 📃 Paper <i>Breath</i> accepted to <b>ACM WWW 2026</b>. </li>
      <li>[2025-09] 📃 Paper <i>Oceanus</i> and <i>LiveMap</i> accepted to <b>ACM CoNEXT 2025</b>. </li>
      <li>[2025-08] 📃 Paper <i>RLive</i> accepted to <b>ACM EuroSys 2026</b>. </li>
      <li>[2025-07] 🎓 My doctoral dissertation was awarded the Excellent Doctoral Dissertations of CAS. </li>
      <li>[2025-07] 📃 Paper <i>Co-RTV</i> accepted to <b>IEEE RTSS 2025</b>. </li>
      <li>[2025-04] 📃 Paper <i>MARC</i> accepted to <b>USENIX ATC 2025</b>.</li>
  </ul>
</div>




## Research Scope of NASG
Main studies on media transmission system (from 2021):

<table cellspacing="0" style="border: 2px solid #595959; border-collapse: collapse;">
    <!-- Title -->
    <tr style="background-color: #f8f8f8">
        <th style="border: 2px solid #595959; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6;"></th>
        <th colspan="2" style="vertical-align: middle; text-align: center; border-top: 2px solid #595959; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6;"><b>Endpoint</b></th>
        <th style="vertical-align: middle; text-align: center; border: 2px solid #595959; border-left: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6;"><b>Network</b></th>
    </tr>
    <!-- 1st Row -->
    <tr style="background-color: #e2f1da">
        <td style="vertical-align: middle; text-align: center; border-left: 2px solid #595959; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6; color: #375d23;"><b>Application<br>Layer</b></td>
        <!-- Bitrate Control -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6"><b>Bitrate Control</b><br>
        - MARC [<a href="https://www.usenix.org/conference/atc25/presentation/zhao-yuankang">ATC’25</a>]<br>
        - Schaferct [<a href="https://dl.acm.org/doi/10.1145/3625468.3652183">MMSys’24 GC No.1</a>]<br>
        - Lumos [<a href="https://ieeexplore.ieee.org/abstract/document/10246426">TMC’23</a> / <a href="https://ieeexplore.ieee.org/abstract/document/9796948/">INFOCOM’22</a>]</td>
        <!-- Buffer Management -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6"><b>Buffer Management</b><br>
        - JitBright [<a href="https://dl.acm.org/doi/10.1145/3746283">TOMM’25</a> / <a href="https://dl.acm.org/doi/10.1145/3651863.3651881">NOSSDAV’24 Best Paper</a>]</td>
        <!-- CDN Scheduling -->
        <td style="vertical-align: top; border-right: 2px solid #595959; border-bottom: 1px solid #a6a6a6"><b>CDN Scheduling</b><br>
        - RLive [EuroSys’26]<br>
        - Oceanus [<a href="https://dl.acm.org/doi/10.1145/3768983">CoNEXT’25</a>]<br>
        - LiveMap [<a href="https://dl.acm.org/doi/10.1145/3768978">CoNEXT’25</a>]<br>
        - LiveNet [<a href="https://dl.acm.org/doi/abs/10.1145/3544216.3544236">SIGCOMM’22</a>]<br>
        </td>
    </tr>
    <!-- 2nd Row -->
    <tr style="background-color: #fef4cf">
        <td style="vertical-align: middle; text-align: center; border-left: 2px solid #595959; border-right: 1px solid #a6a6a6; border-bottom: 2px solid #595959; color: #846802;"><b>Transport<br>Layer</b></td>
        <!-- Transmission Control -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 2px solid #595959"><b>Transmission Control</b><br>
        - Breath [WWW’26]<br>
        - Marten [<a href="https://www.computer.org/csdl/journal/nw/5555/01/11048990/27Oqh8Z0hb2">TON’25</a>]<br>
        - Muse [<a href="https://ieeexplore.ieee.org/abstract/document/9796880">INFOCOM’22</a>]<br>
        </td>
        <!-- Multipath Transport -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 2px solid #595959"><b>Multipath Transport</b><br>
        - Chorus [<a href="https://dl.acm.org/doi/10.1145/3636534.3649359">MobiCom’24</a>]<br>
        - Disco [<a href="https://ieeexplore.ieee.org/abstract/document/10355608/">ICNP’23</a>]<br>
        - XLINK [<a href="https://dl.acm.org/doi/abs/10.1145/3452296.3472893">SIGCOMM’21</a>]</td>
        <!-- Edge Assistance -->
        <td style="vertical-align: top; border-right: 2px solid #595959; border-bottom: 2px solid #595959"><b>Edge Assistance</b><br>
        - Co-RTV [<a href="https://www.computer.org/csdl/proceedings-article/rtss/2025/964200a189/2cTzHjeYbVC">RTSS’25</a>]<br>
        - TECC [<a href="https://www.usenix.org/conference/nsdi24/presentation/zhang-jiaxing">NSDI’24</a>]</td>
    </tr>
</table>


**Open-source projects:** \
[![Lumos](https://img.shields.io/github/stars/GreenLv/Lumos?style=flat-square&logo=github&label=Lumos&color=808080&labelColor=595959)](https://github.com/GreenLv/Lumos)
&nbsp;
[![Schaferct](https://img.shields.io/github/stars/n13eho/Schaferct?style=flat-square&logo=github&label=Schaferct&color=808080&labelColor=595959)](https://github.com/n13eho/Schaferct)
&nbsp;
[![Chorus](https://img.shields.io/github/stars/GreenLv/Chorus?style=flat-square&logo=github&label=Chorus&color=808080&labelColor=595959)](https://github.com/GreenLv/Chorus)
&nbsp;
[![Solis-WiFi-Trace](https://img.shields.io/github/stars/GreenLv/Solis-WiFi-Trace?style=flat-square&logo=github&label=Solis-WiFi-Trace&color=808080&labelColor=595959)](https://github.com/GreenLv/Solis-WiFi-Trace)
&nbsp;
[![Pensieve-retrain](https://img.shields.io/github/stars/GreenLv/pensieve_retrain?style=flat-square&logo=github&label=Pensieve-retrain&color=808080&labelColor=595959)](https://github.com/GreenLv/pensieve_retrain)



## Publications
### Content Transmission Control
- Breath: Adaptive Protection Boundary in FEC Encoding for Mobile Real-Time Video Streaming <span class="pub-tag streaming">RTC</span><span class="pub-tag protocol">QUIC</span> \
  _Shiyang Huang<sup>1</sup>, **Gerui Lv**<sup>1</sup>, Yuankang Zhao, Jiaxing Zhang, Qingyue Tan, Congkai An, [Huanhuan Zhang](https://huanhuanzhangbupt.github.io/), [Xinyi Zhang](https://cynthiazhang.github.io/zhangxinyi/), [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [Zhenyu Li](https://zhenyulee.github.io/)_ \
  <a href="https://www2026.thewebconf.org/"><b>ACM WWW 2026</b></a>  (CCF A), Acceptance Rate: 676/3370=20.1%

- [Low-Latency Transmission Techniques for Large-Scale Internet Services | 大规模互联网服务的低时延传输技术](https://crad.ict.ac.cn/article/doi/10.7544/issn1000-1239.202550536) ([PDF](https://greenlv.github.io/files/2025_计研发_大规模互联网服务的低时延传输技术.pdf)) ([Slides](https://greenlv.github.io/files/2025_计研发_大规模互联网服务的低时延传输技术_slides.pdf)) \
  _**Gerui Lv**, Yuankang Zhao, Jiaxing Zhang, Heng Pan, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [Zhenyu Li](https://zhenyulee.github.io/)_ \
  <a href="https://crad.ict.ac.cn/"><b>Journal of Computer Research and Development | 计算机研究与发展</b></a>, 2025 (CCF中文A, 计算机技术领域T1) \
  <a href="https://mp.weixin.qq.com/s/swdgWVMk_i6RMFk4MiueRg" style="color:OrangeRed">Highlights and Perspectives (前沿亮点专栏收录)</a>

- [Predictable Real-Time Video Latency Control with Frame-level Collaboration](https://www.computer.org/csdl/proceedings-article/rtss/2025/964200a189/2cTzHjeYbVC) ([PDF](https://greenlv.github.io/files/2025_RTSS_Co-RTV.pdf)) ([Slides](https://greenlv.github.io/files/2025_RTSS_Co-RTV_slides.pdf)) <span class="pub-tag streaming">RTC</span><span class="pub-tag arch">Edge</span><span class="pub-tag protocol">QUIC</span> \
  _Jiaxing Zhang, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), **Gerui Lv**, Wenji Du, Qingyue Tan, Wanghong Yang, Kai Lv, Yuankang Zhao, Yongmao Ren, [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_ \
  <a href="https://2025.rtss.org/"><b>IEEE RTSS 2025</b></a>  (CCF A), Acceptance Rate: 44/200=22%

- [MARC: Motion-Aware Rate Control for Mobile E-commerce Cloud Rendering](https://www.usenix.org/conference/atc25/presentation/zhao-yuankang) ([PDF](https://greenlv.github.io/files/2025_ATC_MARC_paper.pdf)) ([Slides](https://greenlv.github.io/files/2025_ATC_MARC_slides.pdf)) ([Poster](https://greenlv.github.io/files/2025_ATC_MARC_poster.pdf)) ([Video](https://youtu.be/NJjfIfyDlmo)) <span class="pub-tag streaming">RTC</span> \
  _Yuankang Zhao<sup>1</sup>, Furong Yang<sup>1</sup>, **Gerui Lv**<sup>1</sup>, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Yanmei Liu, Jiuhai Zhang, Yutang Peng, Feng Peng, Hongyu Guo, Ying Chen, [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://www.usenix.org/conference/atc25"><b>USENIX ATC 2025 </b></a>  (CCF A), Acceptance Rate: 100/634=15.8%

- [Understanding and Taming the Inflated Latency in Mobile Cloud Rendering](https://dl.acm.org/doi/10.1145/3746283) ([PDF](https://greenlv.github.io/files/2025_TOMM_JitBright.pdf)) <span class="pub-tag streaming">RTC</span> \
  _Yuankang Zhao, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), **Gerui Lv**, Furong Yang, Jiuhai Zhang, Feng Peng, Yanmei Liu, [Zhenyu Li](https://zhenyulee.github.io/), Hongyu Guo, Ying Chen, [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://dl.acm.org/journal/tomm"><b>ACM Transactions on Multimedia Computing, Communications, and Applications (TOMM)</b></a>, 2025  (CCF B, JCR Q1)

- [Chorus: Coordinating Mobile Multipath Scheduling and Adaptive Video Streaming](https://dl.acm.org/doi/10.1145/3636534.3649359) ([PDF](https://greenlv.github.io/files/2024_MobiCom_Chorus_paper.pdf)) ([Slides](https://greenlv.github.io/files/2024_MobiCom_Chorus_slides.pdf)) ([Tech Report](https://greenlv.github.io/files/2024_MobiCom_Chorus_tech_report.pdf)) ([Demo Video](https://greenlv.github.io/files/2024_MobiCom_Chorus_demo_video.mp4)) ([GetMobile](https://greenlv.github.io/files/2025_GetMobile_Chorus.pdf)) <a class="github-button" href="https://github.com/GreenLv/Chorus" data-show-count="true" aria-label="Star GreenLv/Chorus on GitHub">Chorus</a> <span class="pub-tag protocol">MP</span><span class="pub-tag protocol">QUIC</span><span class="pub-tag streaming">ABR</span> \
  _**Gerui Lv**, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Yanmei Liu, [Zhenyu Li](https://zhenyulee.github.io/), Qingyue Tan, Furong Yang, Wentao Chen, [Yunfei Ma](https://yfmascgy.github.io/), Hongyu Guo, Ying Chen, [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://www.sigmobile.org/mobicom/2024/"><b>ACM MobiCom 2024</b></a>  (CCF A)  \
  <a href="https://dl.acm.org/doi/10.1145/3733892.3733900" style="color:OrangeRed">Cover Article of ACM SIGMOBILE GetMobile (Vol. 29, No. 1)</a> \
  <span style="color:OrangeRed">The First MobiCom Conference Paper from ICT, CAS</span>

- [Accurate Bandwidth Prediction for Real-Time Media Streaming with Offline Reinforcement Learning](https://dl.acm.org/doi/10.1145/3625468.3652183) ([PDF](https://greenlv.github.io/files/2024_MMSys_GC_Schaferct_paper.pdf)) ([Slides](https://greenlv.github.io/files/2024_MMSys_GC_Schaferct_slides.pdf)) ([Poster](https://greenlv.github.io/files/2024_MMSys_GC_Schaferct_poster.pdf)) <a class="github-button" href="https://github.com/n13eho/Schaferct" data-show-count="true">Schaferct</a> <span class="pub-tag streaming">RTC</span> \
  _Qingyue Tan, **Gerui Lv**, Xing Fang, Jiaxing Zhang, Zejun Yang, Yuan Jiang, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html)_  \
  <a href="https://2024.acmmmsys.org/"><b>ACM MMSys 2024</b></a>, Open-source Software and Datasets  \
  <a href="https://greenlv.github.io/files/2024_MMSys_GC_Schaferct_certificate.pdf" style="color:OrangeRed">Grand Challenge on Offline RL for Bandwidth Estimation in RTC Winner (1st place)</a>

- [JitBright: towards Low-Latency Mobile Cloud Rendering through Jitter Buffer Optimization](https://dl.acm.org/doi/10.1145/3651863.3651881) ([PDF](https://greenlv.github.io/files/2024_NOSSDAV_JitBright_paper.pdf)) ([Slides](https://greenlv.github.io/files/2024_NOSSDAV_JitBright_slides.pdf)) <span class="pub-tag streaming">RTC</span> \
  _Yuankang Zhao, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), **Gerui Lv**, Furong Yang, Jiuhai Zhang, Feng Peng, Yanmei Liu, [Zhenyu Li](https://zhenyulee.github.io/), Ying Chen, Hongyu Guo, [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://nossdav.org/2024/"><b>ACM NOSSDAV 2024</b></a>  (CCF B)  \
  <a href="https://greenlv.github.io/files/2024_NOSSDAV_JitBright_certificate.pdf" style="color:OrangeRed">Best Paper Award</a>

- [Accurate Throughput Prediction for Improving QoE in Mobile Adaptive Streaming](https://ieeexplore.ieee.org/abstract/document/10246426) ([PDF](https://greenlv.github.io/files/2023_TMC_Lumos.pdf)) <span class="pub-tag streaming">ABR</span> \
  _**Gerui Lv**, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Qingyue Tan, Weiran Wang, [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=7755"><b>IEEE Transactions on Mobile Computing (TMC)</b></a>, 2023  (CCF A, JCR Q1)

- [Lumos: towards Better Video Streaming QoE through Accurate Throughput Prediction](https://ieeexplore.ieee.org/abstract/document/9796948/) ([PDF](https://greenlv.github.io/files/2022_INFOCOM_Lumos_paper.pdf)) ([Slides](https://greenlv.github.io/files/2022_INFOCOM_Lumos_slides.pdf)) ([Video](https://youtu.be/9-LKcqPmFhA)) <a class="github-button" href="https://github.com/GreenLv/Lumos" data-show-count="true" aria-label="Star GreenLv/Lumos on GitHub">Luoms</a> <span class="pub-tag streaming">ABR</span> \
  _**Gerui Lv**, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Weiran Wang, [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_  \
  <a href="https://infocom2022.ieee-infocom.org/index.html"><b>IEEE INFOCOM 2022</b></a> (CCF A), Acceptance Rate: 225/1129=19.9%


### Content Delivery Network
- RLive: Robust Delivery System for Scaling Live Streaming Services ([PDF](https://greenlv.github.io/files/2026_EuroSys_RLive.pdf)) <span class="pub-tag arch">CDN</span><span class="pub-tag arch">Edge</span><span class="pub-tag streaming">Live</span><span class="pub-tag protocol">MP</span> \
  _Yu Tian<sup>1</sup>, **Gerui Lv**<sup>1</sup>, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Ruili Fang, Yajie Peng, Zhichen Xue, Rui Han, Chuanqing Lin, Xiaofei Pang, Ri Lu, [Zhenyu Li](https://zhenyulee.github.io/)_ \
  <a href="https://2026.eurosys.org/"><b>ACM EuroSys 2026</b></a>  (CCF A), Acceptance Rate: 79/467=16.9%

- [Oceanus: Scheduling Traffic Flows to Achieve Cost-Efficiency under Uncertainties in Large-Scale Edge CDNs](https://dl.acm.org/doi/10.1145/3768983) ([PDF](https://greenlv.github.io/files/2025_CoNEXT_Oceanus.pdf)) ([Slides](https://greenlv.github.io/files/2025_CoNEXT_Oceanus_slides.pdf)) <span class="pub-tag arch">CDN</span><span class="pub-tag arch">Edge</span> \
  _Chuanqing Lin<sup>1</sup>, **Gerui Lv**<sup>1</sup>, Fuhua Zeng, Hanlin Yang, Junwei Li, Xiaodong Li, Jingyu Yang, Yu Tian, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_ \
  <a href="https://conferences.sigcomm.org/co-next/2025/#!/home"><b>ACM CoNEXT 2025</b></a> (CCF B)

- [Cost-efficient Request Mapping for Large-scale Live Streaming Services](https://dl.acm.org/doi/10.1145/3768978) ([PDF](https://greenlv.github.io/files/2025_CoNEXT_LiveMap.pdf)) ([Slides](https://greenlv.github.io/files/2025_CoNEXT_LiveMap_slides.pdf)) <span class="pub-tag arch">CDN</span><span class="pub-tag streaming">Live</span> \
  _Yu Tian, [Zhenyu Li](https://zhenyulee.github.io/), Matthew Yang Liu, Zhaoxue Zhong, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), Ao Li, Jiaxing Zhang, **Gerui Lv**, Chuanqing Lin, Xi Wang, Jian Mao, [Gareth Tyson](https://facultyprofiles.hkust-gz.edu.cn/faculty-personal-page/TYSON-GarethJohn/gtyson), Jie Xiong, [Zhenhua Li](https://www.thucloud.com/zhenhua/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_ \
  <a href="https://conferences.sigcomm.org/co-next/2025/#!/home"><b>ACM CoNEXT 2025</b></a> (CCF B)
  
- [Bridge the Gap Between QoS and QoE in Mobile Short Video Service: A CDN Perspective](https://link.springer.com/chapter/10.1007/978-3-032-10459-5_27) ([PDF](https://greenlv.github.io/files/2025_NPC_QoE-QoS.pdf)) ([Slides](https://greenlv.github.io/files/2025_NPC_QoE-QoS_slides.pdf)) <span class="pub-tag arch">CDN</span> \
  _Chuanqing Lin, Yangguang Liang, Fuhua Zeng, Zhipeng Huang, Xiaodong Li, Jingyu Yang, Yu Tian, **Gerui Lv**, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [Zhenyu Li](https://zhenyulee.github.io/), [Gaogang Xie](https://people.ucas.ac.cn/~_xie)_ \
  <a href="https://npc-2025.github.io/index.html"><b>IFIP NPC 2025</b></a>  (CCF C)



## Patents & Standards

- [数据传输方法、系统、设备、存储介质及程序产品](https://patents.google.com/patent/CN115834556B/) [CN115834556B, ZL202310152689.9] (Granted: 2023-05-12)  \
  _**吕格瑞**, 刘彦梅, 陈文韬, 杨馥榕, 郭虹宇, 陈颖_

- [多路径传输的重注入控制方法、电子设备及存储介质](https://patents.google.com/patent/CN116436865A/) [CN116436865A]  \
  _**吕格瑞**, 刘彦梅, 杨馥榕, 陈文韬, 郭虹宇, 陈颖_

- [一种路径处理方法、装置及电子设备](https://patents.google.com/patent/CN116827853A/) [CN116827853A]  \
  _**吕格瑞**, 刘彦梅, 陈文韬, 杨馥榕, 郭虹宇, 陈颖_

- [一种数据驱动的网络视频流传输方法及装置](https://patents.google.com/patent/CN118075567A/) [CN118075567A]  \
  _**吕格瑞**, [武庆华](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), 王卫染, 谭清月, [李振宇](https://zhenyulee.github.io/)_

- [一种基于用户动作与视频帧映射的实时质量测量方法](https://patents.google.com/patent/CN120512563A/) [CN120512563A] \
  _赵员康, **吕格瑞**, [武庆华](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [李振宇](https://zhenyulee.github.io/)_

- [一种数据驱动的动态QoE偏好权重参数确定方法](https://patents.google.com/patent/CN120786053A/) [CN120786053A] \
  _赵员康, **吕格瑞**, [武庆华](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [李振宇](https://zhenyulee.github.io/)_

- 音视频服务中QoS-QoE映射关系的刻画方法、装置、介质 [CN202511547273.2] \
  _林川清, 梁阳光, 田语, **吕格瑞**, [武庆华](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [李振宇](https://zhenyulee.github.io/)_

- CDN流量调度方法、系统、装置、存储介质 [CN202511547517.7] \
  _林川清, 梁阳光, 田语, **吕格瑞**, [武庆华](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [李振宇](https://zhenyulee.github.io/)_

- [QoE-Driven Application-Transport Cooperation Requirements](https://datatracker.ietf.org/doc/draft-zhang-qoe-driven-transport-requirement/) (IETF Draft) \
  _Jiaxing Zhang, **Gerui Lv**, [Qinghua Wu](https://www.ict.ac.cn/sourcedb/cn/jssrck/202007/t20200715_5626158.html), [Zhenyu Li](https://zhenyulee.github.io/)_



## Honors and Awards
- [Excellent Doctoral Dissertations of CAS (中国科学院百篇优秀博士学位论文)](https://www.ucas.edu.cn/tz/b104567516144b8db1df8039e6abc077.htm), 2025 ([Report](https://www.ict.ac.cn/xwgg/jssxw/202509/t20250918_7971405.html))
- ACM SIGMOBILE China Doctoral Dissertation Award, 2025
- [Outstanding Ph.D. Graduates of Beijing (北京市优秀博士毕业生)](https://jw.beijing.gov.cn/tzgg/202410/t20241010_3916096.html), 2024
- Outstanding Ph.D. Graduates in UCAS, 2024
- Best Paper Award at ACM NOSSDAV 2024
- First Place in [MMSys ’24 Grand Challenge on Offline RL for Bandwidth Estimation in RTC](https://2024.acmmmsys.org/gc/ORL-BWE-RTC/), 2024
- National Scholarship for Doctoral Students, UCAS, 2023
- Third Prize in Global AI Transmission Competition (AITrans), 2019  \
  _4/138, Rank 2nd in real-world evaluations_
- First Class Academic Scholarship, UCAS, 2019
- Outstanding B.S. Graduates of Hunan (湖南省优秀本科毕业生), 2016
- Outstanding B.S. Graduates in HNU, 2016
- National Scholarship for Undergraduates (_1/111_), HNU, 2015



## Technical Impacts

- RLive [EuroSys’26] has served in the **ByteDance CDN system** for over 3 years, supporting hundreds of millions of daily live-streaming viewers. RLive has tripled delivery capacity, reduced rebuffering events by 14.9-20.1%, and improved video bitrate by 10.2-11.4%.
- LiveMap [CoNEXT’25] has been deployed in the **BiliBili CDN system** since September 2023, serving tens of millions of daily users of both VoD and live streaming. It has saved bandwidth costs by up to 42.18% (equivalent to millions of dollars annually) and decreased access latency by 20.26%.
- The flow scheduler in Oceanus [CoNEXT’25] has been deployed in the **Alibaba Cloud CDN system**, reducing CDN access latency (RTT) and improving scheduling mapping stability. 
- MARC [ATC’25] has been deployed in **Taobao 3D cloud rendering system**. It has served over 1 million sessions, reducing session freeze rates by 71% and increasing user interaction time by 20%.
- JitBright [TOMM’25; NOSSDAV’24 Best Paper] has been deployed in the **Taobao 3D cloud rendering system**. It has served over 591,000 sessions and increased the proportion of sessions that met the MTP latency requirement of less than 150 ms by 6% to 27%.
- Patent CN116436865A (part of Chorus [MobiCom’24]) has been applied in the **Taobao RPC system** (XQUIC) to control multipath reinjection. <a class="github-button" href="https://github.com/alibaba/xquic" data-show-count="true">XQUIC</a>
- One of my tech blogs ranked #1 in Google search results for “DASH标准” ([2024-01-09](https://greenlv.github.io/files/DASH_standard-Google-240109.png)).
- One of my tech blogs ranked #1 in Baidu search results for “DASH视频” ([2023-05-01](https://greenlv.github.io/files/DASH_video-Baidu-230511.png)).



## Talks

- RTC transmission system \
  @ _ByteDance_, Beijing, China, 2024-11-19 \
  @ _BUPT_, Beijing, China, 2024-11-05
- Multipath adaptive video streaming  \
  @ _GuoMeng Studio_, Beijing, China, 2023-12-10 ([Report](https://mp.weixin.qq.com/s/8y8zo96n6Bwq7I7XalsF5Q)) \
  @ _BiliBili_, Beijing, China, 2023-10-31 \
  @ _NJU_, Nanjing, China, 2023-09-02  \
  @ _Huawei_, Beijing, China, 2023-01-13
- Throughput prediction for adaptive streaming   \
  @ _BiliBili_, Beijing, China, 2023-02-07  \
  @ _Alibaba_, Hangzhou, China, 2021-08-02
- QoE optimization for low-latency live streaming  \
  @ _Tencent_, Beijing, China, 2019-12-02



## Internships

- Alibaba (Taotian), Hangzhou, China, Jun. 2021 - Sep. 2022  \
  Research Intern @ Network Technology Team  \
  Mentor: Ms. Yanmei Liu



## Teaching Experiences

- Teaching Assistant, Computer Network, UCAS \
  Fall 2019, Fall 2023 ([Slides](https://greenlv.github.io/files/Lec_Introducing_classical_ABR_algorithms.pdf))  \
  Instructor: Assoc. Prof. [Qinghua Wu](https://people.ucas.ac.cn/~0040408)



## Reviewing Experiences 

- IEEE INFOCOM (2023–2026)
- ACM CoNEXT (2024, 2025)
- IEEE ICNP (2024, 2025)
- IEEE MetaCom (2024)
- IEEE Communications Letters (2025)
- IEEE Access (2025)
- ACM MobiCom Artifacts Evaluation (2024)

