# 關於我重灌後成為踩雷大師的那件事 (上)

## 序
最近不小心就當了社畜，原因是怎樣就懶得說了呢。  
直接切進正題，公司每個人發配了一台電腦（規格 略），以效能來說有點接近我平常使用的 mac ，除了那少得可憐的 ram，光是開機進桌面就用掉了將近 60% 的記憶體。  
身為一個不專業的軟體攻城屍，寫個 Code 不開個幾十頁的分頁怎麼可能夠 (~~加上我用的是 Chrome~~)，在 mac 上記憶體當然是加好加滿的情況下，我很不適應，加上開發過程中 Windows 各種坑搞得我很不爽。  
> 來移民吧  
> 回去用 Linux 吧

所以開啟了移民之旅。

## Linux Distro
光是選擇 Linux 的發布版本我個人就猶豫了很久。
 - [Ubuntu](http://ubuntu.com)
 - [debian](http://debian.org)
 - [neon](https://neon.kde.org/)

其他的 distro 就不怎麼考慮了。
於是我就開始一個一個挑選了 ~~購物中的女性上身~~，選來選去最後用了 [debian](http://debian.org)  
結果是踩坑的開始。

## 字
不知道為什麼搞得，debian 下的 atom, vscode 文字渲染很詭異。  
ref issue: 
 - https://github.com/microsoft/vscode/issues/35675
 - https://github.com/Microsoft/vscode/issues/62501

對 我也遇到了一樣的問題，即使裝了比較正常的字體例如 FiraCode 輸入完整的 Font Family Name 依舊不會正常顯示，好在全球最大攻城屍交友網站有人提出了降級 libfreetype6 到指定版本就可以正常使用了。  
下完指令後電腦身亡。
於是開始了另一段旅程

## 雙系統
就如同前面所說的，~~發大財~~ 雙系統是總目標，上網找了些許的資料就來動手。   
這邊就不另外贅述 UEFI 以及傳統開機的區別了，只講重點。

 ### 空間
 以我自身的電腦是 256G SSD 來說我切了 40G 才算剛好使用，使用了 Windows 內建的磁碟管理壓縮功能就可達成，不過這邊建議使用免費的 [MiniTool Partition Wizard](https://www.partitionwizard.com)，基本上都很簡單的就能完成操作。  
 選定目標磁碟再點擊 `split` 就能順利操作，操作過程中他會幫你重開機進入黑色畫面是正常的，期間不要按任何按鈕，開機完成後就可以看到完成分割的硬碟。
 ![img](https://dr.sudo.host/YB6ZZ8+)

 ## 作業系統
 後來我選擇了 Ubuntu 了，下載 `.iso` 後使用 [refus](http://rufus.ie) 寫入到隨身碟。  
 步驟太簡單懶得拍。

 ## 前置步驟
 東西準備好了之後開始一些安裝前的工作。  
 關閉 `Windows快速啟動`  
    控制台 -> 電源選項 -> 按下電源行為 -> Windows快速啟動
    ![img](https://dr.sudo.host/koXL3s+)  

 進入 BIOS  
 關閉 Intel Rapid Start Technology  
 關閉 Secure boot
 
 ## 安裝
 先進入 BIOS 內將隨身碟選為第一個，或是直接點擊 `F12` 進入開機選單（有些 BIOS 可能沒有這個）
 接著就是開心的安裝時間。  
 唯一要注意的就是將安裝類型選擇第一個，與 Windows 10 一起安裝（Grub 開機選單）
 ![img](https://dr.sudo.host/RPrGPH+)

 ## 開機
 呼呼 終於裝好了  
 幹 為什麼開機直接進 Windows 10？  
 ~~沒錯這也是微軟的商業陰謀~~，先不要急著再重開這邊需要做一點設定，讓開機選單更改為 `Grub2` 就可以了。  
 工作管理員開啟 命令題字元貼上  
 `bcdedit /set {bootmgr} path \EFI\你的 Linux 發行版本\grubx64.efi`
 然而這個步驟很重要，弄錯ㄌ你就打不開ㄌ，為了確認請再打開一次 [MiniTool Partition Wizard](https://www.partitionwizard.com)

 理論上在你的開機碟可以找到一個 `100MB` 以及格式為 `FAT32` ㄉ磁碟，對他右鍵 `Explore`  
 ![img](https://dr.sudo.host/XkqBXe+)  
 按照圖就能正確地填寫位置了。  


 ## 開機崩炸了
 *如果你很不幸的跟我一樣一直踩到雷呢？*  
 **例如不小心寫錯位置，導致無法開機**  
 好的，你需要重建一個正確的 `bcd`  
 你需要另一支裝有 Windows 的安裝程式隨身碟，開機後點擊左下角的  
 `修復您的電腦` -> `進階選項` -> `命令提示字元`  

 輸入 `diskpart` 來進入 `diskpart` 程式  
 輸入 `list disk` 來確認需要重建的硬碟位置理論上就是 `0`  
 輸入 `sel disk 0` 來選定操作硬碟  
 輸入 `list vol` 來確認操作的磁區  
 這邊是重點，目標磁區是上面說的 大小 `100MB` 且格式為 `FAT32` 
 輸入 `sel vol ?` 來選定操作磁區  
 輸入 `assign letter X` 來給予代號  
 `X` 可以是其他未佔用的英文，用 `X` 只是因為聽起來比較中二。  
 退出 `diskpart` 輸入 `exit`  
 這邊做了一大段只是給一個磁區命名，這樣方便後面操作而已，沒錯就只是這樣。  

 刪除舊的有問題的 `EFI` 文件  
 `rd /s /q "X:\EFI\"`  

 重建 `bcd`  
 `bcdboot "C:\Windows" /l zh-tw /s X: /f UEFI`  

 戳一下  
 `bootrec /fixboot`
 恭喜你應該修好了。

 ## 結
 幹 我為了弄好這個花了兩天。

 ## ref
  - [解決 UEFI 無法開機的慘況](https://s.sudo.host/2yiqdRX)
  - [Win10 and Ubuntu 雙系統安裝筆記](https://s.sudo.host/2yep6mr)
  - Font rendering looks ugly on Linux · Issue #35675 · microsoft/vscode https://s.sudo.host/2yepKAn