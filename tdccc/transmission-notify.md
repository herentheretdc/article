# 改造Transmission

# 序
一直以來肥宅我自己是個重度PT使用者，~~也因為如此經常有一堆奇怪的資源~~
~~雖然好用的client不存在~~，但是普遍被大家推薦的有幾個，自己十分推薦[ruTorrent](https://github.com/Novik/ruTorrent) + [flood](https://github.com/jfurrow/flood)、[transmission](https://transmissionbt.com/)
其中[transmission](https://transmissionbt.com/)是個非常有名的跨平台BT下載軟體，幾乎在所有平台都看得到的身影。
 > Transmission是一種BitTorrent用戶端，特點是一個跨平台的後端和其上的簡潔的使用者介面。Transmission以MIT授權條款和GNU通用公眾授權條款雙授權條款授權，因此是一款自由軟體。 - [wiki](https://zh.wikipedia.org/wiki/Transmission)

然而Transmission雖然輕量速度快，卻有個致命的缺點，**他並不支援RSS下載啊！！！！**
震驚之後我才想到ruTorrent都有plugin可以自己寫插件進行擴充了，我在震驚什麼
第三次的震驚來了。

#### transmission沒有像其他client一樣支援plugin擴充啊啊啊啊啊

---
# Geek Time (仮)
不過transmission是有rpc的，所以做起來應該不難呢
列舉了一下自己希望達成的目的有哪些，大概是以下這幾樣

 - RSS下載
 - 下載/新增 通知
 - 上傳到Google Drive

	## RSS下載

	雖然說是Geek Time，但沒有明文規定不能使用現成的Code啊(?)，於是乎上了Google找了一下有沒有比較輕巧簡便的方法能夠實現RSS下載的，
	~~東挑細選~~最後選擇了[transmission-rss](https://github.com/nning/transmission-rss)，用ruby寫的小script，看了看安裝步驟其實也蠻簡單的，先確認電腦上有無安裝ruby
	```shell
	→ ruby -v
	ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
	```
	如果沒有的話請自己`sudo apt-get install ruby`

	接下來就簡單了，只需要利用gem安裝即可
	`gem install transmission-rss`
	等他跑完就完成惹，依照readme說明設定檔位置在`/etc/transmission-rss.conf`
	```shell
	curl -o /etc/transmission-rss.conf https://raw.githubusercontent.com/nning/transmission-rss/master/transmission-rss.conf.example
	sudo vim /etc/transmission-rss.conf
	```
  
