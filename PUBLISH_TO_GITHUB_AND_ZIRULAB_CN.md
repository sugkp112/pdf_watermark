# 发布到 GitHub 和 ZIRULAB（按顺序操作）

**目标仓库**：https://github.com/sugkp112/pdf_watermark
**ZIRULAB 仓库**：https://github.com/sugkp112/zirulab
**网站项目**：ZIRULAB v6.6.0（本任务的修改版本）

## 1. 在 Windows 上验收（发布前必做）

运行 `PDF_Watermark_Tool_2.1.3.20260617.exe`，用无敏感信息的 1～2 个 PDF 副本检查：
- EXE 能正常启动，没有缺少依赖的报错
- 添加文字水印和图片水印分别成功
- 对多个 PDF 批量处理成功，输出文件能正常打开
- 输出文件保存的位置、命名、覆盖行为符合预期
- 使用 Windows 安全扫描；需要的话做联网行为检查

## 2. 更新 GitHub 仓库（不要删除历史）

进入 https://github.com/sugkp112/pdf_watermark ：
1. 将本包中的 `README.md` 替换仓库首页旧 README；可一并提交 `SHA256SUMS.txt`、`RELEASE_NOTES.md`。
2. 在 Releases → Draft a new release → Choose a tag，新建 `v2.1.3`。
3. 上传 **独立 EXE 文件** `PDF_Watermark_Tool_2.1.3.20260617.exe` 作为 Release asset，不要只上传源码 ZIP，也不要提交 40 MiB EXE 到 Git 仓库主分支。
4. Release 标题写 `PDF Watermark Tool v2.1.3 (Windows x64)`，正文使用本包 `RELEASE_NOTES.md`。
5. 发布为 Latest release。
6. 打开下面网址确认能实际下载，注意 404 表示尚未上传成功：

https://github.com/sugkp112/pdf_watermark/releases/download/v2.1.3/PDF_Watermark_Tool_2.1.3.20260617.exe

## 3. 部署修改后的网站

**必须先完成第 2 步**，网站当前已经预设启用直达链接，不应在 EXE 尚未上传时部署。

1. 使用本次提供的 `ZIRULAB_6.6.0_PDF_Watermark_2.1.3_Ready.zip`，更新网站仓库。
2. 在网站项目运行 `npm ci`（如依赖未安装）、`npm run validate:data`、`npm run build`。
3. Commit/Push 到网站 `main`，按原有 Cloudflare Pages 方式构建部署。
4. 验收 https://zirulab.org/ja/software/pdf-watermark-tool
5. 验收 https://zirulab.org/download/pdf-watermark-tool

网站的固定地址会通过 302 跳转到 GitHub Release 文件；访客从 ZIRULAB 点击下载，无需进入 GitHub 页面。

## 4. 下一版更新方法

1. 在 GitHub Release 上传新版本 EXE，确认新的直链可以下载。
2. 在 ZIRULAB 后台“下载管理”编辑 `pdf-watermark-tool`，更新版本、URL、大小、SHA-256、日期。
3. 提交/部署，重新检查 `/download/pdf-watermark-tool`。

## 本次实测范围

- 校验了 PyInstaller 内部 1106 个条目可正确解压
- ZIRULAB 数据验证通过
- ZIRULAB 原有在线管理台 93 项测试通过
- 下载跳转规则生成通过
- 未在 Windows 真实运行 EXE
- 未在本环境连接并推送 Github 或上线 Cloudflare
- 未在缺少 npm 依赖的环境执行完整 Next.js 生产构建
