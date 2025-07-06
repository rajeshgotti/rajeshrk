---
hide:
 - toc
---

### PropertyBinding ante ts file vuna data ni Html lo cupinchadam

<details>
  <summary>PropertyBinding</summary>
  <img src="/images/propertyBinding.jpg" alt="Output image" style="max-width: 100%; height: auto;" />
</details>
<details>
  <summary>NgContent</summary>
  <img src="/images/ngContent.jpg" alt="Output image" style="max-width: 100%; height: auto;" />
</details>
<details>
  <summary>StyleBinding</summary>
  <img src="/images/stylebinding.jpg" alt="Output image" style="max-width: 100%; height: auto;" />
</details>

## syntax: [Property]  

```
      ==> [disabled] ==> [hidden]
```

### Note: True ante kanipinchadu, False ante kanipistundi

``` title="ts.file"
 isDisabled:boolean=true
 isHidden:boolean=false
 
```

```title="html"
<button [disabled]="isDisable">Disable</button>
    //button disable avtunndi bz of disable True,false iste kanipistundi
<input type="text" [hidden]="isHidden">
    //false icham kabati filed kanipistundi True iste Hide avtundni
```

## ex:2 
``` title="ts.file"
  path:string="../img/img/png" ; //stringType
```
``` title="html"  
 <img src={{path}} alt=""/>  (or) 
 <img [src]=path alt=""/> 
  Note: string type vunte html lo manam both propetyBinding or StringInterpolation edaina use cheskovachu
  mainly propetyBinding andedi Boolean type kosam use chestam

```
 ## RealTime example:
``` title="html.file"
     <button mat-stroked-button color="primary" (click)="continueClick(item)"
       [disabled]="item?.medicationStatus?.toLowerCase() === 'current'">Continue</button>
         <button mat-stroked-button color="warn" (click)="discontinueClick(item)"
           [disabled]="item?.medicationStatus?.toLowerCase() === 'discontinued'">Discontinue</button>
          <button mat-stroked-button color="accent" (click)="modifyClick(item)">Modify</button>
			
```
### Realtime Example 2

``` title="html"
// here medstatus='current' vunte continue btn ravali else dis-continue btn

  <button mat-raised-button color="primary" *ngIf="item.medicationStatus" class="mr-2"
     [ngClass]="item.medicationStatus === 'Current' ? 
     'continue-button' : item.medicationStatus === 'Discontinued' ? 'discontinue-button' : ''">
      {{ item.medicationStatus }}
   </button>

	---STYLE.SCSS--			  
 .continue-button {
    background-color: #c8e6c9 !important;
    color: #256029 !important;          
  }
  
  .discontinue-button {
    background-color: #ffcdd2 !important; 
    color: #b71c1c !important;           
  }
  .success-button {
    border-color: #4caf50 !important; 
    color: #4caf50 !important;
  }
```

```
 //here medStatus='current' (or) medstatus='ordered' vuna gani 'continue-button' ravali else discontinue
    <button mat-stroked-button class="mr-2"
      [ngClass]=" (item.medicationStatus === 'Current' || item.medicationStatus === 'Ordered') 
        ? 'continue-button':item.medicationStatus === 'Discontinued' ? 'discontinue-button': ''">
           {{ item?.medicationStatus }}
    </button>
```


### ClassBinding  => syntax:[class]="isAcive"
``` title="ts file"
  isAcive:boolean=false;  //variable:type=value
```
``` title="html"

<h1 [class]="isAcive? 'redColor' : 'blueColor'"> isAcive</h1>
Note: condition true aite redColor false aite blueColor

      ----scss file---
   .redColor{ background-color: red; }

   .blueColor{background-color: blueviolet;}
```
### ex:2 TO apply multiple styles we use [ngClass]
``` title="ts.file"
import { NgClass } from '@angular/common'; //import ngClass

   public required = true;

  public get Group() {
    return {
      TextColor: this.required,
      TextSize: this.required,
      TextStyle: this.required
    };
  }
```
``` title="html.file"  
 <!-- Multi-class binding -->
<h2 [ngClass]="Group">MultiStyles</h2>

   --- css ---
.TextColor {
  color: green;
}

.TextSize {
  font-size: 60px;
}

.TextStyle {
  font-style: italic;
}
```

## -----Style binding-----

```
    2ways ga use ceyachu
i) Inline styleBinding anedi dynamic CSS apply ceyadaniku use avtundi
   syntax: 1.[style.property]=variable
           2.[style]={property:variable}  (or)

ii) General ga manam-Inline style ni yela use chestam ante 
    <h1 style="color:red">Static InlineStyle</h1>

 dynamic css apply cheyali ante tsFile lo variable declare cheskoni chestam
 
--- ts.File ----
 cvar:string:'red'
--- html ----
 <h1 [style.color]="cvar">DynamicColor</h1> //style.color=variableName 
```

## Apply multipleStyle using style
 
``` title="ts.file"
 myStyle:object={
 color:'whit',
 background-color:'blue',
 border:'5px solid pink
 }
 
 --- html ---
 <h1 [style]="myStyle"> multipleStyle</h1> //[style]=propertyName
 
 
 
```
 ## multiple styles using [ngStyle]

 ``` title="ts.file"
  object type lo group ga raskovachu
  public myStyle={  
    color:'green',
    fontStyle:'italic',
    fontSize:'50px'
  }; //this is in objectType

  ---html.file---
  <h2 [ngStyle]="required?'green':'red'> RAJESH </h2>
 ```