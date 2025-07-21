# Google Sheets Scripts and Tips

## Remove line duplicates in Google Sheets
- Tools > Script Editor, add and run:
```js
function removeDuplicates() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var data = sheet.getDataRange().getValues();
  var newData = new Array();
  for(i in data){
    var row = data[i];
    var duplicate = false;
    for(j in newData){
      if(row.join() == newData[j].join()){
        duplicate = true;
      }
    }
    if(!duplicate){
      newData.push(row);
    }
  }
  sheet.clearContents();
  sheet.getRange(1, 1, newData.length, newData[0].length).setValues(newData);
}
```

## Split cell contents into rows based on carriage return
```
=transpose(split(join(char(10),A1:A4),char(10)))
```
