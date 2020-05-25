# CSS FlexBox

``` CSS
.container {
    display: flex;
}
```

를 통해 flexbox를 정의할 수 있다.

### FlexBox container의 속성

#### flex-direction

```CSS
.container {
    flex-direction: row | row-reverse | column | column-reverse;
}
```

row : 현재의 흐름에서 일렬로

row-reverse : 현재의 흐름과 반대로 일렬로

column : 위에서 아래로

column-reverse : 아래에서 위로



#### flex-wrap

```CSS
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

nowrap : 모든 내용이 하나의 줄에서(넘치든 말든)

wrap : 넘치면 다음줄로

wrap-reverse : 넘치면 윗줄로



#### flex-wrap

ex)

```CSS
.container {
    flex-flow: nowrap wrap;
}
```

flex-direction과 flex-wrap를 한 곳에 적을 수 있는 속성



#### justify-content

```CSS
.container {
    flex-flow: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe;
}
```

![justify-content](images/justify-content.svg)

#### align-items

```CSS
.container {
  align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe;
}
```
