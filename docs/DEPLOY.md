# 部署到 GitHub Pages

这个目录是静态网页，可以直接作为 GitHub Pages 的发布目录。

## 推荐方式：Pages 使用 `/docs`

1. 把本仓库推送到 GitHub。
2. 进入 GitHub 仓库：`Settings` → `Pages`。
3. `Build and deployment` 选择 `Deploy from a branch`。
4. Branch 选择 `main`，目录选择 `/docs`。
5. 保存后等待 GitHub Pages 构建完成。

发布地址通常是：

```text
https://<用户名>.github.io/<仓库名>/
```

本仓库如果使用 `Buffetzhu/newbeeAIppt`，地址大概率是：

```text
https://buffetzhu.github.io/newbeeAIppt/
```

## 本地预览

在仓库根目录运行：

```bash
python3 -m http.server 4173 --directory docs
```

然后打开：

```text
http://localhost:4173
```

## 文件说明

- `index.html`：预习网页
- `PREPARE.md`：给朋友看的提前下载说明
- `assets/slides/`：29 页幻灯片图片
- `downloads/ai-share-v41.pdf`：PDF 版
- `downloads/ai-share-v41.pptx`：PPTX 版
- `downloads/agent.md`：可选阅读材料
