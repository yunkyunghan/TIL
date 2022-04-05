## Excel export 시 새로운 행 추가 (text 포함)
### 🌐 chrome, FireFox 
```js
customize: function (xlsx) {
                let sheet = xlsx.xl.worksheets['sheet1.xml'];
                let numrows = 3;
                let clR = $('row', sheet);

                //update Row
                clR.each(function () {
                    let attr = $(this).attr('r');
                    let ind = parseInt(attr);
                    ind = ind + numrows;
                    $(this).attr("r",ind);
                });

                // Create row before data
                $('row c ', sheet).each(function () {
                    let attr = $(this).attr('r');
                    let pre = attr.substring(0, 1);
                    let ind = parseInt(attr.substring(1, attr.length));
                    ind = ind + numrows;
                    $(this).attr("r", pre + ind);
                });

                function Addrow(index,data) {
                    msg='<row r="'+index+'">'
                    for(i=0;i<data.length;i++){
                        let key=data[i].key;
                        let value=data[i].value;
                        msg += '<c t="inlineStr" r="' + key + index + '">';
                        msg += '<is>';
                        msg +=  '<t>'+value+'</t>';
                        msg+=  '</is>';
                        msg+='</c>';
                    }
                    msg += '</row>';
                    return msg;
                }

                //insert
                let r1 = Addrow(1, [{ key: 'A', value: '' }, { key: 'B', value: '' }]);
                let r2 = Addrow(2, [{ key: 'A', value: '' }, { key: 'B', value: '' }]);
                let r3 = Addrow(3, [{ key: 'A', value: '' }, { key: 'B', value: '' }]);

                sheet.childNodes[0].childNodes[1].innerHTML = r1 + r2+ r3+ sheet.childNodes[0].childNodes[1].innerHTML;
            }

```

위의 방법은 IE 브라우저에서 되지 않아 downgrade된 방법을 찾았다.

### 🌐 IE

```js
customize: function (xlsx) {
                let sheet = xlsx.xl.worksheets['sheet1.xml'];
                let numrows = 4;
                let clR = $('row', sheet);

                //update Row
                clR.each(function () {
                    let attr = $(this).attr('r');
                    let ind = parseInt(attr);

                    ind = ind + numrows;
                    $(this).attr("r", ind);
                });

                // Create row before data
                $('row c ', sheet).each(function (index) {
                    let attr = $(this).attr('r');
                    let pre = attr.substring(0, 1);
                    let ind = parseInt(attr.substring(1, attr.length));

                    ind = ind + numrows;
                    $(this).attr("r", pre + ind);
                });

                function Addrow(index, data) {
                    let row = sheet.createElement('row');

                    row.setAttribute("r", index);  

                    for (i = 0; i < data.length; i++) {
                        let key = data[i].key;
                        let value = data[i].value;

                        let c  = sheet.createElement('c');
                        c.setAttribute("t", "inlineStr");
                        c.setAttribute("s", "2");
                        c.setAttribute("r", key + index);

                        let is = sheet.createElement('is');
                        let t = sheet.createElement('t');
                        let text = sheet.createTextNode(value);

                        t.appendChild(text);                                  
                        is.appendChild(t);
                        c.appendChild(is);
                        row.appendChild(c);                                                      
                    }

                    return row;
                }

                let r1 = Addrow(1, [{ key: 'A', value: '' }, { key: 'B', value: '' }, { key: 'C', value: ''}]);
                let r2 = Addrow(2, [{ key: 'A', value: '' }, { key: 'B', value: 'Report Date' }, { key: 'C', value: ''}]);                           
                let r3 = Addrow(3, [{ key: 'A', value: '' }, { key: 'B', value: ':' }, { key: 'C', value: '' }]);
                let r4 = Addrow(4, [{ key: 'A', value: '' }, { key: 'B', value: '' }, { key: 'C', value: ''}]);             

                let sheetData = sheet.getElementsByTagName('sheetData')[0];

                sheetData.insertBefore(r4,sheetData.childNodes[0]);
                sheetData.insertBefore(r3,sheetData.childNodes[0]);
                sheetData.insertBefore(r2,sheetData.childNodes[0]);
                sheetData.insertBefore(r1,sheetData.childNodes[0]);
}

```


#### 참고
- https://stackoverflow.com/questions/36352181/how-to-customize-export-to-csv-excel-pdf-in-jquery-datatables
- https://stackoverflow.com/questions/41485310/exporting-jquery-datatable-to-excel-with-additional-rows-is-not-working-ie 
