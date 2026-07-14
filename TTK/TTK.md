# TTK Test - ESP & Aimbot Console 功能列表

本文件整理並記錄了 `TTK.lua` 腳本中所包含的所有核心功能、進階功能與自定義設定。

---

## 1. 視覺效果 (Visuals - ESP)
基於 Roblox Drawing 庫實現的畫線與透視功能，直接對齊伺服器真實的 `MercHitboxes`。

* **ESP 主開關 (Enable ESP Master)**：開啟或關閉所有 ESP 繪製。
* **顯示方框 (Show Box)**：在敵人身上繪製二維包圍框。
* **顯示射線 (Show Tracer Line)**：從設定起點（可選螢幕底端或中心）連線至敵人的腳底。
* **顯示骨骼 (Show Skeleton)**：繪製敵人的骨骼線段（完全貼合遊戲 R15 人物模型骨架）。
* **顯示玩家名稱 (Show Player Name)**：顯示玩家名稱並附帶目前血量百分比（例如 `Player [100%]`）。
* **顯示距離資訊 (Show Distance Info)**：顯示與目標的距離（公尺為單位）。
* **顯示視線方向線 (Show Player Look Line)**：從目標頭部向前畫一條射線，標示其視線面向。
* **可見度綠色標示 (VisCheck)**：
  * 當目標可被射擊（未被地圖掩體遮擋）時，ESP 顏色會自動轉換為可見顏色（預設綠色）。
  * 排除 `MercPlayers` 自身的碰撞遮擋。
  * 自動穿透具備 `Glass`（玻璃）與 `Glass_Fragile`（易碎玻璃）標籤的障礙物。
* **隊友過濾 (Team Filter)**：隱藏盟友，僅對敵方玩家生效。

---

## 2. 自動瞄準 (Aimbot - 相機模擬自瞄)
透過滑鼠移動模擬真實滑鼠操作的相機自瞄，實現人性化的瞄準修正。

* **自瞄開關 (Enable Camera Aimbot)**：啟用後開始處理自瞄邏輯。
* **持續鎖定 (Always On)**：略過熱鍵綁定，免按鍵持續將鏡頭鎖定在 FOV 範圍內的最近目標。
* **自瞄熱鍵 (Aimbot Hotkey)**：自選按鍵（例如滑鼠右鍵），當「持續鎖定」關閉時，按住此鍵才會鎖定。
* **自瞄部位 (Aim Target Part)**：
  * `Auto`（露哪打哪）：優先鎖定可見度檢查通過的部位（頭 -> 軀幹 -> 腿）。
  * `Head`（頭部固定）。
  * `Torso`（軀幹固定）。
  * `Leg`（腿部固定）。
* **平滑度 (Smoothing)**：1 至 20 級平滑滑鼠移動。級數越高移動越慢越不容易被防作弊偵測，1 則為直接瞬間鎖定。
* **顯示自瞄範圍圈 (Show Aimbot FOV Circle)**：繪製以**槍口真實彈道指向（動態準星）**為中心的 FOV 圓圈。
* **自瞄半徑 (Aimbot FOV Radius)**：設定自瞄有效的像素半徑（30 - 500 px）。
* **障礙物過濾 (Wall Check)**：跳過掩體後的目標。

---

## 3. 靜默自瞄 (Silent Aim)
直接攔截並修改子彈彈道發射方向，外觀無移動相機，但子彈必定精準命中目標。

* **靜默自瞄開關 (Enable Silent Aim)**：啟用或關閉靜默自瞄。
* **瞄準部位 (Target Part)**：可選 `Auto`（露哪打哪）、`Head`（頭部）、`Torso`（軀幹）、`Leg`（腿部）。
* **鎖定中心模式 (Silent FOV Type)**：
  * `Center`（螢幕中心固定）：以螢幕幾何中心為基準搜尋 FOV 內的目標。
  * `Dynamic`（對齊槍口動態）：以真實槍口射向在螢幕上的投影點為基準搜尋目標。
