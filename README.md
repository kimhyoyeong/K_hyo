# 자바스크립트+jquery 완전정복 스터디 3 (중급/고급/활용편)

## lesson1~ lesson4 

### **클래스란**?

연관있는 변수와 함수를 그룹짓거나, 재사용하기위해 사용하는 문법

### **종류**?

1. 리터럴방식 
   장 : 정의함과 동시에 인스턴스가 자동으로 만들어지기 때문에 인스턴스를 만드는 구문을 작성하지않아도됨 
   단 : 인스턴스를 여러개 만들수 없음 (중복코드가 많이생김)
   결 : 여러개의 데이터를 묶어 값을 보관하거나 함수의 매개변수 값으로 전달할때 사용함
2. 함수방식 
   일반함수 만드는 방식과 동일함 구분을 위해 대문자로 시작(일반적인규칙)
   장 : 코드 재사용가능
   단 : 인스턴스 마다 내부에 모든 메서드가 독립적으로 만들어짐
3. 프로토타입방식  - 다음시간

### **용어**?

1. 인스턴스 - new 키워드를 이용해 클래스 실체를 생성할때 사용 (클래스가 설계도라면 인스턴스는 설계도로 만들어진 결과물)
2. 객체 - 인스턴스 생성후 클래스에서 제공하는 프로퍼티와 메서드를 사용할때 주로 사용 
   ex) var 인스턴스 = new Tab(); / Tab 클래스의 인스턴스 생성 == Tab 클래스의 객체 생성
3. 프로퍼티(멤버변수) - var 변수 = 값;
4. 메서드(멤버함수) -  function 함수(){}



```javascript
//리터럴방식-기본문법
var user={ //인스턴스
	name:"hyo",//프로퍼티:초기값,
	age:10,
	showInfo:function(){//메서드:function()
		document.write("name="+this.name+"age="+this.age);
	}
}

user.showInfo();//인스턴스.메서드();
document.write(user.name);//인스턴스.프로퍼티;

//함수방식-기본문법
function User(){
	this.name="hyo";
	this.age=10;
	this.showInfo=function(){
		document.write("name="+this.name+"age="+this.age);
	}
}

var user=new User();//인스턴스 생성
user.showInfo();//메서드호출

```
