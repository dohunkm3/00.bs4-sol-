- - -

# BeautifulSoup

### A Short Introduction

* * *

**박 진 수** 교수  
Intelligent Data Semantics Lab  
Seoul National University

- - -

<h3>Table of Contents<span class="tocSkip"></span></h3>
<div class="toc"><ul class="toc-item"><li><span><a href="#HTML" data-toc-modified-id="HTML-1">HTML</a></span></li><li><span><a href="#기초" data-toc-modified-id="기초-2">기초</a></span></li><li><span><a href="#속성" data-toc-modified-id="속성-3">속성</a></span></li><li><span><a href="#열람" data-toc-modified-id="열람-4">열람</a></span><ul class="toc-item"><li><span><a href="#contents" data-toc-modified-id="contents-4.1">contents</a></span></li><li><span><a href="#children" data-toc-modified-id="children-4.2">children</a></span></li><li><span><a href="#descendants" data-toc-modified-id="descendants-4.3">descendants</a></span></li></ul></li><li><span><a href="#검색" data-toc-modified-id="검색-5">검색</a></span></li><li><span><a href="#텍스트-처리" data-toc-modified-id="텍스트-처리-6">텍스트 처리</a></span><ul class="toc-item"><li><span><a href="#get_text()" data-toc-modified-id="get_text()-6.1">get_text()</a></span></li><li><span><a href="#get_text(),-strings,-stripped_strings의-단순-비교" data-toc-modified-id="get_text(),-strings,-stripped_strings의-단순-비교-6.2">get_text(), strings, stripped_strings의 단순 비교</a></span></li></ul></li></ul></div>

# HTML

다음 HTML 문서와 동일한 문서를 작성하여 'web_page.html'로 저장한다.


```python
%%writefile data/web_page.html
<!DOCTYPE html>
<html>
<head><title>A Simple Local Web Page</title></head>

<body>
  <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
  <h2>The second heading</h2>
    <p class='simple paragraph' id='para'>Paragraph #1 under <b>the second heading</b>.</p>
    <p class='simple paragraph'>Paragraph #2 under <u>the second heading</u>.</p>
    <div>
      <p class='div first-link' id='link'>This is a link to <a href='http://biz.snu.ac.kr' id='snubiz'>Business School at SNU</a>.</p> 
      <p class='div second-link' id='link'>We also want to visit <a href='https://www.python.org' id='python'>Python Official Web Page</a>.</p> 
    </div>
</body>
</html>
```


```python
%%HTML
<!DOCTYPE html>
<html>
<head><title>A Simple Local Web Page</title></head>

<body>
  <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
  <h2>The second heading</h2>
    <p class='simple paragraph' id='para'>Paragraph #1 under <b>the second heading</b>.</p>
    <p class='simple paragraph'>Paragraph #2 under <u>the second heading</u>.</p>
    <div>
      <p class='div first-link' id='link'>This is a link to <a href='http://biz.snu.ac.kr' id='snubiz'>Business School at SNU</a>.</p> 
      <p class='div second-link' id='link'>We also want to visit <a href='https://www.python.org' id='python'>Python Official Web Page</a>.</p> 
    </div>
</body>
</html>
```


<!DOCTYPE html>
<html>
<head><title>A Simple Local Web Page</title></head>

<body>
  <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
  <h2>The second heading</h2>
    <p class='simple paragraph' id='para'>Paragraph #1 under <b>the second heading</b>.</p>
    <p class='simple paragraph'>Paragraph #2 under <u>the second heading</u>.</p>
    <div>
      <p class='div first-link' id='link'>This is a link to <a href='http://biz.snu.ac.kr' id='snubiz'>Business School at SNU</a>.</p> 
      <p class='div second-link' id='link'>We also want to visit <a href='https://www.python.org' id='python'>Python Official Web Page</a>.</p> 
    </div>
</body>
</html>



# 기초


```python
# 관련 모듈을 설치한다.
!python -m pip install bs4

# 또는
# !pip install bs4
```


