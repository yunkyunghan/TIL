## moment.js를 이용하여 Date 다루기 

### 원하는 day 만큼 더하기
```js
startdate = "06.04.2022";
var new_date = moment(startdate, "DD-MM-YYYY").add('days', 5);

console.log("startdate:", startdate) // 11.04.2022
```
### List의 길이만큼 day를 1씩 더하기
```js
let todayDate = moment('20220405');
let exampleList = 
                    [ 
                        {name: "han", age: "20", city: "seoul"}, 
                        {name: "lee", age: "25", city: "daejeon"} 
                    ];

for (let j = 0; j < exampleList.length; j++) { 
        exampleList["nextDay"] = todayDate.add(1, "days").format('MM-DD');
}

console.log("exampleList:", exampleList) 
// [ 
//    {name: "han", age: "20", city: "seoul", nextDay: "04-06"}, 
//    {name: "lee", age: "25", city: "daejeon", nextDay: "04-07"} 
//  ];

console.log("exampleList["nextDay"]:", exampleList["nextDay"]) // 04-06, 04-07
```

### 참고
- https://stackoverflow.com/questions/22547129/momentjs-date-string-add-5-days