# Tmux 設定檔

個人的 Tmux 設定檔，基於 Catppuccin 主題打造簡潔、現代且實用的終端體驗。

此設定檔參考了 [這個 GitHub 討論串](https://github.com/catppuccin/tmux/discussions/317#discussioncomment-11064512)。

## 截圖

![Tmux 設定截圖](Screenshot.png)

## 功能特色

### 主題配色

*   使用 Catppuccin (Mocha) 色票，色彩定義於 `colors.conf`。

### 自訂狀態列

狀態列位於頂部，顯示以下資訊：

**左側：**
*   工作階段名稱（按下 prefix 時高亮顯示）
*   當前執行的指令
*   當前路徑
*   縮放狀態

**右側：**
*   CPU 使用率
*   記憶體使用率
*   主要 IP 位址
*   電池電量（低於 20% 時高亮警示）
*   日期與時間

### 視窗顯示

*   使用編號模式顯示視窗（自動重新命名）
*   視窗索引從 1 開始

### 快捷鍵

| 快捷鍵 | 功能 |
| :--- | :--- |
| `prefix` + `r` | 重新載入設定檔 |
| `prefix` + `-` | 垂直分割面板 |
| `prefix` + `\` | 水平分割面板 |
| `prefix` + `v` | 進入複製模式 |
| `v`（複製模式中） | 開始選取 |
| `y`（複製模式中） | 複製選取內容 |

### 其他設定

*   啟用滑鼠支援
*   啟用 passthrough 模式
*   監控視窗活動
*   使用 vi 模式按鍵
*   256 色終端支援
*   escape-time 設為 0（適合 Neovim 使用者）

### 外掛（透過 TPM 管理）

TPM 會在首次啟動時自動安裝。使用的外掛如下：

| 外掛 | 用途 |
| :--- | :--- |
| `tmux-plugins/tpm` | Tmux 外掛管理器 |
| `tmux-plugins/tmux-battery` | 電池狀態顯示 |
| `tmux-plugins/tmux-cpu` | CPU 使用率顯示 |
| `thewtex/tmux-mem-cpu-load` | 記憶體使用率顯示 |
| `laktak/extrakto` | 文字擷取工具 |
| `christoomey/vim-tmux-navigator` | Vim 與 Tmux 間無縫切換面板 |
| `dreknix/tmux-primary-ip` | 主要 IP 位址顯示 |

## 安裝

1.  **複製專案：**
    ```bash
    git clone https://github.com/vulcanshen/primary-tmux.git ~/.config/tmux
    ```
2.  **啟動 Tmux**，TPM 會自動安裝。或手動安裝：
    ```bash
    git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
    ```
3.  **安裝外掛：**
    *   啟動 Tmux 後按下 `prefix` + `I`（大寫 I）來安裝外掛。

## Neovim (Lualine)

本專案包含 `lualine.lua` 設定檔，用於配置 Neovim 的 Lualine 狀態列外掛，使其與 Tmux 主題風格一致。

### 安裝方式

將 `lualine.lua` 複製到 LazyVim 的外掛目錄下：

```bash
cp ~/.config/tmux/lualine.lua ~/.config/nvim/lua/plugins/lualine.lua
```

### 功能特色

*   **Catppuccin 配色：** 使用與 Tmux 相同的 Catppuccin mocha 色票
*   **自訂元件：** 狀態列包含以下資訊：
    *   模式指示器
    *   Git 分支與差異狀態
    *   檔案圖示、名稱與狀態
    *   緩衝區列表（目前/總計）
    *   檔案格式、編碼與大小
    *   診斷資訊（錯誤、警告、提示）
    *   進度與游標位置
*   **自訂分隔符號：** 使用 `|` 作為分隔符號，呈現簡潔現代的外觀

## Neovim (vim-tmux-navigator)

搭配 `christoomey/vim-tmux-navigator` 外掛，可以在 Tmux 與 Neovim 之間使用 `Ctrl` + `h/j/k/l` 無縫切換面板。

### Neovim 端設定

將以下設定檔放置於 LazyVim 的外掛目錄下 `~/.config/nvim/lua/plugins/vim-tmux-navigator.lua`：

```lua
return {
  "christoomey/vim-tmux-navigator",
  cmd = {
    "TmuxNavigateLeft",
    "TmuxNavigateDown",
    "TmuxNavigateUp",
    "TmuxNavigateRight",
    "TmuxNavigatePrevious",
    "TmuxNavigatorProcessList",
  },
  keys = {
    { "<c-h>", "<cmd><C-U>TmuxNavigateLeft<cr>" },
    { "<c-j>", "<cmd><C-U>TmuxNavigateDown<cr>" },
    { "<c-k>", "<cmd><C-U>TmuxNavigateUp<cr>" },
    { "<c-l>", "<cmd><C-U>TmuxNavigateRight<cr>" },
    { "<c-\\>", "<cmd><C-U>TmuxNavigatePrevious<cr>" },
  },
}
```

### 快捷鍵對照

| 快捷鍵 | 功能 |
| :--- | :--- |
| `Ctrl` + `h` | 切換到左方面板 |
| `Ctrl` + `j` | 切換到下方面板 |
| `Ctrl` + `k` | 切換到上方面板 |
| `Ctrl` + `l` | 切換到右方面板 |
| `Ctrl` + `\` | 切換到上一個面板 |

## 色票

色票定義於 `colors.conf`，基於 Catppuccin Mocha 主題。

| 色彩名稱 | 色碼 |
| :--- | :--- |
| Rosewater | `#f5e0dc` |
| Flamingo | `#f2cdcd` |
| Pink | `#f5c2e7` |
| Mauve | `#cba6f7` |
| Red | `#f38ba8` |
| Maroon | `#eba0ac` |
| Peach | `#fab387` |
| Yellow | `#f9e2af` |
| Green | `#a6e3a1` |
| Teal | `#94e2d5` |
| Sky | `#89dceb` |
| Sapphire | `#74c7ec` |
| Blue | `#89b4fa` |
| Lavender | `#b4befe` |
| Text | `#cdd6f4` |
| Subtext1 | `#bac2de` |
| Subtext0 | `#a6adc8` |
| Overlay2 | `#9399b2` |
| Overlay1 | `#7f849c` |
| Overlay0 | `#6c7086` |
| Surface2 | `#585b70` |
| Surface1 | `#45475a` |
| Surface0 | `#313244` |
| Base | `#1e1e2e` |
| Mantle | `#181825` |
| Crust | `#11111b` |

## Credits

Inspired by / based on [naivecynics](https://github.com/naivecynics/primary-tmux)