```python
from bs4 import BeautifulSoup
```


```python
# BeautifulSoup 클래스를 사용하여 웹 페이지 객체를 생성한다.
# 이 때 파서를 'html.parser'로 설정한다.
page = BeautifulSoup(open('data/web_page.html'), 'html.parser')
# page = BeautifulSoup(open('web_page.html'), 'html.parser')

# 생성한 웹 페이지를 출력한다.
print(page)
```

    <!DOCTYPE html>
    
    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>



```python
# prettify() 메소드를 사용하면 웹 페이지가 태그의 깊이에 따라 들여쓰기가 되어 출력할 수 있다.
print(page.prettify())
```

    <!DOCTYPE html>
    <html>
     <head>
      <title>
       A Simple Local Web Page
      </title>
     </head>
     <body>
      <h1>
       The First Heading
      </h1>
      <p>
       Paragraph under the first heading.
      </p>
      <h2>
       The second heading
      </h2>
      <p class="simple paragraph" id="para">
       Paragraph #1 under
       <b>
        the second heading
       </b>
       .
      </p>
      <p class="simple paragraph">
       Paragraph #2 under
       <u>
        the second heading
       </u>
       .
      </p>
      <div>
       <p class="div first-link" id="link">
        This is a link to
        <a href="http://biz.snu.ac.kr" id="snubiz">
         Business School at SNU
        </a>
        .
       </p>
       <p class="div second-link" id="link">
        We also want to visit
        <a href="https://www.python.org" id="python">
         Python Official Web Page
        </a>
        .
       </p>
      </div>
     </body>
    </html>


# 속성

태그 이름으로 HTML 문서를 탐색할 수 있다.


```python
# 태그 html의 내용을 확인한다.
page.html
```




    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>




```python
# 태그 head의 내용을 확인한다.
page.head
```




    <head><title>A Simple Local Web Page</title></head>




```python
# 태그 title의 내용을 확인한다.
page.title
```




    <title>A Simple Local Web Page</title>




```python
# 태그 body의 내용을 확인한다.
page.body
```




    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>




```python
# (방법 1) 태그 h1의 내용을 확인한다.
page.h1
```




    <h1>The First Heading</h1>




```python
# (방법 2) 태그 h1의 내용을 확인한다.
page.body.h1
```




    <h1>The First Heading</h1>




```python
# (방법 1) 태그 h2의 내용을 확인한다.
page.h2
```




    <h2>The second heading</h2>




```python
# (방법 2) 태그 h2의 내용을 확인한다.
page.body.h2
```




    <h2>The second heading</h2>




```python
# (방법 1) 태그 p의 내용을 확인한다.
page.p  
```




    <p>Paragraph under the first heading.</p>




```python
# (방법 2) 태그 p의 내용을 확인한다.
page.body.p  
```




    <p>Paragraph under the first heading.</p>




```python
# find() 메소드로 태그 p가 있는 문서를 검색한다.
# find the first tag <p> 
page.find('p')  # same as page.p
```




    <p>Paragraph under the first heading.</p>




```python
# 문서에서 모든 태그 p를 검색한다.
# 반환한 객체의 자료형은?
# find all tag <p> 
page.find_all('p') 
```




    [<p>Paragraph under the first heading.</p>,
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>,
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>]




```python
#  url을 포함하는 태그 ???의 내용을 확인한다.
page.a  # same as page.body.a
```




    <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>




```python
# 문서에서 url을 포함하는 태그를 모두 검색한다.
# find all tag <a>
page.find_all('a')
```




    [<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>,
     <a href="https://www.python.org" id="python">Python Official Web Page</a>]




```python
# 태그 a가 포함하고 있는 텍스트 내용을 추출한다.
page.a.string
```




    'Business School at SNU'




```python
# 태그 div의 내용을 확인한다.
page.div  
```




    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>




