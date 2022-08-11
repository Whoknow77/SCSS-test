# SCSS  

CSS를 좀 더 편리하게 작성할 수 있음

Parcel bundler 가 scss를 읽어서 자동으로 css문법으로 변환해줌

----------------

## 중첩
```scss

.container{
    h1{
        color: red;
    }
}
```

다음과 같이 기존의 css에서 부모 요소를 매번 적어줘야했지만 태그 안에서 설정 가능

## 변수(유효범위를 따른다)
```scss

$color:royalblue;

.container{
    h1{
        color: $color;
    }
}
```
어떤 css 값을 자주 사용할 때 변수로 할당하여 사용가능

## & 기호 : 상위 선택자 참조

```scss
.btn{
    position: absolute;
    &.active{
        color:red;
    }
}

.list {
    li{
        &:last-child{
            margin-right:0;
        }
    }
}
```
**&기호는 상위 선택자를 치환한다.(btn, li)**

## 중첩된 속성 묶기

```scss

    .box{
        font:{
            weight:bold;
            size:10px;
            family:sans-serif; //scss
        };
    }
----------------------------------
.box{
    font-weight:bold;
    font-size:10px;
    font-family:sans-serif; //css
}
```

## 나누기(/) 연산

- 소괄호 이용
```scss
{
    margin:(30px / 2);
}
```

- 변수 이용
```scss
{
    $size:30px;
    margin:$size/2;
}
```

- 다른 연산자와 사용
```scss
{
    margin:10px + 12px /2;
}
```

## @(함수느낌)

```scss
@mixin center{
    display:flex;
    justify-content:center;
    align-items:center;
}

@mixin box($size: 100px, $color:tomato){ //기본값(매개변수 없을시 100px)
    width:$size;
    height:$size;
    background-color:$color;
}

.container{
    @include center;
    @include box; //100px tomato

}

.box{
    @include box(200px, red);
}

.item{
    @include box($color:green); //키워드 인수사용
}
```

## 반복문

```scss
@for $i from 1 through 10{ //1부터 10까지
    .box:nth-child(#{$i}){ //값 보관할때는 #
        width:100px* $i;
    }
}
```

## 함수(반환결과 사용, mixin은 속성 재활용)

```scss
@mixin center{ //속성의 재활용
    display:flex;
    justify-content:center;
    align-items:center;
}

@function ratio($size, $ratio){//연산, 반환
    @return $size * $ratio
}

.box{
    $width:100px;
    width:$width;
    height:ratio($width, 1/2);
    @include center;
}
```

## mix, lighten, darken, saturate

```
{
    mix(red,blue); //보라색
    lighten(red, 10%); //10% 밝게
    darken(red, 10%); //10% 어둡게
    saturate(red, 10%) //10% 채도 상승
    desaturate(red, 10%) //10% 채도 하강
    grayscale($color); //회색 만들기
    invert($color); //색 반전
    rgba($color, .5); //투명도
}
```

## 가져오기

```scss
@import "./sub", "./sub2";
// 확장자 생략, 여러개 가져오기 가능



