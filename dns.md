#[觀念更新]關於CloudFlare宣布啟用1.1.1.1
上禮拜的新聞現在才寫文章有點搞笑呢xD，不清楚的人可以到這裡看看[what is 1.1.1.1?](https://www.cloudflare.com/learning/dns/what-is-1.1.1.1/)

自從上次IBM Quad 9.9.9.9也加入Public DNS戰局之後，沒想到連CloudFlare也加入了，由於CloudFlare是一間很有名的CDN廠商，所以此舉非常引人注目呢~
接著在其他板上開始討論關於1.1.1.1的速度如何啊，跟其他Public DNS比起來又怎樣的不斷冒出，但是
### BUT
我居然看到有人這樣測試
```
[16:07:26] TSAI:bin $ ping -c 4 1.1.1.1
PING 1.1.1.1 (1.1.1.1): 56 data bytes
64 bytes from 1.1.1.1: icmp_seq=0 ttl=53 time=11.874 ms
64 bytes from 1.1.1.1: icmp_seq=1 ttl=53 time=5.873 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=53 time=9.132 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=53 time=10.985 ms

--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 5.873/9.466/11.874/2.298 ms
```
這看起來真的是有夠~~母湯~~的，這樣做其實只對了"一半"，~~怎麼說呢詳細請自己上wiki查DNS運作原理~~

以下是一張取自Wiki的DNS運作原理圖
![dns](https://upload.wikimedia.org/wikipedia/commons/7/7e/Dns-rev-1.gif)
文字敘述的話大概是這樣子：
使用者電腦 -> DNS Server：吶吶  ~~Okotta?~~ 你知道 www.google.com 的IP位址多少咩？
DNS Server A ->  使用者電腦：我資料庫找不到捏，我問問其他人->找DNS Server B： ~~Okotta?~~ 你知道 www.google.com 的IP位址多少咩？
DNS Server B -> DNS Server A：我知道喔是"172.217.24.14"
DNS Server A -> 使用者電腦：告訴妳喔是"172.217.24.14"喲~
使用者電腦 -> "172.217.24.14"

---

那如果是上面剛剛那種用```ping```的方式呢？

使用者電腦 -> 1.1.1.1：Hi!
1.1.1.1 -> 使用者電腦：Hi!

這樣會準嗎![crazy](http://dr.sudo.host/lm9645+)


那要怎麼做才正確？
本著佛系的精神，不管怎樣先上[Gayhub](www.github.com)找一下肯定會有的，剛好找到了一份Source Code並且我加上了台灣Hinet的DNS大家來測試一下吧~
[dnsperftest](https://github.com/tasi788/dnsperftest)

##Result
```
               test1   test2   test3   test4   test5   test6   test7   test8   test9   test10  Average
cloudflare     57 ms   49 ms   41 ms   41 ms   39 ms   41 ms   44 ms   39 ms   37 ms   38 ms     42.60
cloudflare2nd  43 ms   41 ms   43 ms   36 ms   35 ms   35 ms   34 ms   38 ms   37 ms   37 ms     37.90
google         37 ms   39 ms   38 ms   7 ms    53 ms   47 ms   45 ms   41 ms   36 ms   37 ms     38.00
google2nd      41 ms   37 ms   40 ms   42 ms   43 ms   49 ms   38 ms   36 ms   38 ms   34 ms     39.80
quad9          118 ms  118 ms  106 ms  119 ms  119 ms  113 ms  108 ms  115 ms  114 ms  121 ms    115.10
opendns        127 ms  87 ms   98 ms   101 ms  99 ms   316 ms  94 ms   259 ms  87 ms   87 ms     135.50
norton         57 ms   59 ms   58 ms   53 ms   52 ms   59 ms   55 ms   49 ms   58 ms   53 ms     55.30
cleanbrowsing  59 ms   58 ms   59 ms   55 ms   55 ms   55 ms   59 ms   58 ms   55 ms   52 ms     56.50
yandex         318 ms  357 ms  306 ms  335 ms  324 ms  469 ms  324 ms  322 ms  306 ms  370 ms    343.10
adguard        69 ms   69 ms   67 ms   65 ms   74 ms   65 ms   65 ms   65 ms   65 ms   70 ms     67.40
neustar        52 ms   51 ms   58 ms   59 ms   59 ms   51 ms   60 ms   57 ms   59 ms   59 ms     56.50
comodo         211 ms  1106 ms 214 ms  214 ms  214 ms  212 ms  213 ms  213 ms  215 ms  214 ms    302.60
hinet          39 ms   43 ms   40 ms   38 ms   50 ms   39 ms   37 ms   40 ms   38 ms   42 ms     40.60
```
台灣還是Hinet可能比較快一點，但是Google, CloudFlare可能比較安全呦（？）
[source](https://medium.com/@nykolas.z/dns-resolvers-performance-compared-cloudflare-x-google-x-quad9-x-opendns-149e803734e5)
![dnss](https://cdn-images-1.medium.com/max/800/1*3IJ5rPalqhkrW4SbbqLmYQ.png)
