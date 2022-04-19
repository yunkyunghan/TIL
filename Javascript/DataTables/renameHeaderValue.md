# table column header 값 변경

## 특정 text 값 변경
아래의 방식으로 특정 text 값을 손쉽게 원하는 값으로 변경 할 수 있다.

```js
$(table).DataTable({
   'initComplete': function(settings){
      let api = new $.fn.dataTable.Api(settings);

      api.columns().header().each(function(column){
         if($(column).text() === 'HI'){
            $(column).text("HELLO");
         }
      });
   }
});
```

## 특정 text를 포함하는 값들을 일괄적(모두)으로 변경
쉽게 말하면 '바나나 젤리', '바나나 주스', 바나나킥' 모두 '바나나'로 변경하는 것이다.

`console.log($(column).text())`을 찍어보면 DataTable에 들어가있는 column 값들이 string으로 뜬다.

```
column: 바나나 젤리
column: 바나나 주스
column: 바나나 과자

column: 당근 주스
column: 당근 사과 주스
```

### 🧀 기존

|<span style="background-color:green">바나나 젤리</span>|<span style="background-color:green">바나나 주스</span>|<span style="background-color:green">바나나 과자</span>|<span style="background-color:orange">당근 주스</span>|<span style="background-color:orange">당근 칵테일</span>|
|---|---|---|---|---|
|젤리|주스|과자|젤리|주스|칵테일|
|10|20|10|30|40|20|


```js
$(table).DataTable({
   'initComplete': function(settings){
      let api = new $.fn.dataTable.Api(settings);

      api.columns().header().each(function(column){
         if($(column).text().split(' ')[0]){
           $(column).text($(column).text().split(' ')[0]);
         }
      });
   }
});
```

### 🍔 변경
|<span style="background-color:green">바나나</span>|<span style="background-color:green">바나나</span>|<span style="background-color:green">바나나</span>|<span style="background-color:orange">당근</span>|<span style="background-color:orange">당근</span>|
|---|---|---|---|---|
|젤리|주스|과자|젤리|주스|칵테일|
|10|20|10|30|40|20|


### 참고
- https://stackoverflow.com/questions/31128065/changing-column-names-inside-datatables