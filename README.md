# AI Sprite Align Tool

## Live Demo

https://zxc02621948-sketch.github.io/ai-sprite-align-tool/

A browser-based tool for fixing misaligned AI-generated sprite sheets.

AI-generated sprite sheets often look good as still images, but each frame may have a different subject position. When imported into a game, the animation can jitter, shake, or appear unstable.

This tool helps align each frame to a consistent anchor point, making AI-generated 2D animation assets more usable in game projects.

---

## Demo

### Before Alignment

The original AI-generated sprite sheet has inconsistent frame positions, causing visible jitter during playback.

![Before alignment](demo/before.gif)

### After Alignment

After using this tool, the frames are aligned to a consistent anchor point, making the animation much more stable.

![After alignment](demo/after.gif)


## What is a Sprite Sheet?

A **sprite** is a 2D image used in games, such as a character, enemy, item, effect, or UI icon.

A **sprite sheet** is a single image that contains multiple animation frames arranged in rows and columns. Games play these frames one by one to create animation.

Example:

```text
[Frame 1][Frame 2][Frame 3][Frame 4]
[Frame 5][Frame 6][Frame 7][Frame 8]
```

---

## Why This Tool Exists

AI image generators can create impressive animation sheets, but they often have alignment problems:

* The character shifts left or right between frames
* The feet or bottom position does not stay stable
* Attack effects extend outside the original frame
* The animation looks shaky when previewed in a game

This tool analyzes each frame, detects the visible subject area, and realigns the frames based on a selected anchor mode.

---

## Features

* Drag and drop PNG / JPG / WebP sprite sheets
* Set custom columns and rows
* Automatically slice the sprite sheet into frames
* Detect subject bounds using transparency / alpha data
* Alignment modes:

  * Subject center
  * Bottom center
  * Visual center of mass
* Choose a reference frame
* Optional overflow sampling margin for effects that cross frame borders
* Subject mask mode that keeps the main body of each frame and avoids copying fragments from neighboring frames
* Row-by-row alignment mode
* Optional output frame expansion to prevent effects from being clipped
* Animation preview
* Export the corrected sprite sheet as PNG
* Runs locally in the browser
* No installation required

---

## How to Use

1. Open `index.html` in your browser.
2. Drop a sprite sheet image into the tool, or click the open file button.
3. Set the number of columns and rows.
4. Choose a reference frame.
5. Click the analyze button to inspect detected bounds and anchor points.
6. Choose an alignment mode.
7. Click auto-align.
8. Preview the animation.
9. Export the corrected PNG.

---

## Recommended Workflow

For AI-generated animation sheets:

1. Generate the sprite sheet with a transparent background if possible.
2. Open it in this tool.
3. Set the correct column and row count, such as `4x2` or `8x1`.
4. Start with **Bottom Center** alignment for characters.
5. Keep **Row-by-row alignment** enabled when the sheet has multiple rows.
6. Keep **Subject mask** enabled when using overflow sampling, so neighboring frame fragments are not copied into the current frame.
7. If an effect is clipped by the original grid, increase the overflow sampling margin. A useful starting range is `40` to `70`.
8. Keep output frame expansion enabled when using overflow sampling.
9. Preview the animation before exporting.
10. Import the corrected sheet into your game project.

---

## Notes

This tool works best with transparent PNG sprite sheets.

If the image has a solid black, white, or colored background, the alpha-based detection may not correctly detect the real subject. In that case, removing the background first will improve the result.

Visual guide:

* Gold frame: original fixed frame area
* White dashed frame: overflow sampling area
* Green frame: detected subject bounds
* Red dot: current alignment anchor

When output frame expansion is enabled, the exported sprite sheet may become larger than the original image. This does not mean the sprite itself was scaled down. The tool adds transparent safety space around each frame so effects are not clipped.

When importing the exported sheet into a game, use the new exported frame size instead of the old original frame size. If needed, scale the displayed sprite in code.

---

## Use Cases

* AI-generated character attack animations
* RPG battle sprites
* Enemy animation sheets
* Skill effect sprite sheets
* Pixel-art style animation cleanup
* 2D game asset preparation
* Game jam asset correction

---

## Running Locally

You can open the tool directly:

```text
index.html
```

