# Plurk API踩雷碎碎念

# 序
原本想說把以前寫過的plurk api的東西拿出來把玩看看，結果試了半天都沒法正常使用，還以為自己太久沒有摸oauth1整個忘記了，腦波弱了下去複製官方頁面底下的範例逐漸發覺越來越母湯，於是有了這篇。

# 所以我說那個官方的東西呢
對，官方API底下提供幾個範例跟`libs`很顯然的當然先複製貼上RUN一次...
![img](https://dr.sudo.host/Zcb95A+)
看起來是`json`套件loads的時候噴了，看一下Gayhub上的最後commit日期
![img](https://dr.sudo.host/lri4u3+)
好像還是今年(2019)的1月的事，追著trackback指示，在 `plurk_oauth/oauth.py`的`L83`前加入一個`print()`
![img](https://dr.sudo.host/d3Jw5Z+)
看到這裡
![img](https://dr.sudo.host/odKmiW+)

**我呆滯了一下**
讀了下code將`r.json()`替換成`r.text`
![img](https://dr.sudo.host/Weo31K+)
哦哦 他動了！！！
 喔 幹。 ~~這很攻城屍日常~~
泡了個咖啡想了下，東西有問題的話...我乾脆自己寫一個好了。
恩 然後我就懶了。
[Gayhub](https://github.com/tasi788/plurkapi)
之後的那些東西以後再說吧。


