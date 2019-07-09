# 解決 Auto beautiful autopep8 SyntaxError: Non-UTF-8 code starting with '\xb9' in file

恩... 總之呢...

如果你用 auto beautiful 時出現類似這樣的錯誤
![SyntaxError: Non-UTF-8 code starting with '\xb9'](http://dr.sudo.host/m1Kj6A+)


只需要去他回報錯誤檔案的位置打開檔案(如下圖藍色選取區域)
(我是用nodepad++，其他的也行)
![藍色選取區域](http://dr.sudo.host/rCEEp0+)

然後把第一行(路徑)整個砍掉。 (此時右下可以知道此文件是ANSI格式)
![檔案畫面](http://dr.sudo.host/z7MKUG+)

並且 "編碼" -> "轉換成 UTF-8 碼"
![轉UTF-8](http://dr.sudo.host/q8ApEn+)

變成這樣後(右下也變UTF-8)，再 "儲存" 就好了。
![完成圖](http://dr.sudo.host/TWbBAj+)
