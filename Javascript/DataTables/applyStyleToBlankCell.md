## excel export시 빈 cell에 style 적용

DataTable에서 excel export시 style 적용은 [홈페이지](https://datatables.net/reference/button/excelHtml5) 확인할 수 있다. 

아래와 같이 attribute를 적용하여 style을 바꿀 수 있다.
```js
customize: function ( xlsx ) {
    let sheet = xlsx.xl.worksheets['sheet1.xml'];
 
    $('c[r=A1] t', sheet).text('Custom text');
    $('row:first B', sheet).attr( 's', '42' );
    $('c[r=C4]', sheet).attr('s', '25');
}
```
하지만 기본적으로 빈 cell에는 style이 적용되지 않는다.

아래와 같이 `createEmptyCells: true`을 추가해주면 원하는 style이 빈 cell에 적용된다.
```js
$('#DataTable').DataTable({
    dom: 'Bfrtip',
    buttons: [
        {
            extend: 'excelHtml5',
            title: '공사명 : ' + material["constructionName"],
            createEmptyCells: true,
            customize: function (xlsx) {
                let sheet = xlsx.xl.worksheets['sheet1.xml'];
                
                $('c[r=A1] t', sheet).text('Custom text');
                $('row:first B', sheet).attr( 's', '42' );
                $('c[r=C4]', sheet).attr('s', '25');
            }
        }
    ]
}];
```

### 참고
- https://stackoverflow.com/questions/50105700/jquery-datatable-export-excel-cannot-apply-built-in-style-to-empty-cell
- https://datatables.net/reference/button/excelHtml5