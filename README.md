PDF Filler (Node.js)
======
[![NPM](https://nodei.co/npm/pdffiller.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/pdffiller/)


A node.js PDF form field data filler and FDF generator toolkit. This essentially is a wrapper around the PDF Toolkit library <a target="_blank" href="http://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/">PDF ToolKit</a>.


Quick start
-----------

First, run `npm install pdffiller --save` for your app. Then:

```js
var pdfFiller = require('pdffiller');

// ...
```


##Examples

#### 1.Fill PDF with existing FDF Data
````javascript
var pdfFiller   = require('pdffiller');

var sourcePDF = "test/test.pdf";
var outputPDF =  "test/test_complete.pdf";

var data = {
    "last_name" : "John",
    "first_name" : "Doe",
    "date" : "Jan 1, 2013",
    "football" : "Off",
    "baseball" : "Yes",
    "basketball" : "Off",
    "hockey" : "Yes",
    "nascar" : "Off"
};

pdfFiller.fillForm( sourcePDF, outputPDF, data, function(err) {
    if (err) throw err;
    console.log("In callback (we're done).");
});

````

This will take the test.pdf, fill the fields with the data values
and create a complete filled in PDF (test_complete.pdf)


#### 2. Generate FDF from PDF
````javascript
var pdfFiller   = require('pdffiller');

var sourcePDF = "test/test.pdf";
pdfFiller.getFdf( sourcePDF, function(err, fdf) { 
    if (err) throw err;
    console.log(fdf);
});

````

This will print out:
````'%FDF-1.2 %âãÏÓ
1 0 obj
<<
/FDF
<<
/Fields [<<
/V()
/T(first_name)
>><<
/V()
/T(last_name)
>><<
/V()
/T(date)
>><<
/V()
/T(football)
>><<
/V()
/T(baseball)
>><<
/V()
/T(basketball)
>><<
/V()
/T(nascar)
>><<
/V()
/T(hockey)
>>]
>>
>>
endobj
trailer

<<
/Root 1 0 R
>>
%%EOF
'````

#### 3. Query PDF for form fields
````javascript
var pdfFiller = require('pdffiller'),
    sourcePDF = "test/test.pdf",
    FDF_data,
    destinationPDF =  "test/test_complete.pdf";

pdfFiller.getFormFields( sourcePDF, function(err, formFields) {
    if (err) throw err;
    console.log(formFields);
});
````

This will print out:
```
[
    {
        fieldType: 'Text',
        fieldName: 'first_name',
        fieldFlags: '0',
        fieldJustification: 'Left'
    },
    {
        fieldType: 'Text',
        fieldName: 'last_name',
        fieldFlags: '0',
        fieldJustification: 'Left'
    },
    {
        fieldType: 'Text',
        fieldName: 'date',
        fieldFlags: '0',
        fieldJustification: 'Left'
    },
    {
        fieldType: 'Button',
        fieldName: 'football',
        fieldFlags: '0',
        fieldJustification: 'Left',
        fieldStateOption: 'Yes'
    },
    {
        fieldType: 'Button',
        fieldName: 'baseball',
        fieldFlags: '0',
        fieldJustification: 'Left',
        fieldStateOption: 'Yes'
    },
    {
        fieldType: 'Button',
        fieldName: 'basketball',
        fieldFlags: '0',
        fieldJustification: 'Left',
        fieldStateOption: 'Yes'
    },
    {
        fieldType: 'Button',
        fieldName: 'nascar',
        fieldFlags: '0',
        fieldJustification: 'Left',
        fieldStateOption: 'Yes'
    },
    {
        fieldType: 'Button',
        fieldName: 'hockey',
        fieldFlags: '0',
        fieldJustification: 'Left',
        fieldStateOption: 'Yes'
    }
];
```
