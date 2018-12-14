# Yubico key - GPG

這邊可能一般人用不太到，覺得用不到的自己跳過  
~~一般人也用不到yubikey~~  
簡而言之就是將 gpg 寫進 yubikey 裡面。

## 序
先來個我自己的QA  

    Q: 長度最長為多少？  
    A: NFC(2048), Neo(4096)  
    Q: 可以一個 GPG 寫在兩隻不同yubikey嗎？  
    Q: 不行。


## 始
好ㄌ 以下純文字，我也不想截圖，基本上就是把官方的內容搬過來，加上自己踩雷的註記。  
按照流程是這樣  
生成一把key在電腦上 > 新增驗證鑰匙 > 新增簽名鑰匙 > 寫入yubikey

首先電腦先安裝以下東西
 - Windows: [GPG4Win](https://www.gpg4win.org/download.html)
 - macOS: [GPG Tools](https://gpgtools.org/gpgsuite.html)

 在下載過程中需要先知道以下事情 [yubico info](https://developers.yubico.com/yubico-piv-tool/YubiKey_PIV_introduction.html):  
 - 預設Pin碼: `123456`
 - 預設Puk碼: `12345678`

以下開始照抄官網資料🌚  
 ### 生成鑰匙  

 1. `gpg --expert --full-gen-key`  
    在你的terminal輸入下面這串

 2. 選擇你的加密方法(預設是RSA啦)，有關RSA的不信任新聞請各位斟酌服用。  
  
 3. 選擇金鑰長度，NFC版似乎是只支援2048吧，其他4帶版本請服用 4096 (其實2048也夠長了)

 4. 選擇金鑰過期時間，這方面自己服用Google。

 5. 輸入名稱。

 6. 輸入 Email。

 7. 註解一些東西，可留空。

 8. 沒問題的話輸入O，輸入密文就能開始產生密鑰，這時候建議隨意移動滑鼠，鍵盤隨便輸入些東西確保產出的東西夠隨機。

 9. `quit`  
    這邊如果沒這麼做，下面出錯就要重新做一次操作，建議先退出保存一次。

 ### 生成驗證用鑰匙
 1. `gpg --expert --edit-key 1234ABC`  
    `1234ABC`是你的key ID, 其實也可以輸入先前步驟的email, 但如果你有多個key 請輸入 key ID。  
 2. `addkey`  
 3. 選擇加密方法(RSA) 8  
 4. 選擇 `A` (authentication key) 接著輸入 `Q` 離開  
 5. 輸入金鑰長度 
 6. 輸入金鑰過期時間
 7. 輸入 `Y` 確定產生 authentication key 接著輸入密文完成。

 ### 生成簽名用鑰匙
 步驟與上面1~3一樣
 1. `gpg --expert --edit-key 1234ABC`  
    `1234ABC`是你的key ID, 其實也可以輸入先前步驟的email, 但如果你有多個key 請輸入 key ID。  
 2. `addkey`  
 3. 選擇加密方法(RSA) 8  
 4. 選擇 `S` (signing key) 接著輸入 `Q` 離開  
 5. 輸入金鑰長度 
 6. 輸入金鑰過期時間
 7. 輸入 `Y` 確定產生 signing key 接著輸入密文完成。
 8. `quit`  
    退出儲存。

### 寫入至Yubikey
 !!! 先插入你的yubikey到電腦上 !!!
 1. `gpg --edit-key 1234ABC`  
    `1234ABC`是你的key ID, 其實也可以輸入先前步驟的email, 但如果你有多個key 請輸入 key ID。  
 2. `keytocard`  
 3. 是否移動主鑰過去 `Y`  
 4. 選則要放哪(key的哪個部位) `1`  
 5. `key 1`  
 6. `keytocard`  
 7. 選則要放哪(key的哪個部位) `2`
 8. `key 1`  
 9. `key 2`  
 10. `keytocard`  
 11. 選則要放哪(key的哪個部位) `3`
 12. `quit` 
     退出保存。
     
就是差不多這樣子完成啦。  

--- 

### 幹我忘記pin碼被鎖了。  
如果pin碼忘記其實可以自己 `reset`  
 1. `gpg --card-edit`  
 2. `passwd`  
 3. `admin`  
    ```
    1 - change PIN
    2 - unblock PIN
    3 - change Admin PIN
    4 - set the Reset Code
    Q - quit
    ```  
 4. `2`  
 5. 提示輸入 `Admin PIN` 其實就是 Puk 碼。  
 6. `Q`重設完成。


## Try Try See?
 > `echo "test" | gpg --clearsign`  

 ## git
 先設定使用的鑰匙以及預設簽名  
 `git config --global user.signingkey 1234ABC`  
 `git config --global commit.gpgsign true`  
 如果有用 remote 倉庫，例如gayhub則需要先去新增pub過去。  
 `gpg --armor --export 1234ABC`  
 並且需要把pub key 給上傳到公開server~  
 ![img](https://dr.sudo.host/x1GYlB+)

 
# 結語

其實就是有個人白目亂玩，結果不小心弄懂了。

# Ref.
[Yubico PIV Tool](https://developers.yubico.com/yubico-piv-tool/YubiKey_PIV_introduction.html)  
[PIV Reset](https://support.yubico.com/support/solutions/articles/15000008587-resetting-the-smart-card-piv-applet-on-your-yubikey)  
[GPG Reset](https://support.yubico.com/support/solutions/articles/15000006421-resetting-the-openpgp-applet-on-your-yubikey)  
[YubiKey with OpenPGP](https://support.yubico.com/support/solutions/articles/15000006420-using-your-yubikey-with-openpgp#Generating_the_Key_on_Your_Local_System_(Recommended)8kpyj)  
[handbook](https://github.com/ruimarinho/yubikey-handbook/blob/master/openpgp/troubleshooting/gpg-failed-to-sign-the-data.md)  
[one key two card](https://security.stackexchange.com/questions/165286/how-to-use-multiple-smart-cards-with-gnupg)
[install to second card](https://lists.gnupg.org/pipermail/gnupg-users/2016-July/056353.html)