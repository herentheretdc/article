# XtraFinder 0.28 更新問題

# 序

自從我用Mac之後都是使用XtraFinder替代原本的Finder，而XtraFinder有多好用不用我贅述，網路上各種文章滿天飛。
而今天的重點就是標題所說，XtraFinder更新到0.28版所發生的問題。

# 問題

當下我急著修好它忘記截圖...
問題再現失敗( ･᷄ὢ･᷅ )
安裝好之後有個彈跳窗，內容如下
```
XtraFinder was not installed properly

Could not find file/Librar/Scripting additions/XtraFinder.osax

Please check to see if you have permission to write to directory/Library/ScriptingAdditions. Then reinstall XtraFinder
```

![汪汪](http://file.sudo.host/r4p0/Image%202018-04-22%20at%203.37.54%20PM.png)[原圖](https://i.imgur.com/oNOqcBd.png)
Hmmm 當下黑人問號，畢竟第一次噴這錯誤。

```
TSAI:Desktop $ ls /Librar/Scripting\ additions/
```
看了下沒有沒為`XtraFinder.osax`的檔案的說...
翻了一下安裝包裡面的Extra <del>為什麼資料夾不乾脆也叫Xtra</del>，發現裡面正好有需要的檔案不過需要重新命名一下
`sudo mv XtraFinderInjector.osax /Librar/Scripting\ additions/XtraFinder.osax`

收工～

# 結論
要期中考了啊啊啊啊啊啊啊啊啊啊。