* **顯示範圍 (Show Silent Aim FOV)**：繪製靜默自瞄的 FOV 圓圈。
* **範圍半徑 (Silent Aim FOV Radius)**：設定靜默自瞄的有效半徑（30 - 800 px）。
* **障礙物過濾 (Wall Check)**：子彈只會導向露出的部位。
* **目標鎖定線 (Show Target Line)**：在靜默鎖定基準點與當前鎖定目標之間繪製連線。

---

## 4. 其他修改與輔助 (Misc Modifications)
修改遊戲核心機制，包含後座力、彈道散佈、彈藥與投擲物等。

* **虛擬準星 (Virtual Crosshair)**：
  * 由於此遊戲腰射時子彈射向與螢幕中心有大幅偏差，此準星會**自動對齊槍口 Attachment 的真實落點**，即使在開火晃動、機瞄、移動時也能給出子彈的準確落點。
  * 準星類型：可選 `Dot`（紅點）、`Cross`（小十字）。
  * 支援大小調整與自定義顏色。
* **無後座力 (No Recoil)**：Hook 相機控制器，並在渲染幀中實時將槍枝的後座 Spring 歸零，畫面完全不抖動。
* **無彈道散佈 (No Spread)**：修改武器執行期的彈道散佈角（SpreadAngle）為 0，子彈必定走直線。
* **關閉開火動畫 (Disable Gun Animation)**：關閉第一人稱手部武器模型的開火動畫與視模後座，使畫面中的瞄準鏡物理狀態更加穩定。
* **子彈穿牆 (Enable Wallbang)**：Hook BulletController 並將 ActiveMap 地圖加入到射線的忽視清單中，實現物理子彈直接穿牆擊殺。
* **強制全自動 (Force Auto Mode)**：強制將所有武器的開火模式修改為 `Auto`（全自動）。
* **無限彈藥 (Infinite Ammo)**：開啟後武器開火不消耗備彈，且彈匣容量鎖定為超大容量（999 彈匣容量，99999 備彈）。

---

## 5. 投擲物修改 (Throwables)
* **防閃光彈 (Anti-Flashbang)**：
  * 免疫閃光彈造成的白光模糊。
  * 免疫閃光彈造成的耳鳴與高頻噪音。
  * 移除閃光彈導致的「無法衝刺（Sprint Block）」狀態。

---

## 6. 系統設定 (Settings)
* **語言選擇 (Language / 語言)**：支援在 **繁體中文 (zh-tw)** 與 **English (en-us)** 之間一鍵切換，介面文字會動態重新加載。
* **自適應語系偵測**：啟動時自動檢測 `Tsetingnil_script/keysystem.json` 的配置以自適應載入英文或繁體中文。
* **最大渲染距離 (Max Render Distance)**：ESP 最大可視長度限制（100m - 5000m）。
* **線條粗細 (Line Thickness)**：畫線的像素粗細。
* **不透明度 (Opacity)**：ESP 文字與畫線的透明度。
* **射線起點 (Tracer Origin)**：設定 ESP Tracer Line 的來源起點為螢幕底部中心（Bottom Center）或螢幕中心（Screen Center）。
* **自定義顏色 (Colors)**：
  * 敵人 ESP 顏色
  * 隊友/盟友 ESP 顏色
  * 可見目標 (VisCheck) ESP 顏色
* **配置存取 (Configuration)**：
  * **儲存配置 (Save Config)**：將當前所有設定值寫入至本地檔案 `Tsetingnil_script/TTK/config.json`。
  * **載入配置 (Load Config)**：手動重新讀取本地檔案。
  * **自動載入配置 (Auto Load Config)**：開啟後，未來啟動此腳本時會自動套用已儲存的配置。
* **卸載腳本 (Unload ESP)**：還原所有 Hook，銷毀所有 Drawing 物件與 GUI 視窗，徹底清理記憶體殘留。