```python
# string 속성을 사용하여 태그 a가 포함하고 있는 텍스트 내용을 추출한다.
# <div> 내에 다른 태그가 있기 때문에 아무 것도 반환하지 않는다.
page.div.string
```

# 열람

## contents

태그 하위항목(children)
- 태그에는 문자열과 다른 태그가 포함될 수 있으며 이러한 요소를 태그의 하위항목(children)이라고 한다.

**.contents** 
- 태그 내의 내용을 **리스트**로 반환한다.
- 문자열은 **contents**를 사용할 수 없는데 그 이유는 문자열 내에 다른 어떤 것도 담을 수 없기 때문이다.

**.children**
- 태그의 내용을 리스트로 가져오는 것이 아니라 태그의 직접적인 하위항목을 순회하는 제너레이터(generator)다.

**.descendants** 
- 태그의 모든 하위항목을 순차적으로 순회하는 제너레이터(generator)다.

참고
- **contents**와 **children** 속성은 태그의 직접적인 하위항목만을 대상으로 함
- e.g., **< head >** 태그는 **< title >** 태그 하나만 직접적인 하위항목으로 가짐  


```python
page.head
```




    <head><title>A Simple Local Web Page</title></head>




```python
# 태그 head가 담고 있는 내용(contents)을 열람한다.
# 반환하는 객체의 자료형은?
page.head.contents
```




    [<title>A Simple Local Web Page</title>]




```python
# 태그 head가 담고 있는 내용 중 첫 번째 값을 열람한다.
# 반환하는 객체의 자료형은?
page.head.contents[0]
```




    <title>A Simple Local Web Page</title>




```python
page.title # same as page.head.contents[0]
```




    <title>A Simple Local Web Page</title>




```python
# 태그 title이 담고 있는 내용(contents)을 열람한다.
page.title.contents
```




    ['A Simple Local Web Page']




```python
# 태그 title이 담고 있는 내용 중 첫 번째 값을 열람한다.
page.title.contents[0]
```




    'A Simple Local Web Page'




```python
# 태그 title의 첫 번째 값이 담고 있는 내용(contents)을 열람한다.
# 문자열은 contents를 사용할 수 없다. 
# 문자열 내에 다른 어떤 것도 담지 않았기 때문이다.
page.title.contents[0].contents
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-28-c6c1c0627b31> in <module>
          2 # 문자열은 contents를 사용할 수 없다.
          3 # 문자열 내에 다른 어떤 것도 담지 않았기 때문이다.
    ----> 4 page.title.contents[0].contents
    

    ~/Dropbox/_data/venv/3.8ds/lib/python3.8/site-packages/bs4/element.py in __getattr__(self, attr)
        867             return self
        868         else:
    --> 869             raise AttributeError(
        870                 "'%s' object has no attribute '%s'" % (
        871                     self.__class__.__name__, attr))


    AttributeError: 'NavigableString' object has no attribute 'contents'



```python
# 태그 body가 담고 있는 내용(contents)을 열람한다.
# 반환하는 객체의 자료형은?
page.body.contents
```




    ['\n',
     <h1>The First Heading</h1>,
     '\n',
     <p>Paragraph under the first heading.</p>,
     '\n',
     <h2>The second heading</h2>,
     '\n',
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     '\n',
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     '\n',
     <div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>,
     '\n']




```python
# 태그 body가 담고 있는 내용(contents) 중 마지막 두 값을 열람한다.
page.body.contents[-2:]
```




    [<div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>,
     '\n']




```python
# for문을 사용하여 태그 body가 담고 있는 모든 내용(contents)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for content in page.body.contents:
   print(repr(content))
