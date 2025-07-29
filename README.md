# 谷歌安全外壳（Google Secure Shell）详细使用教程

## 简介

谷歌安全外壳（Google Secure Shell）是一个基于Chrome浏览器的SSH客户端扩展程序，它允许用户直接在浏览器中连接到远程服务器，无需安装额外的SSH客户端软件。<mcreference link="https://chrome.google.com/webstore/detail/secure-shell/iodihamcpbpeioajjeobimgagajmlibd" index="2">2</mcreference> 该扩展由Google开发，提供xterm兼容的终端模拟器和独立的SSH客户端功能。<mcreference link="https://chrome.google.com/webstore/detail/secure-shell/iodihamcpbpeioajjeobimgagajmlibd" index="2">2</mcreference>

**当前版本：** 0.68（2025年2月更新）<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>

**官方地址：** https://chromewebstore.google.com/detail/iodihamcpbpeioajjeobimgagajmlibd?utm_source=item-share-cb

**重要提醒：** Chrome App版本已被弃用，所有用户（包括ChromeOS用户）应尽快迁移到扩展版本。<mcreference link="https://chrome.google.com/webstore/detail/deprecated-secure-shell-a/pnhechapfaindjhompbnflcldabbghjo" index="5">5</mcreference>

## 安装步骤

### 1. 安装Chrome扩展

1. 打开Chrome浏览器
2. 访问上述官方地址
3. 点击「添加至Chrome」按钮
4. 在弹出的确认对话框中点击「添加扩展程序」
5. 安装完成后，在Chrome的扩展程序栏会出现SSH图标

### 2. 启动应用

- 方法一：点击Chrome工具栏中的SSH图标
- 方法二：在Chrome地址栏输入 `chrome://apps/` 然后点击「Secure Shell App」
- 方法三：在新标签页的应用程序中找到并点击

## 基本配置和使用

### 1. 创建SSH连接

1. 启动应用后，点击「[New Connection]」
2. 填写连接信息：
   - **Username（用户名）**：远程服务器的用户名
   - **Hostname（主机名）**：服务器IP地址或域名
   - **Port（端口）**：SSH端口（默认22）
   - **Connection Name（连接名称）**：为此连接起一个便于识别的名字

3. 点击「Connect」建立连接
4. 首次连接时会提示输入密码

### 2. 保存SSH会话

连接成功后，该连接会自动保存在连接列表中，下次可以直接点击连接名称快速连接。

### 3. 保存密码（密钥认证）

#### 方法一：使用SSH密钥（推荐）

1. 在连接配置中，点击「Import...」
2. 选择你的私钥文件（通常是 `id_rsa` 或 `id_ed25519`）
3. 如果私钥有密码保护，输入密钥密码
4. 保存后，以后连接将自动使用密钥认证

#### 方法二：生成新密钥对

1. 在主界面点击「Generate...」
2. 选择密钥类型（推荐 Ed25519）
3. 设置密钥长度和密码（可选）
4. 生成后将公钥添加到服务器的 `~/.ssh/authorized_keys` 文件中

## 字体和外观配置

### 1. 访问设置

1. 在SSH连接窗口中，按 `Ctrl + Shift + P`（Windows/Linux）或 `Cmd + Shift + P`（Mac）
2. 或者右键点击终端区域，选择「Settings」

### 2. 字体配置

在设置页面中找到「Appearance」部分：

#### 热门字体推荐及配置：

**1. Fira Code（支持连字符）**
```
font-family: 'Fira Code', monospace
font-size: 14
```

**2. JetBrains Mono**
```
font-family: 'JetBrains Mono', monospace
font-size: 14
```

**3. Cascadia Code（微软开发）**
```
font-family: 'Cascadia Code', monospace
font-size: 14
```

**4. Source Code Pro**
```
font-family: 'Source Code Pro', monospace
font-size: 14
```

**5. Consolas（Windows系统字体）**
```
font-family: 'Consolas', monospace
font-size: 14
```

### 3. 颜色主题配置

#### 暗色主题示例：
```
background-color: #1e1e1e
foreground-color: #d4d4d4
cursor-color: #ffffff
```

#### 亮色主题示例：
```
background-color: #ffffff
foreground-color: #000000
cursor-color: #000000
```

#### Solarized Dark主题：
```
background-color: #002b36
foreground-color: #839496
cursor-color: #93a1a1
```

