# 03 화면을 개발하기 위한 필수 단위 - 인스턴스 & 컨포넌트

<br/>

## 03-1 뷰 인스턴스

<br/>

### 뷰 인스턴스의 정의와 속성

뷰 인스턴스는 뷰로 화면을 개발하기 위해 필수 적으로 생성해야하는 기본단위 입니다.

<br/>

#### 뷰 인스턴스 생성

```javascript
new Vue({
    ...
});
```

```html
<!DOCTYPE html>
<html lang="ko">
	<head>
		<meta charset="utf-8">
        <title>Vue Sample</title>
    </head>
    <body>
        <div id="app">
            {{message}}
        </div>
        <script src="https://unpkg.com/vue/dist/vue.js"></script>
        <script>
            //인스턴스
			new Vue({
				el: '#app',//el 속성
				data: { //data 속성
					message: 'Hellow Vue.js!'
				}
			})
        </script>
    </body>
</html>
```

> Hellow Vue.js!를 출력하는 코드

<br/>

#### 뷰 인스턴스 생성자

new Vue()로 인스턴스를 생성할 때 Vue를 생성자라고 합니다. Vue 생성자는 뷰 라이브러리를 로딩하고 나면 접근할 수 있습니다. 

생성자를 사용하는 이유는 뷰로 개발할 때 필요한 기능들을 생성자에 미리 정의해 놓고 사용자가 그 기능을 재정의하여 편리하게 사용하도록 하기 위해서 입니다.

<br/>

### 뷰 인스턴스 옵션 속성

뷰 인스턴스 옵션 속성은 인스턴스를 생성할 때 재 정의할 data, el, template 등의 속성을 의미합니다.

```javascript
//인스턴스
new Vue({
    el: '#app',//el 속성 : 뷰로 만든 화면이 그려지는 시작점 (#app 돔 요소 css 선택자 규칙과같음)
    data: { //data 속성 : message라는 새로운 속성을 추가하고 'Hellow Vue.js!'값 부여
        message: 'Hellow Vue.js!'
    }
})
```

| 속성     | 설명                                                         |
| -------- | ------------------------------------------------------------ |
| template | 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성, <br />뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있음 |
| methods  | 화면 로직 제어와 관계된 메소드를 정의하는 속성,<br />마우스 클릭 이벤트 처리와 같은 화면의 전반적인 이벤트와 <br />화면 동작과 관련된 로직을 추가할 수 있음 |
| created  | 뷰 인스턴스가 생성되자마자 실행할 로직을 정의할 수 있는 속성 |

<br/>

### 뷰 인스턴스의 유효범위

뷰 인스턴스를 생성하면 HTML 특정 범위 안에서만 옵션 속성들이 적용되어 나타납니다. 이를 인스턴스의 유효범위라고 합니다.

> **인스턴스가 유효범위를 벗어 났을 경우**
>
> 현재 코드에 el 속성으로 지정한 div id="app"태그 아래에 오는 요소들로 제한되어 태그 밖에있는 {{message}} 요소를 인식하지 못하기 때문에 텍스트가 바뀌지않고 {{message}} 그대로 출력됩니다. 
>

```html
<script>
new Vue({
    el: '#app',//el 속성 : 뷰로 만든 화면이 그려지는 시작점
    data: {//data 속성 : message라는 새로운 속성을 추가하고 'Hellow Vue.js!'값 부여
        message: 'Hellow Vue.js!'
    }
})
</script>

<div id="app">

</div>

{{message}}
```

<br/>

### 뷰 인스턴스 라이브 사이클

인스턴스의 상태에 따라 호출할 수 있는 속성들을 **라이프 사이클(life cycle)** 속성이라고 합니다.

그리고 각 라이프 사이클 속성에서 실행되는 커스텀 로직을 라이프 사이클 훅(hook)이라고 합니다.



