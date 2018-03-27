# Javascript - 축약

## if ~ else 문

```javascript
//long
function userName(pName) {
	if (pName) {
		console.log("true");
	} else {
		console.log("false");
	}
}
userName('lee');
```

```javascript
//short
function userName(pName) {
	pName ? console.log("true") : console.log("false");
}
userName('lee');
```



## || short-circuit evaluation

기본 값을 부여하기 위해 파라미터의 null 또는 undefined 여부를 파악하느라 코드를 길게 작성하는것보다,
short-circuit evaluation 방법을 이용해서 한줄로 작성하는 방법이 있습니다.

```javascript
//long
function enter(pValue){
    if(pValue === null || pValue === undefined || pValue === ''){
        pValue='default value';
    }
    console.log(pValue);
}

enter("kim");//kim
enter();//default value
```

```javascript
//short
function enter(pValue){
    pValue = pValue || 'default value';
    console.log(pValue);
}

enter("kim");//kim
enter();//default value
```

`short-circuit evaluation`
두가지의 변수를 비교할때, 앞에 있는 변수가 false 일경우 결과는 무조건 false 이기때문에
뒤의 변수는 확인하지 않고 return 시키는 방법
위 예제에서는 pValue 값이 있을경우 넘어온 값을 할당하지만, 없으면 'default value'를 할당함