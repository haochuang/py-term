# py-term   Python在终端中写一首七彩的诗

Python module to style terminal output, moving and positioning the cursor.

**Python 2 and 3 compatible**

![alt text](pyterm.jpg "See? amazing!")

## Installation

Install through **pip**.

```
$ pip install py-term
```

or get from source

```
$ git clone https://github.com/gravmatt/py-term.git
$ cd py-term
$ python setup.py install
```

## Import module

Import the module into your python project.

```
import term
```

## Usage

```
term.write('Hello, ')
term.write('Python!')

> Hello, Python!

term.writeLine('Hello')
term.writeLine('Python!')

> Hello
> Python!
```

## Style output

The first argument is the text output and all following arguments are for styling.

```
term.writeLine(text, *style)

Or

text = term.format(text, *style)
term.writeLine(text)
```

### Usage

```
term.writeLine('Hello, Python!')

term.writeLine('This text line will be green', term.green)

term.writeLine('Reverse the green color', term.green, term.reverse)
```

Or

```
output = term.format('Hello, ', term.green) + term.format('Python!', term.blue, term.bold)

term.writeLine(output)

term.write(term.format('All in one line', term.reverse))
```

#### Text align

**Center align**

```
# term.center(text)

term.writeLine(term.center('Super Python!'))
```

**Right align**

```
# term.right(text)

term.writeLine(term.right('Rene Tanczos (@gravmatt)'))
```

##### Style attributes

| Code                  | Description                          |
| :-------------------- | :----------------------------------- |
| term.off        | All attributes off                   |
| term.bold       | Bold                                 |
| term.dim        | Dim                                  |
| term.underscore | Underscore (monochrome display only) |
| term.blink      | Blink                                |
| term.reverse    | Reverse                              |
| term.hide       | Hide                                 |

##### Text color

| Code               | Color       |
| :----------------- | :---------- |
| term.black   | Black       |
| term.red     | Red         |
| term.green   | Green       |
| term.yellow  | Yellow      |
| term.blue    | Blue        |
| term.magenta | Magenta     |
| term.cyan    | Cyan        |
| term.white   | White       |

##### Background color

| Code                 | Color       |
| :------------------- | :---------- |
| term.bgblack   | Black       |
| term.bgred     | Red         |
| term.bggreen   | Green       |
| term.bgyellow  | Yellow      |
| term.bgblue    | Blue        |
| term.bgMagenta | Magenta     |
| term.bgcyan    | Cyan        |
| term.bgwhite   | White       |

## Remove style attributes

Removes style characters.

(Good to call before you count a string)
```
term.strip(formatted_text)

hello = term.red + 'hello, world' + term.off
print hello
# '\x1b[31mhello, world\x1b[0m\x1b[27m'

print term.strip(hello)
# hello, world
```

## Highlighting text

Simple highlighting of unformatted text strings
```
def callback(matching_text):
  return term.blue + matching_text + term.off

output, match_count, array_of_positions = term.highlight(regex_pattern, text, callback)
```

Return a tuple.

output (index 0) = formatted text output

match_count (index 1) = match count of the pattern

array_of_positions (index 2) = array of tuples with start and stop points of the matches [(4, 6), (9, 11), ..]

## Set title

```
term.setTitle('Hello Terminal')

# or clear it

term.clearTitle()
```

## Set tab name

```
term.setTab('Hello Tab')

# or clear it

term.clearTab()
```

## Cursor position

Move the cursor to a specific position.
```
term.pos(line, column)

term.pos(2, 15)
```

Get the size of the terminal (lines and columns)

```
(30, 100) = term.getSize()

# (lines, colums) = term.getSize()
```

Move the cursor to the home position (1, 1).

```
term.homePos()
```

Moves the current cursor position up, down, left or right by the specified value.

```
term.up(value=1)
term.down(value=1)
term.left(value=1)
term.right(value=1)
```

Saves the current cursor position.

```
term.saveCursor()
```

Restore the previously stored cursor position.

```
term.restoreCursor()
```

Clear the terminal screen.

```
term.clear()
```

Clear the entire line on the current cursor position.

```
term.clearLine()
```

Clear line from the current cursor position to the end.

```
term.clearLineFromPos()
```

Clear line from begin to current cursor position.

```
term.clearLineToPos()
```

## 说迷宫
peom.py这个脚本每运行一次，就会输出一次《上邪》这首诗。但是每次运行，输出的效果都会变化。每行文字的颜色会变化，样式也会变化。

让Python能够轻易地在终端中写出多彩文字的，就是py-term这个库了。

项目地址

https://github.com/gravmatt/py-term


## 库的安装
```
pip install py-term
```

## 库的使用

在终端中输出不换行的文字
```
term.write('Hello, ')
```

在终端中输出换行的文字

```
term.writeLine('Hello')
```

输出绿色的文字

```
term.writeLine('This text line will be green', term.green)
```

输出绿色并且反色的文字

```
term.writeLine('Reverse the green color', term.green, term.reverse)
```

输出居中的文字

```
term.writeLine(term.center('Super Python!'))
```

还有很多其他的特效，比如高亮、移动光标等，有兴趣的同学可以去围观一下。

最后，奉上peom.py的源代码

peom = '''
上邪！ 
我欲与君相知， 
长命无绝衰！ 
山无陵， 
江水为竭， 
冬雷阵阵， 
夏雨雪， 
天地合， 
乃敢与君绝。
'''

```
import term
import random

for line in peom.split("\n"):
    colors = [term.red, term.green, term.yellow, term.blue]
    mode = [term.bold, term.dim, term.underscore, term.blink, term.reverse]
    term.writeLine(line.strip(), random.choice(colors), random.choice(mode))
```    

## Licence

The MIT License (MIT)

Copyright (c) 2015-2016 René Tanczos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