![vue lifecycleì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](http://cfile8.uf.tistory.com/image/994C103B5A7878FE221AFE)



위 그림은 인스턴스가 생성되고 나서 소멸되기까지의 전체적인 흐름을 나타낸 뷰 인스턴스 라이프 사이클 다이어 그램입니다.

라이프 사이클 단계를 크게 나누면 **인스턴스 생성**, **생성된 인스턴스를 화면에 부착**, **화면에 부착된 인스턴스의 내용이 갱신**, **인스턴스가 제거되는 소멸** 4단계로 이루어집니다.

<br/>

| 단계          | 설명                                                         |
| ------------- | ------------------------------------------------------------ |
| beforeCreate  | 인스턴스가 생성되고 나서 가장 처음으로 싱행되는 단계입니다.<br />이 단계에서는 data 속성과 methods 속성이 <br />아직 인스턴스에 정의되어 있지 않고, <br />돔과 같은 화면 요소에도 접근할수 없습니다. |
| created       | beforeCreate 단계 다음에 실행되는 단계입니다. <br />data 속성과 methods 속성이 정의 되었기 때문에 <br />this.data와 같이 속성에 정의된 값에 접근하여 로직을 실행 할수 있습니다. <br />다만, 아직 인스턴스가 화면에 부착되기 전이기 때문에 <br />template 속성에 정의된 돔 요소로 접근할수 없습니다. <br />그리고, data 속성과 methods 속성에 접근할 수 있는 <br />첫 단계이자 컴포넌트가 생성되고 나서 실행되는 단계이기 때문에 <br />서버에 데이터를 요청하여 받아오는 로직을 수행하기 좋습니다. |
| beforeMount   | created단계 이후 <br />template 속성에 지정한 마크업 속성을 render() 함수로 변환한 후 <br />el 속성에 지정한 화면 요소에 인스턴스를 부착하기 전에 호출되는 단계입니다. <br />render() 함수가 호출되기 직전의 로직을 추가하기 좋습니다. |
| mounted       | 인스턴스가 부착되고 나면 호출되는 단계로, <br />template 속성에 정의한 화면 요소에 접근할 수 있어 <br />화면 요소를 제어하는 로직을 수행하기 좋은 단계입니다. <br />다만, 돔에 인스턴스가 부착되자마자 호출되기 때문에 <br />하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면 요소들이 <br />최종 HTML 코드로 변환되는 시점과 다를수있습니다. |
| beforeUpdate  | 인스턴스가 부탁되고나면 인스턴스에 정의한 속성들이 화면에 치환됩니다. <br />치환된 값은 뷰의 반응성을 제공하기위해 $watch 속성으로 감시합니다. <br />이를 데이터 관찰이라고합니다. <br /><br />beforeUpdate는 관찰하고 있는 데이터가 변경되면 <br />가상 돔으로 화면을 다시 그리기 전에 호출되는 단계이며 <br />변경 예정인 새 데이터에 접근 할수있어서 변경 예정 데이터의 값과 관련된 로직을 미리 넣을 수 있습니다.  <br />만약 여기에 값을 변경하는 로직을 넣더라도 화면이 다시 그려지지는 않습니다. |
| updated       | 데이터가 변경되고 나서 가상 돔으로 다시 화면을 그리고나면 실행되는 단계입니다. <br />데이터 변경까지 완료된 시점임으로 데이터 변경후 화면 요소 제어와 관련된 로직을 추가하기 좋은 단계입니다. <br />이 단계에서 데이터 값을 변경하면 무한 루프에 빠질 수 있기 때문에 값을 변경하려면 computed, watch 속성을 사용해야합니다. <br />따라서, 데이터 값을 갱신하는 로직을 beforeUpdate, 변경 데이터의 화면요소와 관련된 로직은 updated에 추가하는 것이 좋습니다. |
| beforeDestroy | 뷰 인스턴스가 파괴되기 직전에 호출되는 단계, 인스턴스 접근가능, 따라서 데이터를 삭제하기 좋은 단계입니다. |
| destroyed     | 뷰인스턴스가 파괴되고 나서 호출되는 단계입니다. 모든 속성이 제가되고 하위에 선언한 인스턴스들 또한 모두 파괴됩니다. |

> 라이프 사이클 훅이 실제로 어떻게 동작하는지 확인하기 위한 예제
>
> updated는 데이터 변경이 일어나 화면을 다시 그려졌을때 호출되는 로직이기 때문에 출력이 안됨

```html
<!DOCTYPE html>
<html lang="ko">
	<head>
		<meta charset="utf-8">
        <title>Vue Sample</title>
    </head>
    <body>
        <div id="app">
            {{message}}
        </div>
        <script src="https://unpkg.com/vue/dist/vue.js"></script>
        <script>
            //인스턴스
			new Vue({
				el: '#app',//el 속성
				data: { //data 속성
					message: 'Hellow Vue.js!'
				},
				beforeCreate:function(){
					console.log("beforeCreate");
				},
				created:function(){
					console.log("created");
				},
				mounted:function(){
					console.log("mounted");
					//this.message="값 변경했어용!";
				},
				updated:function(){
					console.log("updated");
				}
				
			})
        </script>
    </body>
</html>
```

