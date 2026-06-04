[README.md](https://github.com/user-attachments/files/28578393/README.md)
# OpenNVR - 开源视频管理系统

## 部署到新电脑

### 前置条件
1. **Node.js** — 下载安装 https://nodejs.org/ (LTS 版本)
2. **FFmpeg** — 下载 https://www.gyan.dev/ffmpeg/builds/
   - 选择 `release full` 版本
   - 解压后将 `bin\ffmpeg.exe` 复制到项目根目录

### 部署步骤
1. 解压 `OpenNVR.zip` 到任意目录
2. 双击运行 `setup.bat`（自动检测环境）
3. 双击 `start.bat` 启动服务
4. 浏览器打开 http://127.0.0.1:10800

### 登录信息
- 账号: `admin`
- 密码: `admin123`

## 日常使用

| 操作 | 方式 |
|------|------|
| 启动服务 | 双击 `start.bat` |
| 停止服务 | 双击 `stop.bat` |
| 打开管理界面 | 浏览器访问 http://127.0.0.1:10800 |

## 功能特性

- 实时预览（1x1 / 2x2 / 4x4 网格）
- WebSocket-FLV 低延迟播放（~1秒）
- HLS 播放（兼容性回退）
- 支持 RTSP / RTMP / HTTP / 本地文件
- 自动检测 H.264/H.265 编码
- 直播推流（B站/抖音/斗鱼/虎牙/YouTube/Twitch）
- 分享扫码观看
- 通道管理、自动重连
- 快照抓取、操作日志

## 接入摄像头

进入「通道管理」→「添加通道」，填入摄像头 RTSP 地址：

```
rtsp://admin:password@192.168.1.64:554/Streaming/Channels/101
```

## 项目结构

```
OpenNVR/
├── setup.bat              # 环境检测与部署
├── start.bat              # 启动服务
├── stop.bat               # 停止服务
├── ffmpeg.exe             # FFmpeg (需手动放入)
├── server.js              # 主服务入口
├── config/default.js      # 配置文件
├── lib/
│   ├── db.js              # 数据库
│   ├── streamManager.js   # HLS 流引擎
│   ├── flvStreamManager.js# WebSocket-FLV 流引擎
│   └── pushManager.js     # 直播推流
├── routes/
│   ├── api.js             # REST API
│   ├── live.js            # 直播推流 API
│   └── share.js           # 分享 API
├── public/                # 前端页面 (完全离线)
├── storage/               # HLS/录像/快照 (自动创建)
└── data/                  # 数据库文件 (自动创建)
```

## 配置说明

编辑 `config/default.js` 可修改：
- `port` — Web 服务端口（默认 10800）
- `storage.record` — 录像存储路径
- `ffmpeg.hlsTime` — HLS 分片时长
- `channel.reconnectInterval` — 断线重连间隔
