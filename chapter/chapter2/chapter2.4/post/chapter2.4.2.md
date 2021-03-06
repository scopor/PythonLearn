# 2.4.2 装饰器的基本原理

首先，装饰器是个函数，它的参数是被装饰的函数，返回值也是一个函数：

```python
def decorate(origin_func):  # 这个参数是被装饰的函数
	print(1)  # 先输出点东西
	return origin_func  # 把原函数直接返回

@decorate    # 注意这里不是函数调用，所以不用加括号，也不用加被修饰的函数名
def sayHello():
	print('Hello')

sayHello()  # 如果没有装饰器，只会打印 'Hello'，实际结果是打印 1 再打印 'Hello'
```

因此，使用装饰器的这种写法：

```python
@decorate
def foo():
	pass
```

和下面这种写法是完全等价的， 初学者可以把装饰器在心中默默的转换成下一种写法，以方便理解：

```python
def foo():
	pass
foo = decorate(foo)
```

需要注意的是，装饰器函数 `decorate` 在模块被导入时就会执行，而被装饰的函数只在被调用时才会执行，也就是说即使不调用 `sayHello` 函数也会输出 1，但这样就不会输出 Hello 了。

有了装饰器，配合前面介绍的函数对象，函数内省，我们可以做很多有意思的事，至少判断上一节中某个函数是否是策略是非常容易的。在装饰器中，我们还可以把策略函数都保存到数组中， 然后提供一个“推荐最佳策略”的功能， 其实就是遍历执行所有的策略，然后选择最好的结果。
