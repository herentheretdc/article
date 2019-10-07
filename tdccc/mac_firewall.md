# Mac 防火牆簡易設定

## 序
最近做一些簡單 micorweb service 開發，只是有時候被 mac 內建防火牆弄的很煩，剛好有些 app 不是安裝性質的...  
乾脆直接手動戳指令，順便筆記一下。

## 正題
mac 內建的防火牆位置  
`/usr/libexec/ApplicationFirewall/socketfilterfw`  
  
`--add` 新增到列表  
`--unblockapp` 允許連入  
`--listapps` 列出防火牆 app 清單  
  
## 結論  
好耶。