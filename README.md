# 多直播流播放器

一个基于 HTML + CSS + JavaScript 和 Video.js 的多直播流播放器，支持同时播放多个直播流。

## 功能特性

- ✅ 同时播放多个视频流
- ✅ 响应式设计，支持桌面和移动端
- ✅ 统一控制所有播放器（播放、暂停、静音）
- ✅ 实时状态显示
- ✅ 现代化 UI 设计
- ✅ 无需依赖，直接打开 HTML 即可使用

## 使用方法

1. 直接用浏览器打开 `index.html` 文件
2. 页面会自动加载并初始化 4 个视频播放器
3. 使用顶部的控制按钮可以统一控制所有播放器
4. 每个播放器都有独立的控制条和状态显示

## 添加真实直播流

要使用真实的直播流，请按以下步骤修改 `index.html` 文件：

### 支持的流格式

- **HLS (m3u8)**: 推荐用于直播流
- **DASH**: 自适应流媒体
- **MP4**: 普通视频文件
- **WebM**: 现代浏览器支持
- **RTMP**: 需要额外配置

### 修改流地址示例

找到 `<source>` 标签，替换 `src` 属性：

```html
<!-- HLS 直播流示例 -->
<source src="https://example.com/live/stream1/index.m3u8" type="application/x-mpegURL">

<!-- DASH 流示例 -->
<source src="https://example.com/live/stream1/manifest.mpd" type="application/dash+xml">

<!-- MP4 视频示例 -->
<source src="https://example.com/video/stream1.mp4" type="video/mp4">
```

### 常见直播流类型配置

1. **HLS 流 (.m3u8)**:
```html
<source src="https://your-cdn.com/live/channel1/playlist.m3u8" type="application/x-mpegURL">
```

2. **YouTube 直播**:
   - 需要使用 YouTube 提供的嵌入代码或 API

3. **RTMP 流**:
   - 需要额外的 Video.js 插件 (videojs-contrib-hls)

## 自定义配置

### 添加更多播放器

在 HTML 中复制播放器块：

```html
<div class="stream-item">
    <div class="stream-title">直播流 5 - 自定义频道</div>
    <video-js
        id="stream5"
        class="video-js vjs-default-skin"
        controls
        preload="auto"
        data-setup='{}'>
        <source src="YOUR_STREAM_URL" type="application/x-mpegURL">
    </video-js>
    <div class="stream-info">
        <strong>状态:</strong> <span id="status5">准备就绪</span><br>
        <strong>分辨率:</strong> 1920x1080<br>
        <strong>比特率:</strong> 3000 kbps
    </div>
</div>
```

然后在 JavaScript 中添加新的 stream ID：

```javascript
const streamIds = ['stream1', 'stream2', 'stream3', 'stream4', 'stream5'];
```

### 修改播放器设置

在 `initializePlayers()` 函数中可以自定义 Video.js 选项：

```javascript
players[streamId] = videojs(streamId, {
    fluid: true,                    // 响应式
    responsive: true,               // 自适应
    playbackRates: [0.5, 1, 1.5, 2], // 播放速度选项
    controls: true,                 // 显示控制条
    preload: 'metadata',           // 预加载模式
    autoplay: false,               // 自动播放
    muted: false,                  // 静音
    loop: false,                   // 循环播放
    poster: 'thumbnail.jpg'        // 封面图
});
```

## 高级功能

### 添加画质切换

```javascript
// 为支持多码率的流添加画质选择
players[streamId].ready(() => {
    players[streamId].qualityLevels();
});
```

### 添加全屏功能

```javascript
// 单个播放器全屏
function fullscreenPlayer(streamId) {
    if (players[streamId]) {
        players[streamId].requestFullscreen();
    }
}
```

### 自定义主题

修改 CSS 变量来改变播放器外观：

```css
.video-js {
    --vjs-theme-forest: #01B74F;
    --vjs-theme-sea: #0F7B82;
    --vjs-theme-city: #981C26;
}
```

## 故障排除

### 常见问题

1. **视频无法播放**
   - 检查流地址是否正确
   - 确认流格式被浏览器支持
   - 查看浏览器控制台错误信息

2. **CORS 错误**
   - 直播流服务器需要设置正确的 CORS 头
   - 某些流需要在本地服务器环境下运行

3. **性能问题**
   - 减少同时播放的流数量
   - 降低视频质量
   - 使用硬件加速

### 浏览器兼容性

- ✅ Chrome 60+
- ✅ Firefox 55+
- ✅ Safari 11+
- ✅ Edge 79+
- ⚠️ IE 不支持

## 许可证

MIT License - 可自由使用和修改

## 技术栈

- HTML5 Video API
- Video.js 7.x
- CSS Grid & Flexbox
- Vanilla JavaScript (ES6+) # videodemo
