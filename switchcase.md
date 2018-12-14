# Python如何達成Switch Case？

大概幾個月前有朋友問我這樣的問題，當時覺得用```if..else```就可以了啊為什麼要這麼麻煩，後來因為 ~~強迫症~~ 為了美觀也有類似的問題 ~~（純粹沒事做吧你）~~
順便把想法跟寫法記錄下來
```
#switch case in python way
msg = {
	'uid': '12345',
	'data': {
		'name': 'tdccc'},
	'type': 'type_a'
}
def case1(msg):
		print(msg['data']['name'], ' is ', msg['type'])
		#do more func

def case2(msg):
		print(msg['data']['name'], ' is ', msg['type'])
		#do more func
options = {
	'type_a': case1,
	'type_b': case2
}
options[msg['type']](msg)
```

大概就類似這樣吧（？）
大概就是先建立函式，接著把函式創立成dict就搞定了（？）
