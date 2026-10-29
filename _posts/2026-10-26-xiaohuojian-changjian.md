---
layout: post
title: 小火箭配置基础教程：Shadowrocket 初次使用
permalink: /articles/xiaohuojian-changjian/
description: 小火箭（Shadowrocket）初次安装与基础配置的完整步骤：装好之后怎么添加第一个节点、选对协议类型、开启连接并验证真的通了，以及新手最常卡住的几个地方。
date: 2026-10-26
image: /assets/images/shadowrocket-2.webp
tags: ["shadowrocket","小火箭","配置","新手"]
category: 使用教程
---

装完小火箭打开，第一眼通常是一片空白：一个开关、一个「Add Server」，除此之外什么也没有。这和很多人预期的「装好就能用」差得远——Shadowrocket 本身不提供线路，它只是一个客户端，节点得你自己加进去。

这篇讲的就是从这张空白首页到真正连通的过程：第一个节点怎么加、协议怎么选、连上之后怎么确认它真的在干活。已经有节点、只是想了解订阅导入的，可以看站内的 [小火箭订阅链接怎么添加](/shadowrocket-subscribe-link/)，那篇讲的是批量导入。

![Shadowrocket 首页初始状态：显示 Not Connected、Global Routing 与 Connectivity Test，服务器列表为空，只有 Add Server 入口](/assets/images/shadowrocket-1.webp)

<h2>先认清首页那几个入口</h2>

<p>空白首页上其实只有三样东西，作用各不相同：</p>

<ul>
<li><strong>顶部的大开关</strong>：控制代理是否开启。左边写着「Not Connected」的时候处于关闭状态。注意这个开关只管「开不开」，不管「有没有可用节点」——没有节点时打开它，状态会一直停在连接中或者直接失败。</li>
<li><strong>Global Routing</strong>：全局路由，决定哪些流量走代理、哪些直连。默认配置通常是「配置」模式，按规则分流；新手如果发现「有的站能开有的不能」，多半是这里的分流规则在起作用，而不是节点坏了。</li>
<li><strong>服务器列表</strong>：空的时候只有一行「Add Server」。所有节点最终都出现在这里。</li>
</ul>

<p>底部还有四个标签：Home、Config、Data、Settings。配置阶段用到的只有 Home（加节点、开关）和 Settings（全局选项）。Config 是配置文件管理，Data 是流量统计，这两块等基础跑通再看更有意义。</p>

<h2>添加第一个节点</h2>

<p>点右上角的「+」，或者点列表里的「Add Server」，会进入添加服务器页面。这个页面看着字段很多，实际必填的只有四项。</p>

![Shadowrocket 添加服务器页面：Shadowsocks 协议表单，需填写 Host、Port、Password，并选择 Method 加密方式](/assets/images/shadowrocket-2.webp)

<h3>必填的四项</h3>

<ol>
<li><strong>Host（主机）</strong>：服务器地址，可以是 IP，也可以是域名。这是节点提供方给你的那一串。</li>
<li><strong>Port（端口）</strong>：1 到 65535 之间。填错端口的表现是「能保存但连不上」，不会报错提示，所以这一项要核对。</li>
<li><strong>Password（密码）</strong>：节点的连接密码，不是你的 Apple ID 密码。旁边有眼睛图标可以看明文，长密码建议点开核对一遍再保存。</li>
<li><strong>Method（加密方式）</strong>：必须和服务器端一致，常见的是 <code>aes-256-cfb</code>、<code>aes-128-gcm</code>、<code>chacha20-ietf-poly1305</code>。这一项如果和服务器不匹配，表现同样是「连不上」——小火箭不会告诉你密钥协商失败。</li>
</ol>

<p>其余字段都可以留空：One Time Auth 是一次性认证，只有服务端开启时才需要打开；Obfuscation 和 Plugin 属于特殊网络环境下的附加处理，普通节点用不到；Remark 是备注，建议填一个能认出来的名字，节点多了之后列表里全靠它区分。</p>

