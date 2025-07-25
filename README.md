# Dotfiles

個人的 vim、tmux、nvim 設定檔案同步 repository。

## 檔案結構

```
.
├── .vimrc              # Vim 設定檔
├── .tmux.conf          # Tmux 設定檔
├── nvim/               # Neovim 設定目錄
│   ├── init.lua        # Neovim 主設定檔
│   ├── lazy-lock.json  # 插件版本鎖定檔
│   └── lua/            # Lua 設定檔目錄
│       ├── configs/    # 插件設定檔
│       ├── plugins/    # 自定義插件
│       └── utils/      # 工具函數
├── install.sh          # 自動安裝腳本
└── README.md           # 說明文件
```

## 快速安裝

### 方法一：使用安裝腳本（推薦）

```bash
# Clone repository
git clone https://github.com/MineWang/dotfiles.git
cd dotfiles

# 安裝所有設定
./install.sh

# 或選擇性安裝
./install.sh --vim    # 僅安裝 vim 設定
./install.sh --tmux   # 僅安裝 tmux 設定
./install.sh --nvim   # 僅安裝 nvim 設定

# 自動安裝相依工具（包含 neovim 和 ripgrep）
./install.sh --install-deps

# 強制安裝 neovim
./install.sh --install-neovim

# 安裝 Nerd Fonts（圖示顯示）
./install.sh --install-fonts

# 僅檢查安裝狀態不執行安裝
./install.sh --check-only
```

### 方法二：手動安裝

```bash
# Clone repository
git clone https://github.com/MineWang/dotfiles.git
cd dotfiles

# 備份現有設定（建議）
cp ~/.vimrc ~/.vimrc.backup.$(date +%Y%m%d_%H%M%S) 2>/dev/null || true
cp ~/.tmux.conf ~/.tmux.conf.backup.$(date +%Y%m%d_%H%M%S) 2>/dev/null || true
cp -r ~/.config/nvim ~/.config/nvim.backup.$(date +%Y%m%d_%H%M%S) 2>/dev/null || true

# 複製設定檔
cp .vimrc ~/
cp .tmux.conf ~/
mkdir -p ~/.config
cp -r nvim ~/.config/
```

## 設定說明

### Vim 設定特色

- **Plugin Manager**: vim-plug
- **主要 Plugins**:
  - ALE: 語法檢查與自動修復
  - fzf: 模糊搜尋
  - vim-gitgutter: Git 差異顯示
  - lightline: 狀態列美化
  - PaperColor: 主題
  - Codeium: AI 程式碼補全
  - Claude.vim: Claude AI 整合

- **性能優化**: 延遲載入、快取優化
- **按鍵映射**: Leader key 設為 `,`
- **安全增強**: 禁用不安全功能

### Tmux 設定特色

- **前綴鍵**: `Ctrl-a` (取代預設的 `Ctrl-b`)
- **Vi 模式**: 啟用 vi 風格的按鍵綁定
- **滑鼠支援**: 啟用滑鼠操作
- **預設 Shell**: bash

### Neovim 設定特色

- **Framework**: 基於 NvChad v2.5
- **Plugin Manager**: lazy.nvim
- **主要功能**:
  - 智能剪貼簿系統 (<leader>cpr, <leader>cpp)
  - Claude Code AI 助手整合
  - LSP 自動安裝與配置 (Mason)
  - 現代化的 UI 組件
  - 檔案樹導航
  - 模糊搜尋 (Telescope + ripgrep)
  - 自動會話管理
  - Git 整合
  - Blink.cmp 高效能補全引擎 (Ctrl-j/k 導航, Ctrl-n 手動觸發)

## 安裝後步驟

### Vim
1. 開啟 vim
2. 執行 `:PlugInstall` 安裝 plugins
3. 重啟 vim

### Tmux
1. 重啟 tmux 或執行 `tmux source-file ~/.tmux.conf`
2. 新的設定立即生效

### Neovim
1. 腳本會自動安裝 neovim (如未安裝)
2. 開啟 nvim，NvChad 會自動安裝所需的 plugins
3. 等待安裝完成
4. 在終端設定中選擇 Nerd Font (如 FiraCode Nerd Font)
5. 測試功能：
   - 智能剪貼簿：選取代碼後按 <leader>cpr
   - Claude Code：按 <leader>cc 開啟 AI 助手

## 相依性需求

### 必要工具
- vim
- tmux  
- curl (用於下載 vim-plug)

### 核心工具（自動安裝）
- **neovim 0.8.0+** (主要編輯器)
  - 支援包管理器安裝 (brew, apt, yum, dnf, pacman)
  - 支援 AppImage 安裝 (Linux 無權限時)
  - 支援源碼編譯安裝 (最後選項)
- **ripgrep** (NvChad 搜尋功能)
  - 支援包管理器安裝
  - 支援預編譯二進制下載
  - 支援 cargo 安裝
- **Nerd Fonts** (圖示顯示)
  - 自動檢測系統字體目錄
  - 智能選擇字體安裝方式
  - 支援 macOS 和 Linux 平台

### 選用工具
- git (用於 plugin 管理)
- fd (用於更快的檔案搜尋)
- Nerd Fonts (正確顯示圖示)

## 故障排除

### Vim Plugins 安裝失敗
```bash
# 手動安裝 vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# 重新安裝 plugins
vim +PlugInstall +qall
```

### Tmux 設定未生效
```bash
# 重新載入設定
tmux source-file ~/.tmux.conf

# 或重啟 tmux
tmux kill-server
tmux
```

### Neovim 錯誤
```bash
# 清除 nvim 快取
rm -rf ~/.local/share/nvim
rm -rf ~/.cache/nvim

# 重新開啟 nvim
nvim
```

### 工具安裝問題
```bash
# 檢查安裝狀態
./install.sh --check-only

# 強制重新安裝 neovim
./install.sh --install-neovim

# 自動安裝所有缺失工具
./install.sh --install-deps

# 安裝 Nerd Fonts 修復圖示問題
./install.sh --install-fonts
```

## 自訂設定

如需修改設定，請直接編輯對應的設定檔：
- Vim: `~/.vimrc`
- Tmux: `~/.tmux.conf`  
- Neovim: `~/.config/nvim/init.lua`

## 授權

MIT License

## 更新記錄

- 2025-07-27: 
  - 強化安裝腳本安全性：URL 驗證、檔案完整性檢查、錯誤處理優化
  - 更新 NvChad blink.cmp 配置與文檔同步
- 2025-07-26: 
  - 新增 neovim 和 ripgrep 自動安裝功能，支援多平台和無權限安裝
  - 新增 Nerd Fonts 自動安裝功能，修正圖示顯示問題
  - 修正 vim 插件版本參考和相容性問題
- 2025-07-25: 更新 NvChad 配置，新增 Claude Code 和智能剪貼簿功能
- 2025-07-23: 初始版本，包含 vim、tmux、nvim 設定