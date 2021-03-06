# 1.2.4 字典的魔术方法

在 1.1.4 节中介绍过，通过下标访问最终都会由 `__getitem__` 这个魔术方法处理，因此字典的 `d[key]` 这种写法也不例外， 如果键不存在，则会走到 `__missing__ `方法，再给一次挽救的机会。比如我们可以实现一个字典， 自动忽略键的大小写：

```python
class MyDict(dict):
	def __missing__(self, key):
		if key.islower():
			raise KeyError(key)
		else:
			return self[key.lower()]

d = MyDict({'a': 61})
d['A'] # 返回 61
'A' in d # False
```

这个字典比较简陋，比如 key 可能不是字符串，不过我没有处理太多情况，因为它主要是用来演示 `__missing__` 的用法，如果想要最后一行的 `in` 语法正确工作，需要重写 `__contains__` 这个魔术方法，过程类似，就不赘述了。

虽然通过自定义的函数也能实现相似的效果，不过这个自定义字典对用户更加透明，如果不在文档中说明，调用方很难察觉到字典的内部逻辑被修改了。 Python 有很多强大的功能，可以具备这种内部进行修改，但是对外保持透明的能力。这可能是我们第一次体会到，后续还会不断的经历。