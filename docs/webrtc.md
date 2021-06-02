# WebRTC

### 历史现状和前景，优缺点，使用场景

- [WebRTC for the Curious](https://webrtcforthecurious.com/)

### [ORTC](https://ortc.org/)

### 开源方案

- pion
- aiortc

### 构架

![img](S:\emctoo.github.io\docs\assets\webrtc-public-diagram-for-website.png)

媒体协商和网络协商(candidate)

### SDP

信令服务器（比如WebSocket服务器）

createOffer() => SessionDescription

createAnswer() => SessionDescription

数据格式，用于描述媒体信息



一行或者多行UTF-8文本

每行开头一个字符表示类型，后跟等号("=")，然后是结构化文本。

m开头的是提供媒体描述的，也称”m行“

### P2P和NAT

NAT类型

- 完全圆锥形NAT
- 受限圆锥形NAT
- 端口受限圆锥形NAT
- 对称型NAT（又称双向NAT）

ICE (Interactive Connectivity Establishment) 框架来实现RTCPeerConnection的NAT穿透

### STUN

STUN (Session Traversal Utilities for NAT)，找出公网地址和NAT的类型。

能解决前三种。

### TURN

TURN (Tranversal Using Relays around NAT), STUN/RFC5389 扩展

coturn

[pion/turn](https://github.com/pion/turn)

### 信令服务

SDP媒体信息和Candidate网络信息

### Mesh方案

### SFU方案