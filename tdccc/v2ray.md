# v2ray 簡單安裝

# 序
近期朋友說他家人近日要前往某國，因此有翻牆需求，剛好主管也有相關困擾，就剛好來研究一下。
至於什麼事 v2ray 就請大家先 Google 下吧。

# 前期
這邊使用 docker 安裝大法，所以請先安裝 docker。
在 terminal 貼上 
```bash
$ sh -c "$(wget https://get.docker.com -O -)"
```

接著檢查下是不是正確安裝好了 
```bash
$ docker -v
Docker version 18.09.2, build 6247962
```

出現這樣的畫面，就是安裝完成惹。  
建議順便做一下這個[操作](https://docs.docker.com/install/linux/linux-postinstall/)

# 安裝
先來講解一下 `server.json` ，裡面有些東西是需要更改的  
L8 的 port，可改為其他的數字  
L12 的 UUID，請上 https://www.uuidgenerator.net/ 內產生新的 UUID 並且記下來。
![img](https://file.sudo.host/5ee66331a0de/Image%2525202019-05-31%252520at%25252011.56.32%252520AM.png)

接著使用 `docker-compose` 安裝 `v2ray`
```bash
$ docker run --rm \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v "$PWD:$PWD" \
    -w="$PWD" \
    docker/compose:1.24.0 up -d
```

最後看到以下訊息就表示啟動成功了。
```
Starting v2ray ...
Starting v2ray ... done
```

# 使用

- macOS  
    [V2rayU](https://github.com/yanue/V2rayU)  
    [V2rayX](https://github.com/Cenmrev/V2RayX)  

- Windows  
    [V2rayW](https://github.com/Cenmrev/V2RayW)  
    [V2RayS](https://github.com/Shinlor/V2RayS)

~~有人能告訴我為什麼都是以單一英文字母當作結尾嗎~~

這邊使用 mac 的 v2rayU 當作操作示範，因為我沒有 Windows 電腦啊。  
啟動後在上方的快捷欄就會看到新的 icon ，點擊 Configure  
![img](https://file.sudo.host/fd96e75acb0c/Image%2525202019-06-03%252520at%2525208.41.56%252520AM.png)

接著按照步驟點擊，將資料依序填入
![img](https://dr.sudo.host/FEndnQ+)

格子3 裡的 id 以及 alertId, level 都必須和 Server 端設定一樣
如果不一樣連不上去十分的正常呢（茶


連上後的檢查下 IP 與 Server 端相同就是成功了
![img](https://dr.sudo.host/5yhThP+)


# 結語
> 實際使用[快樂表](https://speedtest.net)測速一下
> ![img](https://dr.sudo.host/k8d8kd+)

部署有點方便過頭了，有點不適應，此外 v2ray 還支援架設 MTProto 感覺有空可以順便玩一玩。