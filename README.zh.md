> [!NOTE]
> 此 README 由 [SKILL](https://github.com/pardnchiu/skill-readme-generate) 生成，英文版請參閱 [這裡](./README.md)。

# skill-version-generate

[![license](https://img.shields.io/github/license/pardnchiu/skill-version-generate)](LICENSE)

> Claude Code 技能：從 git tag 到 HEAD 自動生成結構化變更日誌並推薦語義化版本號<br>
> 此專案主要由 [Claude Code](https://claude.ai/claude-code) 生成，作者僅做部分調整。

## 目錄

- [功能特點](#功能特點)
- [安裝](#安裝)
- [使用方法](#使用方法)
- [分類標籤參考](#分類標籤參考)
- [授權](#授權)

## 功能特點

- **自動版本偵測**：從 git 標籤取得最新語義化版本
- **智能分類**：根據變更類型自動分類（FEAT、FIX、BREAKING 等）
- **語義化版本計算**：依據變更自動計算 MAJOR、MINOR、PATCH 升級
- **雙語輸出**：生成的變更日誌包含英文描述與中文翻譯
- **結構化格式**：輸出清晰的 Markdown 格式變更日誌

## 安裝

將此技能加入 Claude Code 技能目錄：

```bash
# 複製到 Claude Code 技能目錄
git clone https://github.com/pardnchiu/skill-version-generate ~/.claude/skills/version-generate
```

## 使用方法

在專案目錄中使用 Claude Code 呼叫此技能：

```
/version-generate
```

技能將自動執行以下流程：

1. **版本偵測**：取得最新的語義化版本標籤（如 `v1.2.3`）
2. **變更收集**：分析從標籤到 HEAD 的所有 git 差異
3. **分類計算**：根據變更類型決定版本升級幅度
4. **生成輸出**：建立 `vA.B.C.md` 變更日誌檔案

### 版本升級規則

| 變更類型 | 版本影響 |
|----------|----------|
| `BREAKING` | MAJOR (+1.0.0) |
| `FEAT` | MINOR (+0.1.0) |
| `FIX`, `UPDATE`, `SECURITY`, `REFACTOR`, `PERF` | PATCH (+0.0.1) |
| `STYLE`, `DOC`, `TEST`, `CHORE` | 不升版 |

### 輸出範例

生成的檔案格式如 `v1.3.0.md`：

```markdown
> v1.2.3 -> v1.3.0

## Summary

新增任務排程功能並修正記憶體洩漏問題。

## Changes

### FEAT
- Add task scheduler with cron expression support

### FIX
- Fix memory leak in worker pool cleanup
```

## 分類標籤參考

| 標籤 | 範圍 | 範例 |
|-----|-------|--------|
| `FEAT` | 新功能 | 新函式、端點、元件 |
| `FIX` | 錯誤修正 | 錯誤處理、邏輯修正 |
| `UPDATE` | 修改現有行為 | 參數變更、演算法調整 |
| `ADD` | 新增檔案/資源 | 設定檔、資源、相依性 |
| `REMOVE` | 刪除 | 棄用程式碼、未使用檔案 |
| `REFACTOR` | 程式碼重構 | 提取函式、重新命名 |
| `PERF` | 效能改善 | 快取、演算法最佳化 |
| `STYLE` | 格式化 | 空白、linting |
| `DOC` | 文件 | 註解、README |
| `TEST` | 測試 | 新測試、測試修正 |
| `CHORE` | 維護 | CI/CD、工具設定 |
| `SECURITY` | 安全性修補 | 漏洞修正 |
| `BREAKING` | 破壞性變更 | API 簽章變更 |

## 授權

本專案採用 [MIT LICENSE](LICENSE)。