<h2>协议类型怎么选</h2>

<p>添加页面第一行的「Type」点进去是协议列表，里面有十几个选项。新手容易在这里犹豫，实际上大部分情况只看这一个判断：<strong>节点提供方告诉你是什么协议，就选什么</strong>，不用自己挑。</p>

![Shadowrocket 的 Type 协议选择页面：列出 Shadowsocks、ShadowsocksR、Subscribe、Vmess、Trojan 等类型，Shadowsocks 默认勾选](/assets/images/shadowrocket-3.webp)

<p>几个常见对应关系：</p>

<ul>
<li>拿到的是「服务器地址 + 端口 + 密码」，通常选 <strong>Shadowsocks</strong>。</li>
<li>拿到的是 <code>vmess://</code> 开头的一长串，或者附带 UUID，选 <strong>Vmess</strong>。</li>
<li>拿到的是 <code>trojan://</code> 开头、带密码和 SNI，选 <strong>Trojan</strong>。</li>
<li>拿到的是 <code>ss://</code>、<code>vmess://</code> 这类完整链接，其实不用手动选协议——复制链接后打开小火箭，它会自动识别并提示添加。</li>
<li>拿到的是订阅地址（一条网址，不是单节点参数），选 <strong>Subscribe</strong>，做法见订阅那篇。</li>
</ul>

<p>如果实在分不清，最省事的做法是把链接复制到剪贴板再打开小火箭，让它自动识别。手动填只在没有链接、只有一组参数时才必要。</p>

<h2>开启连接并确认真的通了</h2>

<p>节点保存后回到首页，它会出现在服务器列表里，名称前面有个圆点表示这是默认节点。把顶部开关打开，首次连接系统会弹「Shadowrocket 想要添加 VPN 配置」，点允许并验证一次（Face ID 或密码）。</p>

<p>接下来这一步最容易被跳过：<strong>开关变绿不等于链路可用</strong>。正确的验证方式是打开浏览器访问一个平时打不开的站点，能正常加载才算通。另一种方式是在首页对节点做一次 Connectivity Test，看能不能返回具体延迟毫秒数——返回超时或者报错，说明节点本身有问题，不是软件问题。</p>

<h2>新手最常卡住的四个地方</h2>

<ol>
<li><strong>节点加了但一直转圈连不上</strong>：九成是端口或加密方式和服务器不一致。这两项填错都不会报错，只会静默失败，所以值得回头逐字核对一遍。</li>
<li><strong>能连上但某些网站打不开</strong>：看 Global Routing 的分流模式。配置模式下按规则走，可能把目标站点判定为直连；切到「代理」模式全部走代理再看，能立刻区分是规则问题还是节点问题。</li>
<li><strong>打开开关没反应、连 VPN 权限都没弹</strong>：多半是之前拒绝过权限。到系统「设置 → 通用 → VPN 与设备管理」里检查是否有小火箭的配置项，删掉后重新连接会重新弹授权。</li>
<li><strong>昨天能用今天不行</strong>：先更新订阅（如果有），再测延迟。节点失效是常态，不是软件坏了；订阅制的话服务商那边换线路，你这边更新一次就恢复了。</li>
</ol>

<h2>配置跑通之后</h2>

<p>到这一步，一个节点能连、能访问目标站点，基础配置就算完成了。往下走的顺序建议是：先解决「节点从哪来」——自己手动加的节点会失效，长期用要么订阅、要么找稳定的来源，这部分可以看 [小火箭共享账号怎么评估](/shared-account-review/) 和 [美区小火箭共享账号](/us-shadowrocket-shared-list/)；再考虑「多条线路怎么管」，也就是 Config 配置文件和多分组，那属于进阶。</p>

<p>另外提醒一句：节点参数和订阅地址都等同于凭证，不要贴到公开群里，也不要用来源不明的免费节点处理敏感账号的登录。配置这件事，把基础四项填对就能用，剩下的优化都不值得用安全去换。</p>
