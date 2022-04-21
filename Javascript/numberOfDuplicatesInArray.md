# 배열에서 중복 값 개수 구하기

```
1. forEach()
2. reduce() 
```

## ✅ forEach()

forEach()는 배열의 각각의 원소들을 순서대로 callback함수에 전달하여 실행한다.

```js
const animal = ["dog", "dog", "dog", "cat", "cat", "chicken"];
const result = {};

animal.forEach((x) =>{ 
    result[x] = (result[x] || 0) + 1;
});

console.log(result) // {"dog": 3, "cat": 2, "chicken": 1}
```

위에서 result[x] = (result[x] || 0) + 1 는 아래처럼 코드를 풀어쓸 수 있다.
```js
if (result[x]) {
    result[x] = result[x] + 1;
} else {
    result[x] = 0 + 1;
}
```

## ✅ reduce()

출력값은 forEach()를 쓸 때와 동일하다.
reduce()는 배열 각각의 element들에 대해 파라미터로 입력받은 callback함수를 실행하여 하나의 return 값을 반환한다.

```js
const animal = ["dog", "dog", "dog", "cat", "cat", "chicken"];
const result = animal.reduce((accu, curr) => { 
    accu[curr] = (accu[curr] || 0) + 1; // accu : 이전 element에 대한 callback 함수 return 값, curr : 현재 처리중인 배열 element
    return accu;
}, {});

console.log(result)
```

reduce() 가 어떤식으로 배열을 순회하는 지 알기 위해 console을 찍어보았다.
```js
console.log( "accu:", accu, ",", "curr:", curr )

accu: {dog : 1}, curr: dog
accu: {dog : 2}, curr: dog
accu: {dog : 3}, curr: dog
accu: {dog : 3, cat: 1}, curr: cat
accu: {dog : 3, cat: 2}, curr: cat
accu: {dog : 3, cat: 2, chicken: 1}, curr: chicken
```

### 참고
- https://hianna.tistory.com/459
- https://velog.io/@dev_cecy/JAVASCRIPT-%EB%B0%B0%EC%97%B4%EC%9D%98-%EC%A4%91%EB%B3%B5-%EA%B0%92-%EA%B0%9C%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0-REDUCE