```

    '\n'
    <h1>The First Heading</h1>
    '\n'
    <p>Paragraph under the first heading.</p>
    '\n'
    <h2>The second heading</h2>
    '\n'
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    '\n'
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    '\n'
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    '\n'


## children


```python
# 태그 body가 담고 있는 하위항목(children)을 열람한다.
# 반환하는 객체의 자료형은?
# .children은 태그의 내용을 리스트로 가져오는 것이 아니라 
# 태그의 직접적인 하위 항목을 순회하는 제너레이터(generator)다.
page.body.children
```




    <list_iterator at 0x7fd5396bf1f0>




```python
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
# Instead of getting sub-items as a list, 
# we can iterate over a tag’s children 
# using the .children generator:
for child in page.body.children:
     print(repr(child))
```

    '\n'
    <h1>The First Heading</h1>
    '\n'
    <p>Paragraph under the first heading.</p>
    '\n'
    <h2>The second heading</h2>
    '\n'
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    '\n'
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    '\n'
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    '\n'



```python
# 태그 body가 담고 있는 하위항목(children)을 리스트로 가져온다.
# page.body.contents와 같다. 
list(page.body.children)
```




    ['\n',
     <h1>The First Heading</h1>,
     '\n',
     <p>Paragraph under the first heading.</p>,
     '\n',
     <h2>The second heading</h2>,
     '\n',
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     '\n',
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     '\n',
     <div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>,
     '\n']



## descendants


```python
# 태그 body의 내용을 확인한다.
page.body
```




    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>




```python
# 태그 body가 담고 있는 내용(contents)을 열람한다.
page.body.contents
```




    ['\n',
     <h1>The First Heading</h1>,
     '\n',
     <p>Paragraph under the first heading.</p>,
     '\n',
     <h2>The second heading</h2>,
     '\n',
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     '\n',
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     '\n',
     <div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>,
     '\n']




```python
# --- traversing .children
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for child in page.body.children:
     print(repr(child))
```

    '\n'
    <h1>The First Heading</h1>
    '\n'
    <p>Paragraph under the first heading.</p>
    '\n'
    <h2>The second heading</h2>
    '\n'
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    '\n'
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    '\n'
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    '\n'



```python
# 태그 body가 담고 있는 하위항목(children)과 
# 그 하위항목의 모든 하위항목(descendants)을 열람한다.
# 반환하는 객체의 자료형은?
# .descendants도 .children과 마찬가지로 제너레이터(generator)다.
# .children이 태그의 직접적인 하위 항목을 순회하는 반면
# .descendants는 태그의 모든 하위항목을 순차적으로 순회하는 제너레이터다.
page.body.descendants
```




    <generator object Tag.descendants at 0x7fd5397923c0>




```python
# --- traversing .descendants
# for문을 사용하여 태그 body가 담고 있는 모든 하위항목(children)과 
# 그 하위항목의 모든 하위항목(descendants)을 출력한다.
# 이 때 대표 형식으로 출력하기 위해 repr() 함수를 사용하여 출력한다.
for content in page.body.descendants:
    print(repr(content))
