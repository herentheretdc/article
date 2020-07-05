# Hydrogen簡介

  這邊先附上官方教學網址，想看更多的可以去那
  <https://nteract.gitbooks.io/hydrogen/>

  Hydrogen 是一個能讓 Atom 像 Jupyter 那樣操作的套件
  具體來說像是下面這樣
  ![Hydrogen_for_python](https://cloud.githubusercontent.com/assets/13285808/20360886/7e03e524-ac03-11e6-9176-37677f226619.gif)
  上面這個是python的範例，但是 Hydrogen 不止能執行 python，還可以執行 MongoDB、SQL、C、Java9、TypeScript、JavaScript、Matlab...等。

  **只要有對應的語言核心(kernel)就可以**，目前最少有122種核心可以使用
  其[核心列表於此](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)。

# Hydrogen怎麼做到的

如果不知道 jupyter 是什麼的可以先看[這邊](https://jupyter.org/)    

這邊要先來了解原本的 jupyter 架構：    

| 網頁(Html5) | <-> | jupyter | <-> | jupyter_kernel |    
|:----:|:-----:|:-----:|:-----:|:-----:|     
| (呈現給使用者) | <-> | (中轉處理) | [消息傳送協議](https://jupyter-client.readthedocs.io/en/latest/messaging.html) | (語言核心) |    

然後再回來看 hydrogen 所扮演的腳色：

| Atom | <-> | hydrogen | <-> |  jupyter_kernel |
|:----:|:-----:|:-----:|:-----:|:-----:|     
| (呈現給使用者) | <-> | (中轉處理) |  [消息傳送協議](https://jupyter-client.readthedocs.io/en/latest/messaging.html) | (語言核心) |  

在這裡不難發現 hydrogen 做的事跟 jupyter 很像，2個都走[消息傳送協議](https://jupyter-client.readthedocs.io/en/latest/messaging.html)來跟後面的核心溝通，不過差在 jupyter 是呈現在網頁上，而 hydrogen 是呈現在 Atom 上罷了。

# Hydrogen安裝
  請參考[這個網頁](https://www.itread01.com/content/1548909203.html)的 "4.atom外掛安裝"，如果不會裝Atom的也可以順便看著這篇裝，順帶一提，這裡有我推薦的[套件清單](https://github.com/we684123/Atom_packages)可以參考看看。

  由於安裝 Hydrogen、Atom 不是本篇重點，恕不多閒述。

# Hydrogen設定

[官網有很清楚的教學](https://nteract.gitbooks.io/hydrogen/docs/Usage/GettingStarted.html)，基本上看一下就會用了    
可以做到如：
1.側欄輸出
![](https://user-images.githubusercontent.com/13436188/31737963-799d2ad2-b449-11e7-9b4c-78e51851e204.gif)

2.管理執行中的核心
![](https://user-images.githubusercontent.com/13285808/30815792-7b685b8a-a214-11e7-863e-f334f03eef0f.png
  )

#### 還有其他的功能如果想用好 Hydroge 務必到官網一看。


這裡可能有問題的是 **"Atom 的設定視窗怎麼叫出來"**    
![](https://dr.sudo.host/jrefRg+)

  如果是 windows 請在 Atom 上打 `ctrl+shift+p`
  如果是 mac 應該(沒用過)打 `⌘-⇧-P`
  或是你的 keymap 是自訂的話，請找原指令為 `command-palette:toggle` 的即可。

# Hydrogen核心安裝

##### 基本上... 絕大多數的你只要跟著他的markdown說明就可以了
  通常有兩種安裝方式
  1. pip install <kernel_name>
  2. npm install <kernel_name>

  用pip安裝的通常不用擔心找不到核心(kernel)，用npm安裝的則要注意安裝完核心後有沒有在部屬到這台電腦的帳戶使用者上!

##### 以TypeScript為例：
  從[核心列表](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)找到[安裝頁面](https://github.com/nearbydelta/itypescript)後看到安裝方式是
```sh
npm install -g itypescript
```
下完指令後來請記得跟著下
```sh
sudo -H its --ts-install=global
```
部屬到所有使用者帳戶，或是只部屬到這個帳戶
```sh
its --ts-install=local
```
不要跟作者一樣安裝完後不知道要部屬就跑了，然後才在那邊想半天(ﾟ皿ﾟﾒ)
(以往用pip安裝的Hydrogen都會自動找到核心...)


#### 再來還有一種狀況，如 [Ioctave](https://github.com/calysto/octave_kernel)這顆核心
這種核心是需要你先在你的電腦先安裝 octave 程式後才能裝的。
且安裝核心後記得要把 octave **增加到系統的環境變數裡面才能使用**
其增加的方式可[參考這篇](https://stackoverflow.com/questions/34228982/how-can-i-add-octave-in-path-environment-variable-in-windows-8)或者[這篇(win10)](https://superuser.com/questions/949560/how-do-i-set-system-environment-variables-in-windows-10)亦或參考前面的[文章中的 "2. 配置環境變數"](https://www.itread01.com/content/1548909203.html)，只差要改一下路徑。

  ps'如果覺得matlab太貴買不起可以用用看 Otctav，語法一模一樣，就是部分功能沒有。


# 核心裝好後你有兩個選擇
  1. 直接重開Atom，讓 Hydrogen 重新尋找現有的核心
  2. `ctrl+shift+p`後執行 **"Hydrogen: updata kernels"**

這是因為 Hydrogen 為了效能考量，所以不隨時監控是否安裝新核心。

# 核心和語言對不上?
什麼? 我明明程式語言是 matlab(XX) 為什麼一直顯示是 coffeeScript(OO)?
![語言判斷錯亂](https://dr.sudo.host/iTtoBe+)

如上圖的情況是有可能發生的，此時請點右下繳的 "coffeeScript"
![點選](https://dr.sudo.host/mzQwOT+)
會出現支援語言清單，這個時候在點正確的語言就可以了

### ㄜ... 不是，我的語言並沒有出現在清單內耶?

![安裝語言](https://dr.sudo.host/go9q8q+)
請去 setting -> install -> (輸入你的語言，如我是octave) -> 安裝後即可。
在沒有的話你就可以考慮寫packages來幫助大家囉(#


# 上面的東西我都去認過了，為什麼 Hydrogen 跟我說沒找到可用核心QAQ

那麼請到  setting -> Packages -> Hydrogen -> (設定 "Languages mappings")
然後照著JSON格式寫核心語言配置
![設定 "Languages mappings"](https://dr.sudo.host/HN9N10+)

# 核心噴錯怎麼辦QAQ (遠端核心教學)

這個時候通常可以在核心的 Github issue 頁面找找看解決方法。    
如果沒有找到且覺得是環境問題的話，可以考慮用 docker 架架看 **遠端核心**    
通常這種問題較常是在 windows 上發生(大多都是支援 Linux較多)    

**像我就在使用 [tslab](https://github.com/yunabe/tslab) 這個核心發生這樣的問題。**    


具體方式就像 [Atom_Hydrogen_remote_kernels_by_docker](https://github.com/we684123/Atom_Hydrogen_remote_kernels_by_docker) 這篇示範一樣，在 dockerfile 中，只要將核心的安裝方法補上去，並在架起來後修改 kernel gateways 並連進去即可。    

![kernel gateways](http://dr.sudo.host/dijyvI+)    
![tslab 成功](http://dr.sudo.host/oVRSPu+)    
----

# 本篇結束
以上通通都是辛酸血淚史Orz(乾
