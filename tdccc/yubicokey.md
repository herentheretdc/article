# Yubico Key

# 序
~~其實這篇我拖了好久了~~  
事情是這樣的。
暑假人在公司實習的時候，意外在Google Accounts檢查安全性的時候，又看到了寫著安全金鑰的東西。
其實之前一直很想買，但看了看[Yubico](https://yubico.com/store/)的價格其實蠻高的...
所幸有個朋友願意跟我跳坑，因此就得到了呢~

# 玩
![img](https://dr.sudo.host/grxqxF+)
入手的規格是 Yubico 4 NFC * 2 以及 Yubico * 1  
開始幫他脫衣服(?)>\

|![img](https://dr.sudo.host/t6Sh4B+)|![img](https://dr.sudo.host/a4ONuN+)|
|-------------|-------------|


很顯然的，這看起來十分的堅固呢。
依照官方所敘述的，yubikey有防水防撞擊功能（然而我並沒有實際實驗過）。  
## NFC
首先來玩玩看NFC的版本，將yubikey放置在手機NFC讀取器就會自動跳出網頁，提示這是一個yubikey，接著就能下載App把玩。
他的App其實就只是將OTP放入yubikey中，要使用時把yubikey放在手機背後就會自動彈跳出來  
~~看來很不實用呢，我都用Authy~~

## U2F
接著把他加入支援U2F的帳號中吧，例如 Google、[Gayhub](https://github.com)...
其餘網站支不支援可以上 dongleauth.info 查詢。
順帶一提該網站資料感覺有點落後，vultr的帳號其實也支援U2F，然而他並沒有列出來呢...!!!  
![img](https://dr.sudo.host/JjFHWA+)
![img](https://dr.sudo.host/JawF2A+)

有一點要注意的是，目前是Chrome支援度最高，其他的瀏覽器我並不能保證，所以還是手機常備TOTP App比較好喔。

