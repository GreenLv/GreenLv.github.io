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


***Special Research Assistant (Postdoctoral Researcher)*** \
Network Architecture and System Research Group (NASG), Network Research Center \
[Institute of Computing Technology, Chinese Academy of Sciences (ICT, CAS)](https://www.ict.ac.cn/) \
中国科学院计算技术研究所 · 网络技术研究中心 · 网络体系结构与系统课题组 \
特别研究助理（博士后）



---

He is currently a Special Research Assistant (Postdoctoral Researcher) at ICT, CAS. He received his Ph.D. degree from ICT, CAS / [University of Chinese Academy of Sciences (UCAS)](https://www.ucas.ac.cn/) in 2024, advised by Prof. [Gaogang Xie](https://people.ucas.ac.cn/~_xie) and Prof. [Zhenyu Li](https://zhenyulee.github.io/).

**Research Interest**:
<div id="research-interests" markdown="1">
- Video Streaming: real-time communication <span class="pub-tag streaming">RTC</span>, adaptive bitrate  streaming <span class="pub-tag streaming">ABR</span>, live streaming <span class="pub-tag streaming">Live</span>, etc.
- Network Protocol: content over QUIC <span class="pub-tag protocol">QUIC</span>, multipath transmission <span class="pub-tag protocol">MP</span>, etc.
- Internet Architecture: content delivery network <span class="pub-tag arch">CDN</span>, edge collaboration <span class="pub-tag arch">Edge</span>, etc.
</div>

**[Full Publication List →](/publications/)** | **[Full CV →](/cv/)**



## Recent News

{% assign recent_news = site.data.news | sort: "date" | reverse %}
<div class="news-panel">
  <ul>
    {% for item in recent_news limit: 6 %}
      <li><span class="news-date">[{{ item.date }}]</span> {{ item.icon }} {{ item.content }}</li>
    {% endfor %}
  </ul>
</div>




## Research Scope of NASG
Main studies on Internet transmission system (from 2021):
<p class="research-scope-hint">Swipe horizontally to view the complete research scope.</p>

<div class="research-scope-table" markdown="1">
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
        <!-- Data Control -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6"><b>Data Control</b><br>
        - MARC [<a href="https://www.usenix.org/conference/atc25/presentation/zhao-yuankang">ATC’25</a>]<br>
        - JitBright [<a href="https://dl.acm.org/doi/10.1145/3651863.3651881">NOSSDAV’24 Best Paper</a>]</td>
        <!-- Bandwidth Prediction -->
        <td style="vertical-align: top; border-right: 1px solid #a6a6a6; border-bottom: 1px solid #a6a6a6"><b>Bandwidth Prediction</b><br>
        - Schaferct [<a href="https://dl.acm.org/doi/10.1145/3625468.3652183">MMSys’24 GC No.1</a>]<br>
        - Lumos [<a href="https://ieeexplore.ieee.org/abstract/document/10246426">TMC’23</a> / <a href="https://ieeexplore.ieee.org/abstract/document/9796948/">INFOCOM’22</a>]</td>
        <!-- CDN Scheduling -->
        <td style="vertical-align: top; border-right: 2px solid #595959; border-bottom: 1px solid #a6a6a6"><b>CDN Scheduling</b><br>
        - RLive [<a href="https://dl.acm.org/doi/abs/10.1145/3767295.3769360">EuroSys’26</a>]<br>
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
        - Breath [<a href="https://dl.acm.org/doi/10.1145/3774904.3792265">WWW’26</a>]<br>
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
        - Co-RTV [<a href="https://ieeexplore.ieee.org/abstract/document/11315082">RTSS’25</a>]<br>
        - TECC [<a href="https://www.usenix.org/conference/nsdi24/presentation/zhang-jiaxing">NSDI’24</a>]</td>
    </tr>
</table>
</div>


**Open-source projects:** \
[![Lumos](https://img.shields.io/github/stars/GreenLv/Lumos?style=flat-square&logo=github&label=Lumos&color=959595&labelColor=595959)](https://github.com/GreenLv/Lumos)
&nbsp;
[![Schaferct](https://img.shields.io/github/stars/n13eho/Schaferct?style=flat-square&logo=github&label=Schaferct&color=959595&labelColor=595959)](https://github.com/n13eho/Schaferct)
&nbsp;
[![Chorus](https://img.shields.io/github/stars/GreenLv/Chorus?style=flat-square&logo=github&label=Chorus&color=959595&labelColor=595959)](https://github.com/GreenLv/Chorus)
&nbsp;
[![Solis-WiFi-Trace](https://img.shields.io/github/stars/GreenLv/Solis-WiFi-Trace?style=flat-square&logo=github&label=Solis-WiFi-Trace&color=959595&labelColor=595959)](https://github.com/GreenLv/Solis-WiFi-Trace)
&nbsp;
[![Pensieve-retrain](https://img.shields.io/github/stars/GreenLv/pensieve_retrain?style=flat-square&logo=github&label=Pensieve-retrain&color=959595&labelColor=595959)](https://github.com/GreenLv/pensieve_retrain)



## Technical Impacts

- RLive [EuroSys’26] has served in the **ByteDance CDN system** for over 3 years, supporting hundreds of millions of daily live-streaming viewers. RLive has tripled delivery capacity, reduced rebuffering events by 14.9-20.1%, and improved video bitrate by 10.2-11.4%.
- LiveMap [CoNEXT’25] has been deployed in the **BiliBili CDN system** since September 2023, serving tens of millions of daily users of both VoD and live streaming. It has saved bandwidth costs by up to 42.18% (equivalent to millions of dollars annually) and decreased access latency by 20.26%.
- The flow scheduler in Oceanus [CoNEXT’25] has been deployed in the **Alibaba Cloud CDN system**, reducing CDN access latency (RTT) and improving scheduling mapping stability.
- MARC [ATC’25] has been deployed in **Taobao 3D cloud rendering system**. It has served over 1 million sessions, reducing session freeze rates by 71% and increasing user interaction time by 20%.
- JitBright [TOMM’25; NOSSDAV’24 Best Paper] has been deployed in the **Taobao 3D cloud rendering system**. It has served over 591,000 sessions and increased the proportion of sessions that met the MTP latency requirement of less than 150 ms by 6% to 27%.
- Patent CN116436865B (part of Chorus [MobiCom’24]) has been applied in the **Taobao RPC system** (XQUIC) to control multipath reinjection. <a class="github-button" href="https://github.com/alibaba/xquic" data-show-count="true">XQUIC</a>
- One of my tech blogs ranked #1 in Google search results for “DASH标准” ([2024-01-09](https://greenlv.github.io/files/DASH_standard-Google-240109.png)).
- One of my tech blogs ranked #1 in Baidu search results for “DASH视频” ([2023-05-01](https://greenlv.github.io/files/DASH_video-Baidu-230511.png)).
