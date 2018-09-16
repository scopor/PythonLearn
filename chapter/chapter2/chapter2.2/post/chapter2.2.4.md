# 2.2.4 参数分类

Python 中函数的参数可以分为两大类：

定位参数（Positional）：表示参数的位置是固定的。比如对于函数 `foo(a, b)` 来说，`foo(1, 2)` 和 `foo(2, 1)` 就是截然不同的，a 和 b 的位置是固定的，不可随意调换。
关键词参数（Keyword）：表示参数的位置不重要，但是参数名称很重要。比如 `foo(a = 1, b = 2)` 和 `foo(b = 2, a = 1)` 的含义相同。
有一种参数叫做仅限关键字（Keyword-Only）参数，比如考虑这个函数：

```python
def foo(*args, n=1, **kwargs):
	print(n)
```

这个函数在调用时，如果参数 n 不指定名字，就会被前面的 `*args` 处理掉，如果指定的名字不是 n，又会被后面的 `**kwargs` 处理掉，所以参数 n 必须精确的以 `(n = xxx)` 的形式出现，也就是 Keyworld-Only。