```

    '\n'
    <h1>The First Heading</h1>
    'The First Heading'
    '\n'
    <p>Paragraph under the first heading.</p>
    'Paragraph under the first heading.'
    '\n'
    <h2>The second heading</h2>
    'The second heading'
    '\n'
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    'Paragraph #1 under '
    <b>the second heading</b>
    'the second heading'
    '.'
    '\n'
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    'Paragraph #2 under '
    <u>the second heading</u>
    'the second heading'
    '.'
    '\n'
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    '\n'
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    'This is a link to '
    <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>
    'Business School at SNU'
    '.'
    '\n'
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    'We also want to visit '
    <a href="https://www.python.org" id="python">Python Official Web Page</a>
    'Python Official Web Page'
    '.'
    '\n'
    '\n'


# 검색

아래 두 메소드는 태그를 검색한다. 태그 내 텍스트의 내용은 검색하지 않는다.

[find](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find) 
- **find**(*name, attrs, recursive, string, **kwargs*)

[find_all](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#find-all)
- **find_all**(*name, attrs, recursive, string, limit, **kwargs*)


```python
# 문서에서 첫 번째 나타나는 태그 p를 검색한다.
# 찾는 태그 <p> 중 첫 번째 태그를 반환한다.
page.find('p')
```




    <p>Paragraph under the first heading.</p>




```python
# 문서에서 모든 태그 p를 검색한다.
# 반환한 객체의 자료형은?
# 찾는 태그 <p> 모두를 리스트로 반환한다.
page.find_all('p')
```




    [<p>Paragraph under the first heading.</p>,
     <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>,
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>,
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>]




```python
# 문서에서 찾는 태그 p 중 첫 번째 태그 내용을 확인한다.
# 찾는 태그 <p> 중 첫 번째 태그 내용을 반환한다.
page.find_all('p')[0]  # same as page.find('a')
```




    <p>Paragraph under the first heading.</p>




```python
# (방법 1) 문서에서 찾는 태그 p 중에 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
# class는 파이썬 키워드라 class_로 표현해야 한다.
page.find_all('p', class_='simple paragraph')
```




    [<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]




```python
# (방법 2) 문서에서 찾는 태그 p 중에 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
# 속성은 딕셔너리 형식으로도 표현이 가능하다.
page.find_all('p', {'class': 'simple paragraph'})
```




    [<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]




```python
# (방법 3) 문서에서 찾는 태그 p 중에 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
# 속성이 class면 class는 생략할 수 있다.
page.find_all('p', 'simple paragraph')
```




    [<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]




```python
# 태그 이름 없이 속성 이름만으로도 찾을 수 있다.
# 문서에서 속성 class의 값이 'simple paragraph'인 태그의 내용을 모두 검색한다.
page.find_all(class_='simple paragraph')
```




    [<p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>,
     <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>]




```python
# 태그 이름 없이 속성 이름만으로도 찾을 수 있다.
# 문서에서 속성 id의 값이 'link'인 태그의 내용을 모두 검색한다.
page.find_all(id='link')
```




    [<p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>,
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>]




```python
# 문서에서 속성 id의 값이 'link' 중 첫 번째 태그의 내용을 검색한다.
page.find(id='link')
```




    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>




```python
# 문서에서 모든 태그 a를 검색한다. 
# 태그 <a>를 모두 찾는다.
page.find_all('a')
```




    [<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>,
     <a href="https://www.python.org" id="python">Python Official Web Page</a>]




```python
# 문서에서 모든 태그 div를 검색한다. 
# 태그 <div>를 모두 찾는다.
page.find_all('div')
```




    [<div>
     <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
     <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
     </div>]



# 텍스트 처리

**get_text()** 
- 문서 또는 태그 내의 모든 텍스트를 하나의 유니코드 문자열(single Unicode string)로 반환

**get_text(strip=True)** 
- 각 텍스트의 시작과 끝에서 화이트스페이스를 제거한다.

**get_text('separator')** 
- 각 텍스트를 결합하는데 사용할 문자열을 설정한다.

**strings** 
- 모든 문자열을 순회하는 제너레이터(generator)다.

**stripped_strings** 
- 전체가 화이트스페이스인 문자열이나 문자열의 처음과 끝의 화이트스페이스를 제거하는 제너레이터(generator)다.

## get_text()


```python
page
```




    <!DOCTYPE html>
    
    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>




```python
# 문서(page)에서 모든 태그를 제거한 텍스트만 가져온다.
# 반환한 객체의 자료형은?
# 하나의 유니코드 문자열(single Unicode string)로 반환한다.
page.get_text()
```




    '\n\nA Simple Local Web Page\n\nThe First Heading\nParagraph under the first heading.\nThe second heading\nParagraph #1 under the second heading.\nParagraph #2 under the second heading.\n\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n\n\n'




```python
# (방법 1) 태그 title을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.title.get_text()
```




    'A Simple Local Web Page'




```python
# (방법 2) 태그 title을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.find('title').get_text()
```




    'A Simple Local Web Page'




```python
# (방법 1) 태그 head을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.head.get_text()  # same as page.title.get_text()
```




    'A Simple Local Web Page'




```python
# (방법 2) 태그 head을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.find('head').get_text()
```




    'A Simple Local Web Page'




```python
# (방법 1) 태그 h1을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.h1.get_text()  
```




    'The First Heading'




```python
# (방법 2) 태그 h1을 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.find('h1').get_text()
```




    'The First Heading'




```python
# (방법 1) 태그 div를 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.div.get_text()
```




    '\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n'




```python
# (방법 2) 태그 div를 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.find('div').get_text()
```




    '\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n'




```python
# --- get_text('sep', strip=False) 
# 태그 body를 찾아 모든 태그를 제거한 텍스트만 가져온다.
page.body.get_text()

