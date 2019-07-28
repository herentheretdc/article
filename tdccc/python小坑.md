# 序
簡單的筆記下有關於最近遇到的`Python`坑。

## `isdigit()`
這個通常用在`str`字串類型中判別是否為數字，只要`str`為純數字`isdigit()`會返回`True`，然而數字是負數時則會返回`False`  
一開始覺得很有事，事後翻了下官方文件
![img](https://dr.sudo.host/WuNlAb+)
他是依照字串去判斷是不是`數字`，這邊數字的定義是`0-9`，因此可以用下列表示他可能做的事情。
```python
def isdigit(input_str):
    for x in input_str:
        if x not in ['1','2','3','4','5','6','7','8','9','0']:
            return False
        return True
```
大概是上面這種感覺，~~不要跟我戰寫法~~。

## 解法
解法那麼多種，自己想啊。

```python
def isdigit(input_str):
    try:
        int(x)
    except ValueError:
        return False
    else:
        return True
```