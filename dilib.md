# Mac下安裝dlib
# 序
最近剛好用到[tensorflow](https://www.tensorflow.org/)又剛好需要用到dlib，一開始有些碰壁順便紀錄下解決過程。

# 準備
Mac下需要X11的執行環境所以先下載[XQuartz](https://www.xquartz.org/)並安裝

安裝後如果直接安裝dlib依舊會出錯
`pip install dlib`

原因是需要安裝其他依賴包，Mac我使用[brew](https://brew.sh)
關於brew的安裝方式也十分簡單，將以下這行貼在Terminal就可以了

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

完成之後只需要透過brew就能安裝以下
 - boost
 - boost-python
 - cmake

不過`boost-python`有三個版本
```
[18:42:18] TSAI:Desktop $ brew search boost-python
==> Searching local taps...
boost-python ✔                               boost-python3                                boost-python@1.59
==> Searching taps on GitHub...
==> Searching blacklisted, migrated and deleted formulae...
```

這邊指安裝第一個版本就好
`brew install boost boost-python cmake`

# dlib
接著就是重頭戲啦，安裝dlib，不過dlib也有依賴其他套件，不過`pip`會自己一並安裝才對，沒有安裝的話自行手動

安裝依賴包
`pip install numpy scipy scikit-image`

接著
`pip install dlib`

驗證安裝有沒有成功唄~
`python -c "import dlib"`
沒有顯示任何東西的話代表安裝成功囉(thumbup)