# page.find('body').get_text()와 같다.
```




    '\nThe First Heading\nParagraph under the first heading.\nThe second heading\nParagraph #1 under the second heading.\nParagraph #2 under the second heading.\n\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n\n'




```python
# --- get_text('sep', strip=False) 
# 태그 body를 찾아 모든 태그와 각 텍스트의 시작과 끝에 있는 화이트스페이스를 제거한 텍스트만 가져온다.
# [참고] 텍스트 중간에 있는 화이트스페이스는 제거할 수 없다.
page.body.get_text(strip=True)
```




    'The First HeadingParagraph under the first heading.The second headingParagraph #1 underthe second heading.Paragraph #2 underthe second heading.This is a link toBusiness School at SNU.We also want to visitPython Official Web Page.'




```python
# --- get_text('sep', strip=False) 
# 태그 body를 찾아 모든 태그를 제거한 후 각 텍스트를 문자열 ':::'로 결합한 텍스트를 가져온다.
page.body.get_text(':::')  # sep 결합문자
```




    '\n:::The First Heading:::\n:::Paragraph under the first heading.:::\n:::The second heading:::\n:::Paragraph #1 under :::the second heading:::.:::\n:::Paragraph #2 under :::the second heading:::.:::\n:::\n:::This is a link to :::Business School at SNU:::.:::\n:::We also want to visit :::Python Official Web Page:::.:::\n:::\n'




```python
# --- get_text('sep', strip=False) 
# 태그 body를 찾아 모든 태그와 각 텍스트의 시작과 끝에 있는 화이트스페이스를 제거한 
# 각 텍스트를 문자열 콤마(',')로 결합한 텍스트를 가져온다.
page.get_text(',', strip=True)
```




    'A Simple Local Web Page,The First Heading,Paragraph under the first heading.,The second heading,Paragraph #1 under,the second heading,.,Paragraph #2 under,the second heading,.,This is a link to,Business School at SNU,.,We also want to visit,Python Official Web Page,.'




```python
# 문서에서 모든 태그 a를 검색하여 변수에 할당한 후 그 결과를 출력한다. 
tags = page.find_all('a')
print(tags, end='\n\n')

# 태그 a의 텍스트는 변수 text에 할당하고 
# 속성 href의 속성값은 변수 link에 할당한 후 출력한다.
# [힌트] 태그 내 속성은 딕셔너리로 표현된다.
for tag in tags:
    text = tag.string   # tag.get_text()와 같다.
    link = tag['href']  # 속성은 딕셔너리로 표현되며 키(속성)로 매핑값(속성값)을 가져올 수 있다.
    print(f'{text} -> {link}')
