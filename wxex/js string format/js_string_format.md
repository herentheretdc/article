# js string format 實現

首先真的感謝原作者做出來 "js string format"
這讓我在寫程式上方便了不少
但遺憾的是，原作者寫得有點問題(詳情見下)，故我在此改良一下


先附上[原作者的blog](https://kevintsengtw.blogspot.com/2011/09/javascript-stringformat.html?showComment=1536387871696#c7569907085658128584)

---
# 先給改良版本code

<pre><code>

//喔乾，感謝 Kevin Tseng 開源這個用法
//來源:
// https://kevintsengtw.blogspot.com/2011/09/javascript-stringformat.html?
// showComment=1536387871696#c7569907085658128584
//可在Javascript中使用如同C#中的string.format (對jQuery String的擴充方法)
//使用方式 : var fullName = 'Hello. My name is {0} {1}.'.format('FirstName', 'LastName');
//
String.prototype.format = function() {
  var txt = this.toString();
  for (var i = 0; i < arguments.length; i++) {
    var exp = getStringFormatPlaceHolderRegEx(i);
    arguments[i] = arguments[i].replace(/\$/gm,'♒☯◈∭')
    txt = txt.replace(exp, (arguments[i] == null ? "" : arguments[i]));
    txt = txt.replace(/♒☯◈∭/gm,'$')
  }
  return cleanStringFormatResult(txt);
}
//讓輸入的字串可以包含{}
function getStringFormatPlaceHolderRegEx(placeHolderIndex) {
  return new RegExp('({)?\\{' + placeHolderIndex + '\\}(?!})', 'gm')
}
//當format格式有多餘的position時，就不會將多餘的position輸出
//ex:
// var fullName = 'Hello. My name is {0} {1} {2}.'.format('firstName', 'lastName');
// 輸出的 fullName 為 'firstName lastName', 而不會是 'firstName lastName {2}'
function cleanStringFormatResult(txt) {
  if (txt == null) return "";
  return txt.replace(getStringFormatPlaceHolderRegEx("\\d+"), "");
}

</code></pre>
---
# 原作的 format 無法處理 "$" 號

如果你要處理的字串如下(包含$號)就會出錯
![c](https://dr.sudo.host/fAIbN8+)

原本預期應該是 "name:方案 $15 元"

---

### 先說明 js 的 replace 有2種取代模式

#### string.replace(regexp/string,replacement)

**1. 字串取代模式**
格式：string.replace(string,replacement)

這一種相信各位都很熟悉
![https://dr.sudo.host/AVMLQw+](https://dr.sudo.host/AVMLQw+)

\---------------------------------------------------------

**2. 正則取代模式**
格式：string.replace(regexp,replacement)

用 **正則表達式(regexp)** 去搜尋取代。 [沒概念的推你看個影片](https://www.youtube.com/watch?v=rCd8zdnWMgk)
![](https://dr.sudo.host/xlbHeg+)

----


**正則取代模式** 跟 **字串取代模式** 的差別就在
正則取代模式可以 **一次取代多個**"欲替換字串"

像是這樣的字串第一種要多做幾次，而用正則的方式則可一次搞定。
![](https://dr.sudo.host/wpJMbr+)


# "正則取代模式"有個雷點，"$"號
### 其實這是 feature 造成的 bug (無奈臉
來看 code
順便附上正則的結果圖

![](https://dr.sudo.host/Jcz7kL+)
![](https://dr.sudo.host/LTYazB+)

如上圖可已發現我的正則是匹配到在 "兩個\*號" 到 "兩個\*號" 之間的文字
\**(這裡面是我要的)**

然後 txt.replace(retxt, '粗體字>> \$1 << 粗體字') 中的 $1 變成了 "()"中匹配到的文字

#### 這代表著網路上提供的 js replace 格式有漏掉Orz...

### X:　~~string.replace(regexp / string, replacement)~~
### O:　string.replace(regexp / string, replacement + extract)

![](https://dr.sudo.host/QbPyaB+)

---

對了! $1 $2 $3 的判定依此規律
誰的 "(" 先出來誰當第一
![](https://dr.sudo.host/8PZ5Vf+)

ps'這個可以 \$1 ~ \$99
更多 regexp $ 號用法可去
http://www.w3school.com.cn/jsref/jsref_replace.asp

----
也因此，原作中遇到 $ 號後就出bug了    

而我的做法就是是先把 $ 號替換掉，之後再替換回來    

**而我的作法也是有bug的，那就是源字串中不能有 "♒☯◈∭"**
但碰上的機率應該很小吧(?
能碰上他也該去買樂透了~~~~
