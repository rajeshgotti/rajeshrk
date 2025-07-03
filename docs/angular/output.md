---
hide:

  - toc
---
## @Output is used to send data from Child to Parent

```
-> child nundi data ni parent ki send ceyadanki manaki 3 ways vuani
   1. @Output Decorator  2. Template ReferenceVariable(#) 3.@ViewChild
->  @Output gurinchi teliyali ante inko 2 terms teliyali 
   1. EventEmitter  2. EventBinding
```

```
Step:1 import @Output & EventEmitter in ChildComponent
         ex: {import Output,EventEmitter } from 'angular/core'
Step:2 create constructor in your child component 
         ex: @Output variable=new EventEmitter();
Step:3 e event emitter lo manaki emit() ane oka method vuntundi.danni e variable tho access chekovachu 
         ex: let obj=new obj(); obj.m1() (or) obj.m2()
       same elane variable.emit() ani use chestam so e emit method lopala edite 
       manam pass chestamo ha emit aina data ni parentComp.html lo use cheskovali            
```
### Example

``` title="child.ts"
import { Output, EventEmitter } from '@angular/core';
  @Output() eventName = new EventEmitter<any>();

  msg="pass to parent"; //your data

    passToParent(){
       this.eventName.emit(this.msg);
    }

    ---html--- 
in html file write one clickEvent to hit above method

<button (click)="passToParent()">Send</button> 
```

```title="parent.ts"

myData:any;

 ---html---
 <app-child
   myData=$event
 ></app-child>
 <h1>{{myData}}</h1>
 
```
 ###  RealTime Ex: 
``` title="AddressComp.ts" 
   ---- [ChildComponent.ts] ----
import { Output } from '@angular/core';

@Output() formAddressReady: EventEmitter<UntypedFormGroup> = new EventEmitter<UntypedFormGroup>();

   ngOnInit() {
    this.formAddressReady.emit(this.addressForm);
    }

    --- Address.component.html ---

<form [formGroup]="addressForm">
    <input type="text" formControlName="name" />
</form>

```
  ###   [Parent]
``` title="add-location.ts" 

import AddressComp from './addressComp.ts';

addAddressFormControl(name: string, form: UntypedFormGroup): void {
    this.locationForm.addControl(name, form);
}

add-location.html
<app-address (formAddressReady)="addAddressFormControl('addressForm', $event)">
  </app-address>
```
## Realtime ex:
``` 
    --PresentMedicationComponent1.ts--
 @Output() saveEvent=new EventEmitter(); // child-parent

 this.historyService.addPresentMedicationHistory(forms).pipe(takeUntil(this.onDestroy$)).subscribe(res => {
        if(res.status==200)
        {
          this.clearStatus=true;
         this.saveEvent.emit(true)	; //this save we are emmiting
        }})

     ---MedicationsReconciliationComponent.ts--		
		 
 addHomeMedication(event){
  
      const dialogRef=this.dialog.open(PresentMedicationComponent1,{
       
        width:'60%',
        height:'45%',
        data:{event,
          type:'add-home-medication',
        },
        disableClose: true,
      })
      dialogRef.componentInstance.saveEvent.pipe(takeUntil(this.onDestroy$)).subscribe({ //here we are using that emited data
        next: (res) => {
          this.getHomeMedications();
        }
      });		
 }
```
