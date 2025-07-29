# 谷歌安全外壳（Google Secure Shell）使用教程

## 概要

本指南涵盖了 Google Secure Shell 扩展的以下内容：

- **安装**：如何在各种平台上添加并启动扩展/应用
- **第一次连接与保存会话**：创建并保存 SSH 连接
- **自定义外观**：如何更改字体、字号、配色方案，并示例热门字体配置
- **会话管理**：保存密码与私钥、会话同步，以及在浏览器中像书签一样管理多个连接
- **多窗口/多标签并行连接**：同时打开多个 SSH 会话的技巧
- **文件上传/下载**：使用内置 SFTP 客户端执行文件传输

**当前版本：** 0.68（2025年2月更新）

## 1. 安装

### 1.1 Chrome 扩展与 App 版本

**Chrome/Windows/macOS/Linux 用户**：请安装 [Secure Shell Extension](https://chrome.google.com/webstore/detail/pnhechapfaindjhompbnflcldabbghjo)

**Chrome OS 用户**：建议安装 [Secure Shell App](https://chrome.google.com/webstore/detail/iodihamcpbpeioajjeobimgagajmlibd)

在 Chrome 浏览器中访问 Web Store 页面，点击 "Add to Chrome" 即可完成安装。

### 1.2 启动方式

- **扩展图标**：点击浏览器工具栏中的小黑色终端图标，再选择 "Connection Dialog"
- **命令行快捷**：在地址栏输入 `ssh`，然后按 Tab → Enter
- **App 版**：在 `chrome://apps` 或 Web Store 的 "Launch App" 按钮中启动

## 2. 第一次连接与保存会话

### 2.1 创建新连接

1. 打开连接对话框后，确保左上角选择 "New Connection"
2. 在文本框中输入 `用户名@主机名[:端口]`（如 `root@192.168.1.100:2222`），也可直接输入自定义名称
3. 若未自动填充，可手动在下方分别填写 用户名 (Username)、主机 (Hostname)、端口 (Port)
4. 点击 "Connect" 或按 Enter 建立连接

### 2.2 保存并重连

- 首次连接后，下次可直接在名称框中选择已保存的连接，无需重复填写
- 也可在连接对话框或扩展管理页中 右键 → Bookmark，将会话作为书签保存

## 3. 自定义外观

所有外观设置均在 Secure Shell Options 页面（Chrome 扩展设置 → "Options"）下的 Terminal Settings → Appearance 中完成。

### 3.1 选择与配置字体

**字体选择**：建议使用等宽字体；扩展默认提供以下 Web 字体：
- Cousine, Inconsolata, Roboto Mono, Source Code Pro
- Powerline 系列：Powerline For Cousine, Powerline For Inconsolata…

**示例：使用 Google Web Fonts**
在 Custom CSS URI 或 user-css-text 中添加：
```css
@import url('https://fonts.googleapis.com/css?family=Roboto+Mono');
x-row {
  font-family: "Roboto Mono", monospace;
}
```

**示例：Powerline 字体**
```css
@font-face {
  font-family: "Anonymous Pro";
  src: url("https://cdn.rawgit.com/wernight/powerline-web-fonts/8040cf32c146c7cd4f776c1484d23dc40685c1bc/fonts/AnonymousPro.woff2") format("woff2");
}
x-row {
  font-family: "Anonymous Pro", monospace;
}
```

### 3.2 字号 & 缩放

- 默认字号在 Appearance → Font size 中设置
- 快捷临时放大/缩小：`Ctrl + Plus/Minus/Zero`

### 3.3 其他配色与光标

- **配色方案**：可输入任何合法 CSS 颜色值（支持 rgba 半透明）
- **光标闪烁**：Appearance → Cursor blink 开关

## 4. 会话管理

### 4.1 保存密码与私钥

**密码自动保存**：Chrome 自带密码管理会提示是否保存，不会与扩展同步（仅本地存储）

**私钥管理**：
- 在连接对话框中点击 "Import"，上传 id_rsa（私钥）与 id_rsa.pub（公钥），存储于 HTML5 文件系统
- 删除私钥：选中身份后按 Delete 即可清除

### 4.2 同步与多设备

**Chrome Sync**：连接信息、偏好设置同步，私钥不上传云端；在不同设备重装时需重新导入私钥

## 5. 多窗口/多标签并行连接

- **Ctrl + 点击 "Connection Dialog"**：可在新标签打开连接界面
- **Chrome App 模式**：右键扩展图标 → "Create shortcut…" → 选 "Open as window"
- **使用书签**：将带有连接参数的 URL 收藏，点击即可并行发起多个 SSH 会话

## 6. 文件上传/下载

Secure Shell 内置 SFTP 客户端，无需额外安装。

### 6.1 基本 SFTP 操作

在终端中输入：
```bash
sftp 用户名@主机[:端口]
```

#### 目录操作命令：
- `pwd` 查看远端当前目录
- `lpwd` 查看本地当前目录
- `ls` 或 `ls -l` 列出远程目录文件
- `lls` 列出本地目录文件
- `cd <path>` 切换远程目录
- `lcd <path>` 切换本地目录

#### 文件下载命令：

**基本语法：**
```bash
get <remote_path> [<local_path>]
```

**示例：**
```bash
# 下载到当前本地目录（保持原文件名）
sftp> get filebeat-7.9.1-x86_64.rpm

# 指定本地保存路径和文件名
sftp> get filebeat-7.9.1-x86_64.rpm /home/user/downloads/filebeat-7.9.1-x86_64.rpm

# 批量下载（使用通配符）
sftp> mget *.rpm
```

**注意：** 如果不指定 `<local_path>`，下载的文件会保存在当前本地工作目录，文件名与远端相同。

#### 文件上传命令：

**基本语法：**
```bash
put <local_path> [<remote_path>]
```

**示例：**
```bash
# 上传到当前远程目录
sftp> put local_file.txt

# 指定远程保存路径
sftp> put local_file.txt /remote/path/remote_file.txt

# 批量上传
sftp> mput *.txt
```

### 6.2 SFTP 操作流程

#### 确认远端与本地目录

1. **查看远端目录**
   ```bash
   sftp> pwd
   ```
   确认你目前所在的远端路径（如 `/root/soft/`）

2. **查看远端文件列表**
   ```bash
   sftp> ls -l
   ```
   确认目标文件名完全一致（注意大小写和文件后缀）

3. **查看本地目录**
   ```bash
   sftp> lpwd
   ```
   确认本地当前保存下载文件的位置

4. **（可选）切换本地目录**
   ```bash
   sftp> lcd /desired/local/path
   ```
   将本地工作目录切换到你希望存放文件的路径

### 6.3 常见问题排查

#### "找不到文件"
- 检查 `ls -l` 输出的文件名是否与命令中完全一致（包括大小写、路径）
- 如果当前不在目标目录，可先 `cd /target/path/` 后再执行 `get`

#### 下载后找不到文件
- 确认本地下载目录：使用 `lpwd` 查看当前本地目录，或切换到预期目录后再下载
- 可在本地终端用 `ls` 或文件管理器查看下载结果

### 6.4 Chrome OS SFTP 挂载

在 Chrome OS 上还可创建 SFTP 挂载，直接在 Files App 浏览目标主机文件系统。

### 6.5 文件传输进度监控

- 文件传输时会显示进度条
- 大文件传输可以在后台进行
- 传输完成后会有通知提示
- **新功能**：支持使用File System Access API保存大文件
- **断点续传**：支持下载中断后的续传功能（reget命令）

## 7. 高级配置

### 7.1 SSH隧道配置

#### 本地端口转发：
```bash
ssh -L 本地端口:目标主机:目标端口 用户名@跳板机
```

#### 远程端口转发：
```bash
ssh -R 远程端口:本地主机:本地端口 用户名@远程主机
```

#### 动态端口转发（SOCKS代理）：
```bash
ssh -D 本地端口 用户名@远程主机
```

#### 在Google Secure Shell中配置SSH隧道：
1. 在连接配置中，找到「SSH Relay Server Options」
2. 添加相应的端口转发参数
3. 例如：`--ssh-client-version=2 -L 8080:localhost:80`



### 7.2 连接保持配置

防止连接超时，在SSH连接配置中添加：
```
ServerAliveInterval 60
ServerAliveCountMax 3
```

### 7.3 自定义快捷键

在设置中可以配置：
- 复制：`Ctrl + Shift + C`
- 粘贴：`Ctrl + Shift + V`
- 清屏：`Ctrl + L`
- 中断：`Ctrl + C`
- 新连接：`Ctrl + Shift + N`

**注意：** 更多键盘绑定和快捷键配置可以在官方FAQ中找到详细说明。

## 8. 故障排除

### 8.1 连接问题

#### 连接超时：
- 检查网络连接
- 确认服务器IP和端口正确
- 检查防火墙设置
- 尝试使用其他SSH客户端验证

#### 认证失败：
- 确认用户名和密码正确
- 检查SSH密钥是否正确导入
- 验证服务器是否允许密钥认证
- 检查密钥文件权限

#### 连接中断：
- 启用连接保持功能
- 检查网络稳定性
- 调整超时设置

### 8.2 字体显示问题

#### 字体不生效：
- 确认字体名称拼写正确
- 检查字体是否已安装在系统中
- 尝试使用Web字体
- 清除浏览器缓存

#### 中文显示乱码：
- 设置正确的字符编码（UTF-8）
- 确认服务器locale设置
- 检查终端字体是否支持中文

### 8.3 文件传输问题

#### SFTP连接失败：
- 确认服务器支持SFTP
- 检查用户权限
- 验证SSH连接正常

#### 文件上传失败：
- 检查目标目录权限
- 确认磁盘空间充足
- 验证文件大小限制

## 9. 最佳实践

### 9.1 安全建议

- **使用SSH密钥认证**：比密码认证更安全
- **定期更换密钥**：建议每年更换一次SSH密钥
- **禁用密码认证**：在服务器上禁用密码登录，仅允许密钥认证
- **使用强密码**：如果必须使用密码，确保密码复杂度足够
- **限制登录IP**：在服务器上配置允许登录的IP地址范围

### 9.2 性能优化

- **选择合适的加密算法**：在安全和性能之间找到平衡
- **启用压缩**：对于慢速网络连接，启用SSH压缩可以提高传输速度
- **调整缓冲区大小**：根据网络条件调整SSH缓冲区大小
- **使用连接复用**：对于频繁连接，启用SSH连接复用

### 9.3 工作流程建议

- 为不同项目创建不同的连接配置
- 使用有意义的连接名称
- 定期备份SSH密钥和配置
- 建立标准化的文件传输流程
- **新功能**：支持同步SSH配置文件（/etc/ssh/ssh_config 和 /etc/ssh/ssh_known_hosts）<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>
- 利用Chrome同步功能在多设备间同步连接配置

## 10. 总结

谷歌安全外壳是一个功能强大且易于使用的SSH客户端，特别适合需要在浏览器环境中进行远程服务器管理的用户。通过合理的配置和使用技巧，可以大大提高工作效率。

### 版本更新亮点

最新版本（0.68）包含以下重要改进：<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>
- 改进的SFTP API和文件传输性能
- 支持Mosh WASM工作
- 更好的连接对话框用户体验
- 增强的SSH配置同步功能
- 支持更多的字体连字和键盘绑定

### 使用建议

- 定期更新扩展程序以获得最新功能和安全修复
- 根据实际需求调整配置以获得最佳使用体验
- 对于ChromeOS用户，充分利用SFTP挂载功能提高文件管理效率
- 使用SSH密钥认证替代密码认证以提高安全性
- 关注官方更新日志了解新功能和改进

## 文档编写参考资料

- [Chrome Web Store: Secure Shell Extension](https://chrome.google.com/webstore/detail/pnhechapfaindjhompbnflcldabbghjo)
- [hterm/Secure Shell FAQ](https://hterm.org/x/ssh/faq)
- [官方更新日志](https://hterm.org/x/ssh/changelog)
- [邮件列表](https://hterm.org/x/ssh/contact)