```

    [<a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>, <a href="https://www.python.org" id="python">Python Official Web Page</a>]
    
    Business School at SNU -> http://biz.snu.ac.kr
    Python Official Web Page -> https://www.python.org


## get_text(), strings, stripped_strings의 단순 비교


```python
page
```




    <!DOCTYPE html>
    
    <html>
    <head><title>A Simple Local Web Page</title></head>
    <body>
    <h1>The First Heading</h1>
    <p>Paragraph under the first heading.</p>
    <h2>The second heading</h2>
    <p class="simple paragraph" id="para">Paragraph #1 under <b>the second heading</b>.</p>
    <p class="simple paragraph">Paragraph #2 under <u>the second heading</u>.</p>
    <div>
    <p class="div first-link" id="link">This is a link to <a href="http://biz.snu.ac.kr" id="snubiz">Business School at SNU</a>.</p>
    <p class="div second-link" id="link">We also want to visit <a href="https://www.python.org" id="python">Python Official Web Page</a>.</p>
    </div>
    </body>
    </html>




```python
page.get_text()
```




    '\n\nA Simple Local Web Page\n\nThe First Heading\nParagraph under the first heading.\nThe second heading\nParagraph #1 under the second heading.\nParagraph #2 under the second heading.\n\nThis is a link to Business School at SNU.\nWe also want to visit Python Official Web Page.\n\n\n'




```python
print(page.get_text())
```

    
    
    A Simple Local Web Page
    
    The First Heading
    Paragraph under the first heading.
    The second heading
    Paragraph #1 under the second heading.
    Paragraph #2 under the second heading.
    
    This is a link to Business School at SNU.
    We also want to visit Python Official Web Page.
    
    
    



```python
page.strings
```




    <generator object Tag._all_strings at 0x7fd5397a34a0>




```python
page.stripped_strings
```




    <generator object Tag.stripped_strings at 0x7fd5397a3120>




```python
tuple(page.strings)
```




    ('\n',
     '\n',
     'A Simple Local Web Page',
     '\n',
     '\n',
     'The First Heading',
     '\n',
     'Paragraph under the first heading.',
     '\n',
     'The second heading',
     '\n',
     'Paragraph #1 under ',
     'the second heading',
     '.',
     '\n',
     'Paragraph #2 under ',
     'the second heading',
     '.',
     '\n',
     '\n',
     'This is a link to ',
     'Business School at SNU',
     '.',
     '\n',
     'We also want to visit ',
     'Python Official Web Page',
     '.',
     '\n',
     '\n',
     '\n')




```python
tuple(page.stripped_strings)
```




    ('A Simple Local Web Page',
     'The First Heading',
     'Paragraph under the first heading.',
     'The second heading',
     'Paragraph #1 under',
     'the second heading',
     '.',
     'Paragraph #2 under',
     'the second heading',
     '.',
     'This is a link to',
     'Business School at SNU',
     '.',
     'We also want to visit',
     'Python Official Web Page',
     '.')




```python
for content in page.strings:
    print(repr(content))
```

    '\n'
    '\n'
    'A Simple Local Web Page'
    '\n'
    '\n'
    'The First Heading'
    '\n'
    'Paragraph under the first heading.'
    '\n'
    'The second heading'
    '\n'
    'Paragraph #1 under '
    'the second heading'
    '.'
    '\n'
    'Paragraph #2 under '
    'the second heading'
    '.'
    '\n'
    '\n'
    'This is a link to '
    'Business School at SNU'
    '.'
    '\n'
    'We also want to visit '
    'Python Official Web Page'
    '.'
    '\n'
    '\n'
    '\n'



```python
for content in page.stripped_strings:
    print(repr(content))
```

    'A Simple Local Web Page'
    'The First Heading'
    'Paragraph under the first heading.'
    'The second heading'
    'Paragraph #1 under'
    'the second heading'
    '.'
    'Paragraph #2 under'
    'the second heading'
    '.'
    'This is a link to'
    'Business School at SNU'
    '.'
    'We also want to visit'
    'Python Official Web Page'
    '.'



```python
[text for text in page.stripped_strings]
```




    ['A Simple Local Web Page',
     'The First Heading',
     'Paragraph under the first heading.',
     'The second heading',
     'Paragraph #1 under',
     'the second heading',
     '.',
     'Paragraph #2 under',
     'the second heading',
     '.',
     'This is a link to',
     'Business School at SNU',
     '.',
     'We also want to visit',
     'Python Official Web Page',
     '.']



- - -

# THE END
