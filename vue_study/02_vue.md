@@ -1,4 +1,81 @@
# 02 개발 환경 셋팅

<br/>

## 02-1 뷰 학습을 위한 개발 환경 설정하기

<br/>

- 크롬 브라우저
- 아톰(Atom) 텍스트 에디터
- 노드제이에스(Node.js)
- 뷰 개발자 도구(Vue.js devtools, 크롬 확장 플러그인)

<br/>

### 1단계 크롬 브라우저 설치하기

https://www.google.co.kr/chrome/index.html

<br/>

### 2단계 아톰 에디터 설치하기

https://atom.io/

<br/>

### 3단계 Node.js 설치하기

> Node.js는 서버 사이드 자바스크립트로, 서버측에서 실행되는 자바스크립트 실행 환경을 의미합니다.
>
> CLI(Command Line Interface)를 이용하여 쉽게 뷰 프로젝트를 구성하려면 Node.js가 설치 되어 있어야 합니다. 또한 뷰 CLI로 생성한 프로젝트에서 프로토타이핑을 할 때도 Node.js 서버를ㄹ 사용하기 때문에 필수적인 환경입니다.

https://nodejs.org/en/

1. **LTS 버전 다운로드**
2. 윈도우 명령 프롬프트나, 맥의 터미넣에서 node -v를 실행합니다. 정상적으로 설치된 경우엔 Node.js 버전이 표시됩니다.

<br/>

### 4단계 뷰 개발자 도구 설치하기

https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd

<br/>

------

<br/>

## 02-2 Hello Vue.js! 프로젝트 만들기

<br/>

#### 뷰 시작하기

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
