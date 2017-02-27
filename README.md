# workbook
Wrapper for [SheetJS/js-xlsx](https://github.com/SheetJS/js-xlsx) providing convenient way to accumulate sheets, rows, styles.


[![NPM](https://nodei.co/npm/workbook.png?downloads=true&stars=true)](https://nodei.co/npm/workbook/)

## Install

* `npm install workbook --save`
* `npm install xlsx --save` 

Note that this can also wrap other versions of js-xlsx, e.g. [protobi/js-xlsx](https://github.com/SheetJS/js-xlsx), to allow application of styles using the `.s` attribute instead:

* `npm install js-xlsx-style --save` 


## Use

```js
var XLSX = require('xlsx');
var Workbook = require('./workbook');

var workbook = new Workbook()
    .addRowsToSheet("Main", [
      [
        {
           v: "This is a submerged cell",
           s:{
             border: {
               left: {style: 'thick', color: {auto: 1}},
               top: {style: 'thick', color: {auto: 1}},
               bottom: {style: 'thick', color: {auto: 1}}
             }
             }
        },
        {
             v: "Pirate ship",
             s:{
               border: {
                 top: {style: 'thick', color: {auto: 1}},
                 bottom: {style: 'thick', color: {auto: 1}}
               }
             }
        },
        {
             v: "Sunken treasure",
             s:{
               border: {
                 right: {style: 'thick', color: {auto: 1}},
                 top: {style: 'thick', color: {auto: 1}},
                 bottom: {style: 'thick', color: {auto: 1}}
               }
             }
        }
       ],
      [
        {"v": "Blank"},
        {"v": "Red", "s": {fill: { fgColor: { rgb: "FFFF0000"}}}},
        {"v": "Green", "s": {fill: { fgColor: { rgb: "FF00FF00"}}}},
        {"v": "Blue", "s": {fill: { fgColor: { rgb: "FF0000FF"}}}}
      ],
      [
        {"v": "Default"},
        {"v": "Arial", "s": {font: {name: "Arial", sz: 24}}},
        {"v": "Times New Roman", "s": {font: {name: "Times New Roman", sz: 16}}},
        {"v": "Courier New", "s": {font: {name: "Courier New", sz: 14}}}
      ],
      [
        0.618033989,
        {"v": 0.618033989},
        {"v": 0.618033989, "t": "n"},
        {"v": 0.618033989, "t": "n", "s": { "numFmt": "0.00%"}},
        {"v": 0.618033989, "t": "n", "s": { "numFmt": "0.00%"}, fill: { fgColor: { rgb: "FFFFCC00"}}},
        [(new Date()).toLocaleString()]
      ]
    ]).mergeCells("Main", {
      "s": {"c": 0, "r": 0 },
      "e": {"c": 2, "r": 0 }
    }).finalize();

var OUTFILE = '/tmp/wb.xlsx';
XLSX.writeFile(workbook, OUTFILE, {defaultCellStyle: { font: {name: 'Arial', sz: '12'}}});
console.log("Results written to " + OUTFILE)
```

