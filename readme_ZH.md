## PhotoshopEvents（CEP 插件示例）

此示例展示如何在 Photoshop 中通过 CEP 面板监听事件。`host/ps.jsx` 中注册了常见事件；通过 `js/CSInterface.js` 与 Photoshop 交互。

### 支持宿主
- Photoshop（PHXS）

### 前置条件
- Windows 下需要允许加载未签名扩展：双击运行项目根目录的 `enable_cep_debug.reg`。
- 目录中必须包含 `CSXS/manifest.xml`。

### 安装与加载
1. 将整个 `PhotoshopEvents` 文件夹复制到 CEP 扩展目录：
   - Windows：`C:\Users\<你的用户名>\AppData\Roaming\Adobe\CEP\extensions\PhotoshopEvents`
2. 重启 Photoshop。
3. 在菜单：窗口 → 扩展，打开“PhotoshopEvents”或“PhotoshopEvents 2”。

### 调试与查看问题
- 远程调试（DevTools）：
  - `.debug` 已为两个扩展配置端口（8001、8002）。
  - 在浏览器访问 `http://localhost:8001/`（或 `8002`）即可打开 DevTools。
- 查看 JavaScript 错误：
  - 在 DevTools 的 Console 面板查看报错与 `console.log` 输出。
  - 使用 Network 面板观察请求与资源加载情况；Sources 面板设置断点。
- 查看 ExtendScript（PS 脚本）错误：
  - 通过 `CSInterface.evalScript()` 调用脚本时，使用回调函数的 `result` 字符串查看错误信息。
- 刷新变更：
  - 本示例无需构建；直接修改 HTML/CSS/JS。
  - 关闭并重新打开面板即可应用修改（必要时重启 Photoshop）。

### 生成/打包（可选）
- 开发阶段：依赖注册表启用未签名加载，无需打包。
- 分发阶段：如需 `.zxp` 包，可使用 Adobe ZXPSignCmd 进行签名（本仓库未包含该工具）。常见流程为：
  - 保持目录结构（含 `CSXS/manifest.xml`）；
  - 使用 ZXPSignCmd 进行签名生成 `.zxp`；
  - 通过相应安装器或手动安装到 CEP 扩展目录。

### 关键文件
- `CSXS/manifest.xml`：扩展清单（宿主、UI、图标等）。
- `host/ps.jsx`：Photoshop 事件监听与脚本桥接。
- `js/CSInterface.js`：CEP 接口库。

### 常见问题
- 扩展未显示：
  - 确认已启用 PlayerDebugMode（运行 `enable_cep_debug.reg`）。
  - 确认扩展目录路径正确（使用用户目录下的 CEP\extensions）。
  - 清单中的宿主设为 `PHXS` 且版本范围兼容（默认 `[14.0, 99.9]`）。
- 权限/路径问题：
  - 建议使用用户目录路径；`Program Files` 目录可能受权限限制。
- 多 Photoshop 版本：
  - 注册表文件已覆盖常见 CSXS 版本；若仍不生效，请提供具体 Photoshop 版本以追加对应 CSXS.X。