### 4. 完整配置示例

在设置页面中，可以通过以下方式配置终端外观：

**字体设置：**
```
font-family: 'Fira Code', 'JetBrains Mono', monospace
font-size: 14
```

**颜色设置：**
```
background-color: #1e1e1e
foreground-color: #d4d4d4
cursor-color: #ffffff
```

**行为设置：**
```
cursor-blink: true
scrollbar-visible: true
scroll-on-output: false
scroll-on-keystroke: true
```

**注意：** 设置页面可以通过右键点击终端区域并选择「Settings」或按 `Ctrl + Shift + P` 访问。

## 多窗口管理

### 1. 打开多个SSH窗口

#### 方法一：新标签页方式
1. 在已有SSH连接的标签页中，按 `Ctrl + T` 打开新标签页
2. 在新标签页中访问 `chrome://apps/` 并启动Secure Shell App
3. 建立新的SSH连接

#### 方法二：右键菜单方式
1. 右键点击Chrome工具栏中的SSH图标
2. 选择「在新标签页中打开」
3. 重复此操作可打开多个实例

#### 方法三：书签方式
1. 将 `chrome-extension://iodihamcpbpeioajjeobimgagajmlibd/html/nassh.html` 添加为书签
2. 可以创建多个书签，每个对应不同的连接配置
3. 通过书签栏快速打开多个SSH会话

### 2. 窗口管理技巧

- **标签页重命名**：右键点击标签页，选择重命名，输入服务器名称便于识别
- **固定标签页**：右键点击标签页，选择「固定标签页」，标签页会变小并固定在左侧
- **标签页分组**：右键选择「将标签页添加到新群组」，可以按项目或环境分组管理

### 3. 快捷键操作

- `Ctrl + Shift + T`：重新打开最近关闭的标签页
- `Ctrl + Tab`：切换到下一个标签页
- `Ctrl + Shift + Tab`：切换到上一个标签页
- `Ctrl + W`：关闭当前标签页
- `Ctrl + Shift + N`：打开新的隐身窗口

## 文件传输功能

### 1. SFTP文件管理器

#### 启用SFTP功能：
**方法一：连接对话框中启用**
1. 在创建新连接时，勾选「SFTP Mount」选项
2. 设置「Mount Path」（默认为用户主目录，可设置为"/"访问根目录）<mcreference link="https://superuser.com/questions/1532799/mounting-sftp-to-files-on-chromeos-using-secure-shell-app-but-no-files-are-showi" index="3">3</mcreference>
3. 连接成功后会自动在Chrome OS的文件应用中创建SFTP挂载点

**方法二：已有连接中启用**
1. 在SSH连接建立后，点击「SFTP Mount」按钮
2. 输入密码进行认证
3. 挂载点会出现在文件应用的侧边栏中

#### 使用SFTP界面：
1. **Chrome OS用户**：SFTP挂载会直接显示在文件应用中，无需保持SSH窗口打开<mcreference link="https://www.reddit.com/r/chromeos/comments/68nov6/secure_shell_app_now_does_sftp/" index="2">2</mcreference>
2. **其他平台用户**：界面会分为两部分：终端和文件管理器
3. 可以通过图形界面浏览、上传、下载文件
4. 支持从文件应用直接访问远程文件系统<mcreference link="https://secure-shell.en.softonic.com/chrome/extension" index="4">4</mcreference>

### 2. 文件上传

#### 方法一：拖拽上传
1. 直接将本地文件拖拽到SFTP文件管理器窗口
2. 文件会自动上传到当前目录

#### 方法二：右键上传
1. 在SFTP文件管理器中右键点击空白区域
2. 选择「Upload Files」
3. 选择要上传的文件

#### 方法三：命令行上传（使用rz命令）
```bash
# 首先在服务器上安装lrzsz
sudo apt-get install lrzsz  # Ubuntu/Debian
sudo yum install lrzsz      # CentOS/RHEL
sudo dnf install lrzsz      # Fedora

# 使用rz命令接收文件
rz
```
然后在弹出的对话框中选择要上传的文件。

**注意：** 现代版本的Google Secure Shell主要依赖SFTP协议进行文件传输，rz/sz命令可能在某些配置下不可用。<mcreference link="https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server" index="2">2</mcreference>

### 3. 文件下载

