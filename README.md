# 猪跑酷 · PWA 发布包

这个目录就是可以直接上传到静态托管的版本：入口是 `index.html`，PWA 清单、Service Worker 和图标都已配好。

## 本地预览

在本目录执行：

```bash
python -m http.server 8000
```

然后打开 `http://localhost:8000/`。注意：Service Worker 只在 `localhost` 或 HTTPS 下生效，直接双击 `index.html`（file://）不会注册 PWA。

## 发布到 GitHub Pages

1. 在 GitHub 新建一个 **Public** 仓库（例如 `pigrun`）；
2. 把本目录里的**所有文件**上传到仓库根目录（网页拖拽或 git push 均可）；
3. 仓库 **Settings → Pages**；
4. **Build and deployment → Source** 选 `Deploy from a branch`，Branch 选 `main`，目录选 `/(root)`，保存；
5. 等 1–2 分钟，页面顶部会出现站点地址，形如：

   `https://<你的用户名>.github.io/pigrun/`
6. 手机浏览器打开这个地址即可游玩；Android Chrome 菜单里会出现「安装应用 / 添加到主屏幕」，iOS Safari 用「分享 → 添加到主屏幕」。

分享时直接发第 5 步的链接即可，别人点开就能玩，不需要安装。

## 更新与注意事项

- 修改游戏后重新上传，并把 `sw.js` 第一行的 `CACHE` 版本号改一下（例如 `pigrun-v2`），否则老用户可能继续用缓存；
- 必须通过 HTTPS 访问（GitHub Pages 自带 HTTPS）；
- 结算界面的随机猪图来自 `pighub.top` 外链，离线或该站不可达时会回退到 🐖；
- `*.github.io` 在国内部分网络下可能不稳定。如果分享给国内朋友后打不开，可以：
  - 给 Pages 绑定自己的域名（仓库根目录加 `CNAME` 文件，DNS 加 CNAME 记录，再开启 Enforce HTTPS）；
  - 或改用 Cloudflare Pages、Vercel、Netlify 等静态托管（同样支持 PWA）；
  - 或使用国内对象存储 + CDN（需要域名备案）。

## 文件说明

| 文件                     | 作用                    |
| ---------------------- | --------------------- |
| `index.html`           | 游戏本体（单文件，图片已内嵌）       |
| `manifest.json`        | PWA 清单（名称、图标、全屏、任意方向） |
| `sw.js`                | 离线缓存                  |
| `icon-*.png`           | 安装图标（含 maskable）      |
| `apple-touch-icon.png` | iOS 主屏幕图标             |
