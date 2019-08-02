# VSCode & atom 在 Linux 上無法輸入中文

## 序
起初遇到這問題時覺的無所謂，頂多文件改用英文撰寫，直到發現有時候真的有迫切需求會使用到才發現非常需要。

## 探查
先列出環境

```
OS：Ubuntu 19.04
Version：VSCode Insider 1.37.0
Input：iBus + chewing
```

調查了一陣子發現不只我有遇到這種問題，根據說法是 `Snap` 商店上的 `VSCode` 或是 `atom` 都沒有 `fix` 中文輸入法的輸入問題鎖導致的。  

可參考下列文章  
Quick Note on Crostini + Chinese IME  
https://s.sudo.host/2YGSCQm


## Fix
所以解決辦法就是  
**重新安裝**  

先移除 `snap` 的版本  
`sudo snap remove code-insiders`  
`sudo snap remove atom`  

接著安裝官網提供的 `.deb`  
`sudo dpkg -i vscode.deb`  
`sudo dpkg -i atom.deb`

## Ref.
Quick Note on Crostini + Chinese IME  
https://s.sudo.host/2YGSCQm

Chromebook安裝Linux系統，並順利打出繁體中文 (Crostini)
https://s.sudo.host/2YEJL1I

1.2.1 can't input chinese · Issue #7997 · microsoft/vscode
https://s.sudo.host/2YBMGrP