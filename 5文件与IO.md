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
##5. 文件不存在才能写入
- 在`open()`函数中使用`x`模式代替`w`模式的方法来解决这个问题。like this:
```python
with open('soflefile', 'xt') as f:
    f.write('hello\n')
```
- `x`文件模式仅限于python3中。
##6. 字符串的I/O操作
- 使用`io.StringIO()`和`io.BytesIO()`类来创建类文件对象操作字符串数据。
```python
s = io.StringIO()
s.write('hello world\n')
s.getvalue()
s.read(4)
```
- 可以用于模拟一个普通文件，用于单元测试中。
##7. 读写压缩文件
- 使用`gzip`和`bz2`模块来读取gzip或bz2格式的压缩文件。如这样：
```python
import gzip
with gzip.open('somefile.gz', 'rt') as f:
    text = f.read()

import bz2
with bz2.open('somefile.bz2', 'rt') as f:
    text = f.read()
```
- `gzip.open()`和`bz2.open()`接受跟内置`open()`函数一样的参数，包括`encoding`, `errors`, `newline`等。当写入压缩数据时，可以用`compresslevel`关键字指定压缩等级，**默认为9级，也是最高等级**
- 它们还可以作用在一个已经存在并以二进制模式打开的文件上，如下：
```python
import gzip
f = open('somefile.gz', 'rb')
with gzip.open(f, 'rt') as g:
    text = g.read()
```
##8. 固定大小记录的文件迭代
- 使用`iter`和`functools.partial()`函数：
```python
from functools import partial

RECORD_SIZE = 32
with open('somefile', 'rb') as f:
    records = iter(partial(f.read, RECORD_SIZE), b'')
    for r in records:
        ...
```
- `iter()`函数如果给它传递一个可调用对象和一个标记值，它会创建一个迭代器。
##9. 读取二进制数据到可变缓冲区
- xxxxxx
- xxxxxx
##10. 内存映射的二进制文件
- ××××××
- ××××××
##11. 文件路径名的操作
- 使用`os.path`模块中的函数来操作路径名。
- `os.path.basename()`: get the last component of the path
- `os.path.dirname()`: get the directory name
- `os.path.join()`: join path components together
- `os.path.splitext(): split the file extension
- ××××××× any more
##12. 测试文件或目录是否存在
- 使用`os.path.exists()`
- 进一步，测试这个文件什么类型
- `os.path.isfile()`: is a regular file
- `os.path.isdir()`: is a directory
- `os.path.islink()`: is a symbolic link
- `os.path.realpath()`: get the file linked to 
- `os.path.getsize()`: 
- `'os.path.gettime()`:
- **使用`os.path`进行文件测试时需要注意文件权限的问题。**
##13. 获取文件夹中的文件列表
- `os.listdir()`: 获取某个目录中的文件列表，包括所有文件，子目录，符号链接等 。可以使用如下的方法：
```python
import os.path

# get all files
names = [name for name in os.listdir('somedir') if os.path.isfile(os.path.join('somedir', name))]

# get all dirs
dirnames = [name for name in os.listdir('somedir') if os.path.isdir(os.path.join('somedir', name))]
```
- `startswith()`和`endswith()`方法对于过滤一个目录的内容也很有用,like this:
```python
pyfiles = [name for name in os.listdir('somedir') if name.endswith('.py')]
```
##14. 忽略文件名编码
- ××××××
##15. 打印不合法的文件名
- ××××××
##16. 与串行端口的数据通信
- 使用`pySerial`包，用法如下：
```python
import serial
ser = serial.Serial('/dev/tty.usbmodem641', # Device name varies
                baudrate=9600,
                bytesize=8,
                parity='N',
                stopbits=1)
```
##17. 创建临时文件和文件夹
- `tempfile`模块可以创建一个匿名的临时文件，如下：
```python
from tempfile import TemporaryFile

with TemporaryFile('w+t') as f:
    f.write('xxx\n')
    f.seek(0)
    data = f.read()
```
- TemporaryFile()第一个参数是文件模式，文本模式用`w+t`,二进制模式用`w+b`。这个模式同时支持读和写。
## 18. 序列化Python对象
- 使用`pickle`模块，将Python对象序列化为一个字节流，便于保存，存储到数据库或是网络传输。用法如：
```python
import pickle

data = ... # some Python object
pickle.dump(data, f)
```
- `pickle.dumps()`: 将一个对象转储为一个字符串。
- `pickle.load()`或`pickle.loads()`，从字节流中恢复一个对象。