# 엑셀에서 number가 자동 반올림되는 것 막기 

 [엑셀에 다중 적용](https://github.com/yunkyunghan/TIL/blob/master/Javascript/DataTables/applyMultipleStyle.md)을 했을 때 excel export 시 숫자가 자동 반올림된다. 

 아래 코드와 같이 `customizeData` 부분을 추가해주면 콤마도 잘 되고 자동반올림도 되지 않는다.
 `\u200C`를 써줌으로써 숫자를 문자열로 처리를 한다고 한다 : )

```js
$('#example').DataTable({
                dom: 'Bfrtip',
                buttons: [
                    
                        {
                        extend: 'excelHtml5',
                        customizeData: function (data) {
                            for (let i = 0; i < data.body.length; i++) {
                                for (let j = 0; j < data.body[i].length; j++) {
                                    data.body[i][j] = '\u200C' + data.body[i][j];
                                }
                            }
                        },
                       customize: function (xlsx) {
                           ...
                       }
                    }
                ]                  
});
```

### 참고
- https://stackoverflow.com/questions/71239048/jquery-datatable-format-column-as-string-when-exporting-to-excel
- https://stackoverflow.com/questions/24054004/datatables-tabletools-format-data-as-text-when-exporting-to-excel