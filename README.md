Here is a Sudoku and 24 point Game
```markdown
# 🧩 Sudoku & 24 Game – Free Online Logic Puzzles

[![Website](https://img.shields.io/badge/website-live-brightgreen)](https://qwwpwyp.dpdns.org/)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Made with HTML/CSS/JS](https://img.shields.io/badge/made%20with-HTML%2FCSS%2FJS-orange)]()

> A responsive, ad‑free web‑based puzzle collection featuring **Sudoku** (with scoring) and the **24 Game**. No downloads, no registration – just pure logic.

🔗 **Play now:** [https://qwwpwyp.dpdns.org/hello.html](https://qwwpwyp.dpdns.org/hello.html)

---

## 🎮 Features

### Sudoku – Classic 9×9 puzzles
- **Three difficulty levels** – Easy (+1 point), Medium (+3 points), Hard (+5 points)
- **51 built‑in puzzles** (15 Easy / 20 Medium / 16 Hard) – all verified to have **a unique solution**
- **Scoring system** – total score persists in your browser (localStorage)
- **Smart helpers** – conflict highlighting, hint system, and one‑click reset
- **Keyboard support** – use number keys or on‑screen numpad
- **Clean UI** – thick 3×3 box borders for better visual clarity

### 24 Game – Mental arithmetic challenge
- Generate four random numbers and combine them with `+`, `-`, `×`, `÷` to reach 24
- Instant feedback and solution checking

---

## 🛠️ Tech stack

- **Frontend** – HTML5, CSS3 (Flexbox/Grid), Vanilla JavaScript
- **Hosting** – GitHub Pages + Cloudflare (CDN & caching)
- **Persistence** – localStorage for score storage
- **No external dependencies** – pure, lightweight, and fast

---

## 🚀 Run locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. **Open the game**
   - Double‑click `index.html` (game hub) or `sudoku.html` / `24PointGame.html` in your browser.
   - No build steps, no server required.

> 💡 For the best experience, serve with a local HTTP server (e.g., `npx serve .`) to avoid CORS quirks when testing.

---

## 🧠 How puzzles are stored

All Sudoku puzzles are hard‑coded as **81‑digit strings** inside `sudoku.html`. Each string represents a row‑major 9×9 grid where `0` = empty cell.  
Example:  
`"208010570..."` →  
```
2 0 8 0 1 0 5 7 0
4 0 1 3 5 0 0 0 0
...
```

The built‑in solver (backtracking) guarantees that every puzzle has **exactly one solution**.

---

## 🤝 Contributing

Want to add more puzzles, improve the UI, or fix a bug? Contributions are welcome!

1. Fork the repo
2. Create a new branch (`git checkout -b feature/your-idea`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-idea`)
5. Open a Pull Request

Please ensure any new Sudoku puzzle has a **unique solution** (you can test it with the built‑in solver).

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 🙏 Acknowledgements

- Inspired by classic Sudoku and 24 Game
- Icons and emojis for playful UX
- Thanks to all playtesters and contributors

---

⭐ **If you enjoy the games, please leave a star on GitHub!**  
🐛 Found an issue? [Open an issue](https://github.com/your-username/your-repo-name/issues)

---

# 🧩 数独 & 24点游戏 – 免费在线逻辑挑战

[![网站](https://img.shields.io/badge/网站-在线-green)](https://qwwpwyp.dpdns.org/)
[![GitHub 许可证](https://img.shields.io/badge/许可证-MIT-blue.svg)](LICENSE)
[![技术栈](https://img.shields.io/badge/技术-HTML%2FCSS%2FJS-orange)]()

> 一个响应式的、无广告的网页益智游戏合集，包含**数独**（带得分系统）和**24点游戏**。无需下载，无需注册，即点即玩。

🔗 **立即游玩：** [https://qwwpwyp.dpdns.org/hello.html](https://qwwpwyp.dpdns.org/hello.html)

---

## 🎮 功能特色

### 数独 – 经典九宫格谜题
- **三种难度级别** – 简单（+1分）、中等（+3分）、困难（+5分）
- **内置 51 道谜题**（简单15题 / 中等20题 / 困难16题）– 所有题目经验证**有唯一解**
- **得分系统** – 总分自动保存在浏览器中（localStorage）
- **智能辅助** – 冲突高亮、提示功能、一键重置
- **键盘支持** – 可直接使用数字键或屏幕数字键盘
- **清爽界面** – 九宫格粗边框，视觉更清晰

### 24点游戏 – 心算挑战
- 随机生成四个数字，使用 `+`、`-`、`×`、`÷` 组合出 24
- 即时反馈，自动验证答案

---

## 🛠️ 技术栈

- **前端** – HTML5、CSS3（Flexbox/Grid）、原生 JavaScript
- **托管** – GitHub Pages + Cloudflare（CDN 加速与缓存）
- **数据持久化** – localStorage 存储得分
- **无外部依赖** – 纯原生，轻量快速

---

## 🚀 本地运行

1. **克隆仓库**
   ```bash
   git clone https://github.com/你的用户名/你的仓库名.git
   cd 你的仓库名
   ```

2. **打开游戏**
   - 双击 `index.html`（游戏导航页）或 `sudoku.html` / `24PointGame.html` 即可在浏览器中运行。
   - 无需构建步骤，不需要服务器。

> 💡 最佳体验：使用本地 HTTP 服务器（例如 `npx serve .`）来避免测试时可能出现的跨域问题。

---

## 🧠 谜题的存储方式

所有数独谜题以 **81 位数字字符串** 的形式硬编码在 `sudoku.html` 中。每个字符串表示一个按行优先排列的 9×9 网格，其中 `0` 代表空格。  
例如：  
`"208010570..."` 对应 →  
```
2 0 8 0 1 0 5 7 0
4 0 1 3 5 0 0 0 0
...
```

内置的回溯求解器保证每道谜题**有且仅有一个解**。

---

## 🤝 贡献

想添加更多谜题、改进界面或修复 bug？欢迎贡献！

1. Fork 本仓库
2. 创建新分支 (`git checkout -b feature/你的想法`)
3. 提交更改 (`git commit -m '添加某个功能'`)
4. 推送到分支 (`git push origin feature/你的想法`)
5. 发起 Pull Request

请确保新增的数独谜题有**唯一解**（可以用内置求解器验证）。

---

## 📄 许可证

基于 **MIT 许可证** 分发。详见 `LICENSE` 文件。

---

## 🙏 致谢

- 灵感来自经典的数独和 24 点游戏
- 有趣的表情符号和图标
- 感谢所有测试者和贡献者

---

⭐ **如果你喜欢这些游戏，请在 GitHub 上给个 Star！**  
🐛 发现问题？[提交 Issue](https://github.com/你的用户名/你的仓库名/issues)
```
