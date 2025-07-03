---
hide:
 - toc
---

# @Input decorator is used to send data fom PARENT-CHILD
### STEP:1 import childComp in ur parentComp 
``` title="parent.ts.file"                 
import {childComponent} from './directory';//import ur childComponent
         
  data1:string="mango" // varible:type="yourData"
  data2:string="sweet" 
```
  STEP:2 Your sending data from P-C so in [ parentComponent.html ] file use ur childComponent selector
``` title="parent.html"
  <app-child [d1]="data1"
             [d2]="data2"
   ></app-child>
```
### STEP:3 Now go to your childComponent and here your data is present in d1 & d2

``` title="child.ts"
  
import { Component, Input } from '@angular/core';
 @Input() d1:string;
 @Input() d2:string;
  
```
### STEP:4 use this d1 & d2 in HTML file

``` title="child.html"
<h1> {{d1}} </h1>
<h2> {{d2}} </h2>
```

## Example:2

### Input decorator and ngOnChanges(data:any){}
``` title="parent.ts"
@input is used to send data from parent to child 

array=[1,2,3,4] ;
name_type_code: NameTypeCodes[]; // this is present in the parent component 

formsubmitbutton(){
this.array=[...this.array,this.form.value]   
  }; //// (here we are pushing the formdata to that array)

  parent compnent 
    getNameTypeCode() {
    this.masterDataService.getNameCodes().pipe(takeUntil(this.onDestroy$)).subscribe(res => {
      this.name_type_code = res.body;
      this.nameTypeCodeStatus = true;
      ////console.log.log.log("name type code ==> ", res.body);
    })
    },

     ----parent html ---

<app-child 
     [array]="array"
     [name_type_code]="name_type_code" 
     >
  </app-child>  // (the selector of the child componenet )

```

``` title="child.ts"
import {component,Input} from '@angular/core'
@Input() name_type_code: NameTypeCodes[]; here the data we will get
@Input array:any; // ( here the data comes in that arrayFormat from the parent that data we can use it in any way )

    ---child html ----
<p>child works!</p>

@for(item of array ;track item ){  // (track is used for the performance)
     <li>{{item.firstname}}</li>
   }
@empty{   // (if the data is not present )
  <li>there is no data </li>
}


why we need to use ngOnChanges

-> the data is send from parent to child intitally when the component is loaded 
    only the initial data will come 

-> but when we need the updated data of that array when the form is submitted 
   so the updated data is triggered in that ngOnchnages

ngOnChanges(changes: SimpleChanges): void {
  // Object.keys(changes).forEach(key => this[key] = changes[key].currentValue);

if(changes['array']?.currentValue){
  let obj = changes['array']?.currentValue
  console.log(obj,'datadata')

  }
}
```