Or use the included Windows shortcut:

```bat
run.bat
```

---

## 中文說明：AI 動畫圖格對齊工具

## 線上工具

https://zxc02621948-sketch.github.io/ai-sprite-align-tool/

這是一個本地瀏覽器工具，用來修正 AI 生成 spritesheet 時，每一格主體位置不一致的問題。

AI 很容易生成漂亮的動畫圖，但常見問題是：

* 每一格角色位置不同
* 播放起來會抖動
* 腳底基準線不穩
* 攻擊特效超出原本格子
* 放進遊戲後動畫看起來會飄

這個工具會自動分析每格主體位置，並依照指定的錨點重新對齊，讓 AI 生成的動畫素材更接近遊戲可用狀態。

---

## 展示效果

### 修正前

原本 AI 生成的 spritesheet 每格位置不一致，播放時會明顯抖動。

![修正前](demo/before.gif)

### 修正後

使用工具對齊後，每格主體位置更穩定，動畫播放也更順。

![修正後](demo/after.gif)


## 什麼是精靈圖 / Sprite？

在遊戲開發裡，**Sprite** 指的是遊戲中可以獨立顯示、移動或播放動畫的 2D 圖像，例如：

* 角色
* 敵人
* 道具
* 攻擊特效
* 火球、斬擊、爆炸
* UI 圖示

中文常翻成「精靈圖」，但它不是指妖精，而是遊戲用的 2D 圖像物件。

---

## 什麼是 Spritesheet？

**Spritesheet** 是把多張動畫格集中在同一張圖片裡。

遊戲會依序切出每一格播放，形成動畫。

例如：

```text
[第1格][第2格][第3格][第4格]
[第5格][第6格][第7格][第8格]
```

如果每一格主體沒有對齊，播放時角色就會抖動或亂飄。

---

## 功能

* 支援拖放 PNG / JPG / WebP spritesheet
* 可設定欄列數，例如 4x2、8x1
* 自動切格並偵測每格主體範圍
* 可選擇基準格
* 支援多種對齊方式：

  * 主體中心
  * 底部中心
  * 視覺重心
* 支援外溢取樣邊距，處理特效被格線切到的情況
* 支援主體遮罩，避免外溢取樣時把隔壁格的碎片一起撈進來
* 支援逐列對齊，避免上下排不同動作互相拉歪
* 支援自動擴大輸出格子，避免特效被裁切
* 可即時播放預覽動畫
* 可匯出修正後 PNG
* 完全本地運作，不需要安裝

---

## 使用方式

1. 打開 `index.html`。
2. 將 spritesheet 拖進工具，或按開啟圖檔。
3. 設定欄數與列數。
4. 選擇基準格。
5. 按分析格子，查看主體偵測框與錨點。
6. 選擇對齊方式，角色動畫通常建議先用「底部中心」。
7. 若特效有被格線切到，調整「取樣外溢邊距」。
8. 建議保持「逐列對齊」、「自動擴大格子避免裁切」、「只保留每格主體」開啟。
9. 按自動對齊。
10. 播放預覽，確認動畫是否穩定。
11. 匯出修正後 PNG。

---

## 建議

透明背景 PNG 效果最好。

如果圖片是黑底、白底或其他純色背景，建議先去背再使用，否則工具可能無法正確判斷主體範圍。

角色動畫通常建議使用：

```text
Bottom Center / 底部中心
```

攻擊特效或漂浮物件可以嘗試：

```text
Subject Center / 主體中心
```

如果是 `4x2`、`8x1` 這類 AI 生成的攻擊動畫，建議先從這組設定開始：

```text
對齊方式：底部中心
逐列對齊：開啟
自動擴大格子避免裁切：開啟
只保留每格主體：開啟
取樣外溢邊距：40～70
```

注意：開啟「自動擴大格子避免裁切」後，匯出的 spritesheet 尺寸可能會比原圖大。這不是把圖縮小，而是每一格周圍多了透明安全邊，避免特效被切掉。

放進遊戲時，要用匯出後的新格子尺寸切圖。如果畫面上看起來變小，可以在遊戲程式裡把顯示尺寸放大。

---

## License

License not decided yet.

If this project is released as open source, MIT License is recommended.
