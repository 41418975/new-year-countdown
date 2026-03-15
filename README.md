# 跨年倒计时网站

一个功能完整、视觉吸引力强的跨年倒计时网站，实时显示距离新年的剩余时间，并在倒计时结束时展示庆祝动画和新年祝福。

在线网站：https://wmyqg.dpdns.org/

## 功能特性

### 核心功能
- **精确倒计时**：实时显示距离新年的天、时、分、秒
- **自动更新**：每秒自动刷新倒计时显示
- **跨年检测**：自动识别并计算到明年1月1日的时间

### 视觉设计
- **节日配色**：提供红色、蓝色、紫色三种主题
- **动态背景**：渐变动画背景效果
- **粒子动画**：Canvas实现的星星闪烁效果
- **烟花特效**：倒计时结束时的庆祝烟花动画
- **玻璃拟态**：现代化的毛玻璃UI设计

### 交互体验
- **平滑过渡**：数字切换时的脉冲动画
- **悬停效果**：卡片悬停时的缩放效果
- **主题切换**：一键切换不同的节日主题
- **响应式设计**：完美适配桌面、平板和移动设备

### 可定制化
- **主题持久化**：用户选择的主题会保存到本地存储
- **重新开始**：倒计时结束后可重新开始

## 技术栈

- **HTML5**：语义化标签构建页面结构
- **Tailwind CSS v3**：响应式布局和样式设计
- **CSS3**：自定义动画和过渡效果
- **JavaScript (ES6+)**：倒计时逻辑和交互效果
- **Canvas API**：粒子系统和烟花动画

## 文件结构

```
cross-year-countdown/
├── index.html          # 主页面
├── style.css           # 自定义样式和动画
├── script.js           # 倒计时逻辑和交互效果
└── README.md           # 部署说明文档
```

## 部署说明

### 方法一：本地直接打开

1. 下载所有文件到本地目录
2. 双击 `index.html` 文件在浏览器中打开
3. 即可查看倒计时效果

### 方法二：使用本地服务器

#### 使用 Python
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

#### 使用 Node.js (http-server)
```bash
# 安装 http-server
npm install -g http-server

# 启动服务器
http-server -p 8000
```

#### 使用 PHP
```bash
php -S localhost:8000
```

然后在浏览器中访问 `http://localhost:8000`

### 方法三：部署到静态网站托管平台

#### GitHub Pages
1. 创建 GitHub 仓库
2. 上传所有文件到仓库
3. 进入仓库 Settings > Pages
4. 选择 main 分支作为源
5. 保存后即可通过 GitHub Pages 访问

#### Netlify
1. 注册 Netlify 账号
2. 将文件拖拽到 Netlify 部署页面
3. 或连接 GitHub 仓库自动部署
4. 部署完成后获得网站 URL

#### Vercel
1. 注册 Vercel 账号
2. 导入 GitHub 仓库
3. 配置构建设置（静态网站无需配置）
4. 部署完成

### 方法四：部署到云服务器

#### 使用 Nginx
1. 将文件上传到服务器（如 `/var/www/countdown`）
2. 配置 Nginx：
```nginx
server {
    listen 80;
    server_name your-domain.com;
    
    root /var/www/countdown;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```
3. 重启 Nginx：`sudo systemctl restart nginx`

#### 使用 Apache
1. 将文件上传到服务器（如 `/var/www/html/countdown`）
2. 配置虚拟主机
3. 重启 Apache：`sudo systemctl restart apache2`

## 浏览器兼容性

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Opera 76+

## 性能优化

- 使用 `requestAnimationFrame` 优化动画性能
- Canvas 粒子系统自动清理过期粒子
- CSS 动画使用 transform 和 opacity 属性
- 懒加载非关键资源
- 最小化重排和重绘

## 自定义配置

### 修改主题颜色

在 `style.css` 中修改 CSS 变量：

```css
:root {
    --primary-color: #C41E3A;      /* 主色调 */
    --secondary-color: #FFD700;    /* 辅助色 */
    --bg-gradient-start: #1a0000;  /* 背景渐变起始色 */
    --bg-gradient-end: #4a0000;     /* 背景渐变结束色 */
}
```

### 添加新主题

1. 在 `style.css` 中添加新的主题类：
```css
.theme-green {
    --primary-color: #10B981;
    --secondary-color: #34D399;
    --bg-gradient-start: #064e3b;
    --bg-gradient-end: #065f46;
}
```

2. 在 `index.html` 中添加主题按钮：
```html
<button class="theme-btn w-8 h-8 rounded-full bg-green-600 border-2 border-white" data-theme="green"></button>
```

### 调整倒计时目标

在 `script.js` 的 `getNextNewYear()` 方法中修改目标日期：

```javascript
getNextNewYear() {
    const now = new Date();
    const currentYear = now.getFullYear();
    const nextYear = currentYear + 1;
    return new Date(`January 1, ${nextYear} 00:00:00`);
}
```

### 修改粒子效果

在 `script.js` 的 `createParticles()` 方法中调整粒子数量和属性：

```javascript
createParticles() {
    const particleCount = 100;  // 调整粒子数量
    
    for (let i = 0; i < particleCount; i++) {
        this.particles.push({
            x: Math.random() * this.canvas.width,
            y: Math.random() * this.canvas.height,
            size: Math.random() * 3 + 1,      // 调整粒子大小
            speedX: (Math.random() - 0.5) * 0.5,
            speedY: (Math.random() - 0.5) * 0.5,
            opacity: Math.random() * 0.5 + 0.2,
            twinkleSpeed: Math.random() * 0.02 + 0.01,
            twinkleDirection: 1
        });
    }
}
```

## 常见问题

### Q: 倒计时不准确怎么办？
A: 确保您的设备时间设置正确，网站使用的是本地系统时间。

### Q: 在移动设备上显示异常？
A: 网站已针对移动设备优化，建议使用最新版本的移动浏览器。

### Q: 如何添加音效？
A: 可以在 `script.js` 的 `handleCountdownComplete()` 方法中添加音频播放代码。

### Q: 如何修改新年祝福语？
A: 在 `index.html` 的 `celebrationContainer` 部分修改祝福文本。

## 维护和扩展

### 代码结构
- HTML：页面结构和语义化标签
- CSS：样式、动画和响应式布局
- JavaScript：倒计时逻辑、粒子系统和交互功能

### 添加新功能建议
- 添加倒计时提醒功能
- 支持自定义目标日期
- 添加分享功能
- 集成社交媒体
- 添加多语言支持
- 实现用户个性化设置

## 许可证

本项目可自由使用和修改，用于个人或商业项目。

## 联系方式

如有问题或建议，欢迎反馈。

---

**祝您新年快乐！** 🎊✨
