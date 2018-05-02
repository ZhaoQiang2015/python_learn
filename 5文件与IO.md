# 文件与IO
##1. 读写文件数据
- 使用带有`rt`模式的`open()`函数读取文本文件。
- 使用带有`wt`模式的`open()`函数写入一个文本文件。
- 使用带有`at`模式的`open()`函数追加模式
- `sys.getdefaultencoding()`函数：获取系统默认编码格式。
- 传递一个可选的`encoding`参数给`open()`函数，如下：
```python
with open('somefile.txt', 'rt', encoding='utf-8') as f:
    ...
```
- 使用`with`控制块打开文件，在`with`块结束时，文件会自动关闭。
##2. `print()`函数输出重定向到文件中
- 在`print()`函数中指定`file`关键字参数，like this:
```python
with open('somefile.txt', 'wt') as f:
    print('hello python, file=f)
```
- **注意：文件必须以文本模式打开，如果是二进制模式，打印就会出错。**
##3. 使用其它分隔符或行终止符打印
- 可以在`print()`函数中使用`sep`和`end`关键字参数，以想要方式输出。such as:
```python
print('abc', 40, 203)
print('abc', 40, 203, sep=',')
print('abc', 40, 203, sep=',', end='!!\n')
```
- 令`end=' '`可以在输出中禁止换行。
- `str.join()`函数可以完成同样工作，但只适用于字符串。
##4. 读写字节数据
- 使用`rb`或`wb`模式的`open()`函数来读写二进制数据，如图片，声音文件等。
- 读取二进制数据时，返回的都是字节字符串格式的，而不是文本字符串。