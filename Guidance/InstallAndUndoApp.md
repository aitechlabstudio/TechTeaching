#### List App on Windows Power Shell
```
winget list node
```
#### Install and uninstall Node.js
```
winget install "Node.js"
```
```
winget uninstall "Node.js"
```

#### Install and uninstall codex CLI
##### Method 1

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```
##### Method 2

以**管理员身份**运行 PowerShell，先安装 Node.js：

```powershell
winget install OpenJS.NodeJS.LTS
```

然后安装 Codex：

```powershell
npm install -g @openai/codex
```

##### Uninstall 
```
npm uninstall -g @openai/codex
```
Remove Codex settings and login data
```
Remove-Item "$HOME\.codex" -Recurse -Force
```


