# 宠伴时光 · PawTrack

一个移动端优先的养宠成长记录与社区雏形。围绕「记录成长 → 管理健康 → 认识同城宠友」，把宠物的日常串成可回看的陪伴手记。

公开地址：**https://luo-1020-qc.github.io/pawtrack/**。已通过 GitHub Actions 部署与无登录 HTTP 访问验证。不要重命名仓库，以保持评审链接不变。

## 产品体验

- **首页**：成长手记、宠物切换、健康快捷入口、六条演示日常、同城筛选、点赞及发布日常。
- **记录**：体重趋势图；体重、疫苗、驱虫和其他记录；自行设置下次计划日期，自动显示临近/到期/过期标签。
- **时间线**：选中宠物的健康记录、自己发布的日常及出生节点，按日期倒序排列，支持分类筛选。
- **宠友**：按城市、地区、物种筛选演示宠友，并按模拟距离排序；关注状态在本地保存。
- **我的**：个人资料、多宠物档案、JSON 数据导出、带确认的演示重置。

首次使用生成两只宠物的完整演示数据，日期相对于首次访问当天生成。后续刷新读取 localStorage，不覆盖自己的修改。

## 本地运行

需要 Node.js 20.19+ 或 22.12+；本项目使用 Node.js 24 验证。

```powershell
npm.cmd ci
npm.cmd run dev
```

打开输出中的本地地址，并访问 `/pawtrack/`。Windows PowerShell 若禁止 npm.ps1，请使用 `npm.cmd`；脚本直接运行 Vite 的 Node 入口，兼容项目上层目录 `Job&Intern` 中的 `&` 字符。

```powershell
npm.cmd test
npm.cmd run build
npm.cmd run preview
```

生产产物在 `dist/`。React 18 + Vite 6 + Tailwind CSS 3 + React Router HashRouter + Recharts；没有后端或环境密钥。

## GitHub Pages 部署

1. 在账号 `Luo-1020-qc` 下创建公开仓库 `pawtrack`。
2. 推送本项目至 `main`，包含 `package-lock.json` 和 `.github/workflows/pages.yml`。
3. 在仓库 **Settings → Pages → Build and deployment → Source** 选择 **GitHub Actions**。
4. 在 Actions 中确认 `Deploy PawTrack to GitHub Pages` 的 build 与 deploy 均成功；必要时手动 Run workflow。
5. 用未登录窗口访问公开地址，确认静态资源、页面切换及刷新正常。保持仓库名不变。

每次推送 main，工作流使用 `npm ci` 安装锁定依赖，执行模型测试、生产构建，再部署 Pages。Vite base 固定为 `/pawtrack/`，HashRouter 避免路径刷新 404。

## 数据与边界

- 所有输入、图片、关注、点赞和记录保存在当前浏览器的 `pawtrack:v1` 中，不会同步其他设备或真实用户。
- 图片限制 JPG/PNG/WebP、1.2 MB 以下。localStorage 写入失败会明确显示警告；请及时导出备份。
- 附近宠友与距离均为演示数据，不获取真实地理定位；没有真实私信、评论或后端账号系统。
- 到期提醒仅在应用内展示，不发送系统推送；计划日期自行填写，不推断医疗周期。
- 清除浏览器数据、切换浏览器或重置会影响本地数据。导出 JSON 用于备份，本版未提供导入功能。
- 日期按浏览器本地日历处理。健康记录为日常管理工具，计划请遵循兽医建议。

更多说明见 [产品设计](docs/产品设计.md) 和 [交付验收](docs/交付验收.md)。
