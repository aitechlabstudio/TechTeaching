# 免费试用 Grok 4.5：Grok Build 安装教程

xAI 目前正在**限时免费开放 Grok 4.5** 在 **Grok Build** 和 **Cursor** 中的使用。

立即体验：

https://x.ai/cli

---

## 什么是 Grok Build？

Grok Build 是 xAI 推出的 AI 编程工具，可以直接在终端中使用 Grok 4.5 来：

- 🤖 生成代码
- 🐛 调试程序和修复 Bug
- 📁 分析项目代码
- ✨ 自动生成文档
- 🚀 辅助开发各种应用

---

## Windows 安装教程

在 PowerShell 中执行：

```powershell
irm https://x.ai/cli/install.ps1 | iex
```

说明：

- `irm`：下载官方安装脚本（Invoke-RestMethod）
- `iex`：执行下载的安装脚本（Invoke-Expression）

执行完成后，系统会自动下载并安装 Grok Build。

---



## 开始体验 Grok 4.5

```powershell
mkdir C:\grok; cd C:\grok
```
然后再执行
```powershell
grok
```

```powershell
agent
```
## 测试太阳系模拟器
```
Make a beautiful simulation of the universe and solar system. should be sped up with adjustable time, realistic motion, orbits, stars. use threejs. Make the HUD well styled and conform to modern design principles.
```
## 测试城市建造游戏
```
使用 HTML、CSS 和 JavaScript 创建一个类似 SimCity 的城市建造游戏。

要求：
- 网格地图
- 建造住宅区、商业区和发电厂
- 金币和税收系统
- 人口增长
- 时间推进系统
- 游戏存档
- 美观的现代 HUD
- 支持鼠标拖拽建造
```
## 测试简单的第一人称射击游戏
```
Create a complete first-person shooter (FPS) game using Three.js and pure JavaScript.

Requirements:

- Everything should run locally in a browser with no backend required.
- Use Three.js for all 3D rendering.
- Create a modern sci-fi environment with buildings, obstacles, lighting, shadows, and atmospheric effects.
- Implement true first-person controls using Pointer Lock API:
  - WASD movement
  - Mouse look
  - Jumping
  - Sprinting
  - Collision detection
- Add weapons:
  - Assault rifle
  - Pistol
  - Reload system
  - Muzzle flash
  - Recoil animation
  - Ammo counter
- Add enemies:
  - Enemy AI patrols the map
  - Detects the player
  - Chases and attacks the player
  - Takes damage and dies
  - Respawns after a delay
- Add gameplay systems:
  - Health system
  - Damage indicators
  - Kill counter
  - Score system
  - Game over screen
  - Pause menu
- Add visual effects:
  - Crosshair
  - Particle effects
  - Explosions
  - Bullet impacts
  - Dynamic lighting
  - Screen shake
- Create a modern HUD:
  - Health bar
  - Ammo display
  - Score display
  - FPS counter
  - Minimap
- Add sound effects:
  - Gunshots
  - Reload sounds
  - Footsteps
  - Explosions
  - Background music
- Optimize performance to maintain smooth gameplay.
- Organize the code into multiple files and use clean software architecture.
- Include comments explaining the implementation.

After generating the project:
1. Create all required files and folders.
2. Explain how to run the game.
3. Automatically start a local web server.
4. Launch the game in the browser and verify that it is fully playable.
5. If there are any errors, debug and fix them automatically until the game runs correctly.

The final result should feel like a small but complete FPS game rather than a simple demo.
```
### 测试生成PPT
```
请创建一个完整的 PowerPoint 演示文稿，主题为《2026 年人工智能编程助手行业发展趋势》。

要求：

1. 生成 12-15 页 PPT。
2. 包含封面页、目录页、总结页和感谢页。
3. 包含以下章节：
   - AI 编程助手的发展历程
   - GPT、Claude、Gemini、Grok 的对比
   - 市场规模与增长趋势
   - 企业应用案例
   - 开发者使用场景
   - 未来发展方向与挑战
4. 自动生成图表，包括：
   - 柱状图
   - 折线图
   - 饼图
   - 对比表格
5. 每页采用现代化商务风格设计：
   - 深色科技主题
   - 统一配色方案
   - 图标和数据可视化元素
   - 简洁且具有演示感的排版
6. 自动生成演讲备注（Speaker Notes）。
7. 最终输出为可编辑的 .pptx 文件。
```
---

## 官方地址

- 官网：https://x.ai/cli

> 🎉 xAI 正在限时免费开放 Grok 4.5 在 Grok Build 和 Cursor 中的使用，感兴趣的开发者可以尽快安装体验。
