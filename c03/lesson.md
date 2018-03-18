# L01_jQuery 확장 소개



### 01_소개

jQuery가 성공할 수 있었던 가장 큰 이유는 수많은 jQuery플러그인 때문!

**jQuery가 제공하는 기본적인 기능 뿐만 아니라 필요시 다른 개발자가 만든 기능을 손쉽게 확장이 가능함**

**자바스크립트 클래스로 만들어 사용하는 것보다 jQuery 플러그인으로 만들면 좀더 쉽고 간결하게 사용할 수 있음.**

```javascript
//자바스크립트 방식
var tab1=new TabMenu("#tabMenu");
tab1.setSelectItemAt(1);

//jQuery 플러그인 방식
$("#tabMenu1").setSelectItemAt(1);
```



### 02_jQuery 확장 요소 종류

| 유틸리티                                                     | 플러그인                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 문자열의 앞뒤 공백을 없애주는 trim() 메서드와 같이 클래스 직접 접근해서 도움을 주는 기능 | 아코디언 메뉴나 탭메뉴와 같이 주로 노드를 다루는 특정 기능을 재사용하고자 할때 사용하는 포장 기능 |





------





# L02_jQuery 유틸리티



### 01_소개

**jQuery유틸리티는 인스턴스를 생성하지 않고 클래스 직접 접근해 도움을 주는 기능**

jQuery 유틸리티는 문자열의 앞 뒤 공백을 없애주는 jQuery의 trim() 메서드와 같이 
클래스 직접 접근하여 주로 도움을 주는 기능을 함.

1. trim() : 공백제거
2. index() : 인덱스 탐색
3. extend() : 객체 병합
4. data() : HTML Element에 <key : value> 형태로 데이터를 저장/조회

jQuery 유틸 참조 : <http://api.jquery.com/category/Utilities/



### 02_구조

```javascript
//문법
(function($){
    $.유틸리티 = function(){
        //기능 구현
    }
})(jQuery);


//접근방법
jQuery.유틸리티();
//또는
$.유틸리티();
```



### 03_사용하기

```javascript
$(document).ready(function(){
    var data="      abc     ";
    console.log("실행 전 = "+data+", 실행 후 ="+$.trim(data));
})

//실행결과
//1.실행전=      abc     ,실행 후=abc
```



### 04_만들기

```javascript
(function($){
    $.addComma=function(value){
        var num=value+"";
        var arr=num.split("");
        var startPoint=arr.length-3;

        for(var i=startPoint;i>0;i-=3){
            arr.splice(i,0,",");
        }
        return arr.join("");//배열의 원소들을 하나의값으로 만듬
    }
})(jQuery);

$(document).ready(function(){
    document.write("123=>",$.addComma("123"),"<br>");
    document.write("1231231232=>",$.addComma("1231231232"),"<br>");
})
//실행결과
//123=>123
//1231231232=>1,231,231,232
```



------





# L03_jQuery 플러그인



### 01_소개

jQuery 플러그인은 아코디언 메뉴나 탭메뉴와 같이 특정 기능을 재사용하고자 할때 사용하는 포장 기능!

쉽게말해 jQuery유틸리티는 제외한 모든 기능은 jQuery 플로그인이라고 생각하면 됨!



### 02_구조

유틸리티의 경우 클래스 메서드로 만드는 것과 달리 플러그인은 jQuery 클래스의 fn이란 곳에 플러그인을 만듬.

**여기서 fn은 prototype의 줄인 닉네임일뿐. **( $.fn = jQuery.protorype)

```javascript
//문법
(function($){
    $.fn.플러그인이름=function(속성값){
        this.each(function(index){
            //기능구현
        }
        return this;
    }
})(jQuery)
```

예를 들어 지금까지 즐겨사용한 find(), filter(), children() 등을 다음과 같이 표현할수 있음.

```javascript
function jQuery(){
    
}
jQuery.protorype.find=function(){
    ...
}
jQuery.protorype.children=function(){
    ...
}
jQuery.protorype.플러그인이름=function(){
    ...
}
```

즉,  jQuery 플러그인 모두 jQuery의 인스턴스 메서드일 뿐이라는 것임. 



### 03_구조 분석

```javascript
(function($){
    $fn.redColor=function(){
        this.each(function(index){
            $(this).css("border","4px solid #f00");
        })
        return this;
    }
})(jQuery);

$(document).ready(function(){
    $("p").redColor();
})
```



```javascript
(function($){
    $fn.redColor=function(){
   //$.fn = jQuery.protorype 동일함
        
        this.each(function(index){
            
            $(this).css("border","4px solid #f00");
            //$(this)구문을 이용 jQuery 인스턴스를 생성한 후 css()메서드를 사용함.
            
        })
        
        return this;
        //$("p").redColor.on(..)과 같이 플러그인 호출 후 jQuery 메서드를 체인 구조로 호출 할수있게 하기위해 this를 리턴해줘야함. 
        //var $temp = $("p").redColor();
        //$temp.on(...);
        //이때 $temp에 저장되는 값이 바로 return this이다. this는 jQuery인스턴스이기 때문에 $temp.on() 메서드를 연속해서 호출 할수있게 됨
        
    }
})(jQuery);

$(document).ready(function(){
    $("p").redColor();
    //클래스의 일반 메서드를 사용하기 위해서 인스턴스를 생성해야하는데, $("p")에 의해 생섬됨
    //접근연산자인 .을 활용해 신규생성한 redColor() 메서드(플러그인)를 호출한것임
})
```



### 04_만들기

*작업파일확인*