#### 方法一：SFTP界面下载
1. 在SFTP文件管理器中右键点击要下载的文件
2. 选择「Download」
3. 选择本地保存位置

#### 方法二：命令行下载（使用sz命令）
```bash
# 下载单个文件
sz filename

# 下载多个文件
sz file1 file2 file3
```

### 4. 批量文件操作

#### 批量上传：
1. 选择多个文件（按住Ctrl键点击）
2. 拖拽到SFTP窗口
3. 或使用「Upload Files」选择多个文件

#### 批量下载：
1. 在SFTP界面中按住Ctrl键选择多个文件
2. 右键选择「Download Selected」

### 5. 文件传输进度监控

- 文件传输时会显示进度条
- 大文件传输可以在后台进行
- 传输完成后会有通知提示
- **新功能**：支持使用File System Access API保存大文件<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>
- **断点续传**：支持下载中断后的续传功能（reget命令）<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>

## 高级配置

### 1. SSH隧道配置

#### 本地端口转发：
在连接配置的「SSH Relay Server Options」中添加：
```
--ssh-agent=<extension_id>
```

#### 使用SSH Agent扩展：
Google提供了专门的SSH Agent扩展来管理密钥：<mcreference link="https://github.com/google/chrome-ssh-agent" index="4">4</mcreference>
1. 安装SSH Agent for Google Chrome扩展
2. 在连接配置中添加：`--ssh-agent=eechpbnaifiimgajnomdipfaamobdfha`
3. 这样可以使用智能卡或其他高级认证方式

#### 端口转发示例：
```
# 本地端口转发
ssh -L 本地端口:目标主机:目标端口 用户名@跳板机

# 远程端口转发
ssh -R 远程端口:本地主机:本地端口 用户名@远程主机
```

### 2. 连接保持配置

在连接的「SSH Relay Server Options」中添加：
```
--resume-connection
```
这将启用自动重连功能。<mcreference link="https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/options.md" index="1">1</mcreference>

或在SSH配置文件中添加：
```
ServerAliveInterval 60
ServerAliveCountMax 3
```

### 3. 自定义快捷键

在设置中可以配置：
- 复制：`Ctrl + Shift + C`
- 粘贴：`Ctrl + Shift + V`
- 清屏：`Ctrl + L`
- 中断：`Ctrl + C`
- 新连接：`Ctrl + Shift + N`<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>

**注意：** 更多键盘绑定和快捷键配置可以在官方FAQ中找到详细说明。<mcreference link="https://chromium.googlesource.com/apps/libapps/+/hterm-1.80/nassh/doc/FAQ.md" index="2">2</mcreference>

## 故障排除

### 1. 连接问题

**问题：无法连接到服务器**
- 检查网络连接
- 确认服务器IP和端口正确
- 检查防火墙设置
- 确认SSH服务正在运行

**问题：认证失败**
- 检查用户名和密码
- 确认SSH密钥配置正确
- 检查服务器的SSH配置

### 2. 字体显示问题

**问题：字体不显示或显示异常**
- 确保系统已安装指定字体
- 尝试使用系统默认等宽字体
- 清除浏览器缓存后重试

### 3. 文件传输问题

**问题：无法上传/下载文件**
- 检查SFTP功能是否启用
- 确认服务器支持SFTP
- 检查文件权限
- 确认磁盘空间充足

## 最佳实践

### 1. 安全建议

- 使用SSH密钥认证而非密码认证
- 定期更换SSH密钥
- 不要在公共网络上保存敏感连接信息
- 使用强密码保护私钥

### 2. 性能优化

- 关闭不必要的视觉效果
- 适当调整字体大小和缓冲区大小
- 定期清理连接历史

### 3. 工作流程建议

- 为不同项目创建不同的连接配置
- 使用有意义的连接名称
- 定期备份SSH密钥和配置
- 建立标准化的文件传输流程
- **新功能**：支持同步SSH配置文件（/etc/ssh/ssh_config 和 /etc/ssh/ssh_known_hosts）<mcreference link="https://chromium.googlesource.com/apps/libapps/+/HEAD/nassh/docs/ChangeLog.md" index="1">1</mcreference>
- 利用Chrome同步功能在多设备间同步连接配置

## 总结

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

**官方资源：**
- FAQ：https://hterm.org/x/ssh/faq
- 更新日志：https://hterm.org/x/ssh/changelog
- 邮件列表：https://hterm.org/x/ssh/contact