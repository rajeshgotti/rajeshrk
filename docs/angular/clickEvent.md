---
hide:

  - toc
---
```
 01: ngModelChange()  ==> (ngModelChange)="onChange($event)"
 02: mat-autoComplete ==> (optionSelected)="selectedData($event)"
 03: mat-select       ==> (selectionChange)="demo()"
 04: ng-Select        ==> (change)="demo()"
 05: date change      ==> (dateChange)="onFromDateToDateChange($event)
 06: input
 07: focus()
 08: blur()
 09: keyup()
 10: keydown()
 11: keypress()
 
```

### 01: ngModelChange()

``` title="html.file"
   
 <input matInput formControlName="fm" (ngModelChange)="onChange($event)">
    
    ---ts.file--
 onChange(e):void{
    ---
    ---
 }
```
### RealTime Ex:   ngModelChange="onChange(event)"
```
## Syntax : <input [(ngModel)]="yourVariable" (ngModelChange)="onChange($event)" />
```
``` title="html.file"
 Ex:1
  <input [(ngModel)]="username" (ngModelChange)="onUsernameChange($event)" placeholder="Enter username" />
			<p>You typed: {{ username }}</p>

```
``` title="ts.file"
 
 export class AppComponent {
  username = '';

  onUsernameChange(value: string) {
    console.log('Username changed to:', value);
    // You can do anything here, like validation, API call, etc.
  }}

```
### RealTime Ex:2

``` title="html.file"
<mat-form-field class="example-full-width" appearance="outline">
    <mat-label>Edu Date</mat-label>
       <input matInput  matTooltip="MM/dd/yyyy" appMaskDate [type]="'datetime'"
          [max]="ToDayDate" [owlDateTime]="time1" formControlName="edudate" 
          (ngModelChange)="onChange($event,'S')" placeholder="Edu Date">
       <mat-icon matSuffix [owlDateTimeTrigger]="time1" class="date-icon">schedule</mat-icon>
          <owl-date-time #time1></owl-date-time>
</mat-form-field>
  
```
``` title="ts.file"
  onChange(event: any, type) {
    // console.log("change event",event)
    if (type == "P") {
      let sDate = this.amendmentForm.get('requestedDate').value;
      // console.log("dropdown select", event, sDate)
    }
    else {
      let sDate = this.amendmentForm.get('requestedDate').value;
      // console.log("dropdown select", event, sDate)
      //   console.log("dropdown select", event, sDate)
    }					
  }


```
### RealTime Ex:3
``` title="html.file"
<ng-container>
   <div class="icu-element-focus-control">
     <div *ngIf="vital?.element?.controlData?.length>0">
      <select *ngIf="vital?.element?.controlData[0]?.heartRhythm?.length>0"
        placeholder="Rhythm " class="icu-element-focus" [(ngModel)]="vital[header.value].rhytham"
          (ngModelChange)="onChange1(header?.value,icuIndex,index,item.componentName,item)">
         <option *ngFor="let item1 of vital?.element?.controlData[0]?.heartRhythm;trackBy: trackByFn"
            [value]="item1.heartRhythmID">
              <!-- <input type="checkbox"> -->
         </option>
       </select>
      </div>
   </div>
</ng-container>
```
``` title="ts.file"
 onChange12(vitalUnitId,icuIndex,index,item,vitalSignDate,data){
    if(item.value&&item.unitId){
   let convertedValue=null;}	 
 }
```


### 02:mat-autoComplete

<details>
  <summary>Click to expand image</summary>
  <img src="images/autocomplete.png" alt="Output image" style="max-width: 100%; height: auto;" />
</details>

``` title="html.file"
<mat-autoComplete (optionSelected)="selectedData($event)">
   <mat-option *ngFor="let item of data" >

   --- ts.file---
  selectedData(event:MatAutoCompleteSelectedEvent){
     ---
     ---
  } 
```
### RealTime Ex: mat-autoComplete (optionSelected)="onchangeSource($event)"
``` title="html.file"
  <mat-form-field appearance="outline" *ngIf="amendmentForm.get('requestType').value != 4">
     <mat-label>Requested By</mat-label>
      <input aria-label="requestedBy" type="text" placeholder="Requested By" 
       (input)="getResquestBy()" matInput formControlName="requestedBy" 
       [matAutocomplete]="auto"> 
   <mat-autocomplete #auto="matAutocomplete" [displayWith]="displayFn" 
          (optionSelected)="onchangeSource($event)">  //this is changeEvent 
      <mat-option *ngFor="let option of options" [value]="option">
                {{option.userName}}
       </mat-option>
    </mat-autocomplete>
 </mat-form-field>							
 
```
``` title="ts.file"
 // here import matAutoComplete,formFileldModule,InputModule
import { MatAutocompleteModule } from '@angular/material/autocomplete';
import { MatFormFieldModule } from '@angular/material/form-field';
import { MatInputModule } from '@angular/material/input';
import { ReactiveFormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common'; 
 
  onchangeSource(event) {   //this is ur method
    // debugger
    this.userName = event.option.value.userName;
    // console.log("########",this.userName);
    if (event?.option.value.userName == this.userName) {
      this.amendmentForm.patchValue({
        userType: event.option.value.roleName,
      })
    }
  }

```
  ### EX:2
```  title="html"
Note: here [displayWith]="anyName" it is used, what to dispaly in the view
                         loop motam lo yem dispaly avvali anedi e [ dispalyWith] lo istam 
 <mat-autocomplete #auto="matAutocomplete" autoActiveFirstOption 
    (optionSelected)="onDrugSelected($event.option.value)" [displayWith]="displayDrugName">
  <mat-option class="custom_line_height_generic" *ngFor="let drug of drugSuggestions" [value]="drug">
    <div class="drug-info-block">
      <div><span class="label-sky">Generic Name :</span> {{ drug.drug }}</div>
       <div style="display: flex; flex-wrap: wrap; gap: 16px;">
        <div><span class="label-red">Brand Name:</span> {{ drug.brandname }}</div>
        <div><span class="label-sky">RxNorm:</span> {{ drug.rxNormCode || 'NONE' }}</div>
        <div><span class="label-red">NDC :</span> {{ drug.ndc || 'NONE' }}</div>
      </div>
    </div>
   <hr>
  </mat-option>
 </mat-autocomplete>


```
``` title="ts.file"
 displayDrugName(drug: any): string {  //this is ur displayWith here we are dispalying drugname
    return drug?.drugname ?? drug ?? ''; 
 }//retung drug ane loop lo vuna drugname ni dispaly chesunam okavela drugname lekunte then ?? 
      ante motam drugObj ne dispaly chestam okavela drugObj null or undefined vunte then '' 
    empty string ni dispaly chestunam
    ----     ---  
   drugSuggestions : any[] = [];

  onDrugNameInput(event: Event): void {
    const inputValue = (event.target as HTMLInputElement).value;
  
    if (inputValue?.length > 2) {
      this.historyService.getWsDrugSuggestions(inputValue, 'DRUG', 'F').pipe(takeUntil(this.onDestroy$))
        .subscribe({
          next: (res: any) => {
            this.drugSuggestions  = res?.body || [];
          },
          error: (err) => {
            console.error('Drug name search error:', err);
            this.drugSuggestions  = [];
          },
        });
      }else {
      this.drugSuggestions  = [];
    }

    if(!this.pharmacyForm.get('drugName').value){
      this.SearchDrugId='0'
    }
  }
  onDrugSelected(event){
    let Data = event 
    this.SearchDrugId= Data?.drugid
   if(Data.drug){
    this.pharmacyService.getDuplicateCheck('Generic',Data?.drug ?? Data,(this.drugLibraryId ?? 0))
    .pipe(takeUntil(this.onDestroy$)).subscribe({
      next:(res)=>{
    if (res && res?.body?.value==="Already Exists" ){
        Swal.fire({
          title: 'Medication Already Present',
          text: 'This medication is already in the list.',
          icon: 'info',
          confirmButtonText: 'OK'
        });
        this.pharmacyForm.reset()
        this.drugSuggestions  = [];
       }
       else {
        // this.pharmacyForm?.reset()
         this.pharmacyForm?.patchValue({
           barndName: Data?.brandname,
           deaClassCode: this.deaClassCodeUnits?.
           find(ele => ele.meD_REF_DEA_CD === numberAttribute(Data?.deaclasscode)) ?? null,
           dosageForm: Data?.dosageform ? numberAttribute(Data?.dosageform) : null,
           rxNormCode: Data?.rxNormCode,
           routeName: this.routes?.find(ele => ele.meD_ROUTE_ID == Data?.route) ?? null,
           ndc: Data?.ndc,
           theraputicCategory: Data?.theraputiccategory,
           drugName:Data?.drug,
           medStrength:Data?.meD_STRENGTH ?? null,
           medUnit:Data?.meD_UNIT ?? null,
           PackageDes:Data?.pd ?? null,
           PackageUnit:Data?.hcfA_UNIT ?? null,
           PackageSize:Data?.ps ?? null,
          })
        }
         this.selectedOptions = [];
      },
     error:(err)=>{
        this.SearchDrugId='0'
      }
    })
  }

  }

```
 ## Ex:3
``` title="html"
<div class="col-12 col-xl-4 col-lg-4 col-md-4 col-sm-6">
  <mat-form-field class="example-full-width" appearance="outline">
     <mat-label>Medicine Name</mat-label>
     <input aria-label="input" type="text" placeholder="Medications" aria-label="Number" 
          matInput required (blur)="onBlur()" formControlName="drug" [matAutocomplete]="auto" >
              <mat-autocomplete   [displayWith]="displayFn" #auto="matAutocomplete"
                (optionSelected)="medicationSelectedEvent($event)" >
                <mat-option  *ngFor="let item of problems" [value]="item" [title]="item.drug">
                  {{item | tallManLettering}} ||
                  {{item?.theraputiccategory}} || {{item?.meD_STRENGTH}} 
                  ({{item?.dataprovider}})
                </mat-option>
              </mat-autocomplete>
              <mat-error *ngIf=" !getdrug().valid &&  (getdrug().dirty || getdrug().touched ||
                isSubmit) " id="validation-dob-error"
                 class="error jquery-validation-error small invalid-feedback">
                 Medications are required
              </mat-error>
  </mat-form-field>
  <span style="color: red" *ngIf="medicationStatusData?.status===true">
     {{medicationStatusData?.message}}
  </span>

```
```title="ts.file"
  displayFn(obj) {  //this is ur displaywith name
    return obj?.drug ? obj?.drug : obj;
  }
---in problems res.body we have data---
  problems: Drug[];
  getProblemSuggestions(value) {
    this.problems = [];
    if (value?.length > 2) {
      // console.log(this.presentMedicationForm.value?.drug)
      // this.historyService.getMedicationsSuggestions(value).pipe(debounceTime(400),takeUntil(this.onDestroy$))
      .subscribe(res => {
        this.historyService.getWsDrugSuggestions(value, 'RxNorm','')
        .pipe(debounceTime(400),takeUntil(this.onDestroy$)).subscribe(res => {   
        this.problems = res.body;
      })
    })
    }
  }

  ------ ----------
  medicationSelectedEvent(event) {
  // console.log(event);
    this.presentMedicationForm.patchValue({
      dosage: this.dosage[0].dosage,
     dosageForm: (this.dosageForms.find(ele => +ele?.meD_DOSAGE_FORM_ID === +event.option.value?.dosageform)?
        .meD_DOSAGE_FORM_DESC),
      route: this.routes.find(ele => +ele?.meD_ROUTE_ID === +event.option.value?.route),
      source: this.medicationSourcess[0].medicationSourceName,
      dosageUnits:event.option.value.dosing_unit,
      rxNormCode:event.option?.value?.rxNormCode,
      dosageQ:event.option?.value?.meD_STRENGTH,
      medUnit:(this.drugMedUnits.find(ele => +ele?.medUnit === +event.option.value?.meD_UNIT))
       ??event.option.value?.meD_UNIT,
    });
    this.medicationsStatus(event?.option?.value?.drugid);
     let routeValue = ((this.presentMedicationForm.get('route')?.value)?.meD_ROUTE_ABBR).trim();
    // console.log(routeValue);
     
    if(((this.presentMedicationForm.get('route')?.value)?.meD_ROUTE_ABBR).trim() === "IV"){
     this.presentMedicationForm.patchValue({
      frequency:this.frequency[0].freq
     })
    }else{
      this.presentMedicationForm.patchValue({
        frequency:this.frequency[1].freq
       })
    }
    this.triggerValidations();
  }


```


### 03: mat-select (selectionChange)="demo()"

``` title="html.file"

<mat-select [ngModel]=" " (selectChange)="onSelectionChange($event)">
  
   ---ts.file--
   onSelectionChange(event){
    ---
    ---
   }
```
### RealTime ex: mat-select (selectionChange)="onMergeChange($event)"

```
 <mat-form-field class="example-full-width" appearance="outline">
    <mat-label>Merge Type</mat-label>
     <mat-select [(ngModel)]="mergeTypeIndex" name="mergeType"
          [disableOptionCentering]="true" (selectionChange)="onMergeChange($event)" >
        <mat-option *ngFor="let list of mergeType" [value]="list.id">
           {{list.field}}
        </mat-option>
     </mat-select>
 </mat-form-field> 
```

### 4: ng-Select (change)="demo()"

``` title="ts.file"
 <ng-select bindValue="" (change)="demo()">
        (Or)
 <raido-button (change)="radioChange()">

  ---ts.file--
 demo(){
    ---
 }          
```
### RealTime Ex: mat-form-field (change)="onChangeName()" 
```title="html.file"
  <div class="mat-form-field-block">
    <ng-select  dropdownPosition="top"  class="ng-select-custom" 
     [items]="sourcerecords" bindLabel="sourceName" bindValue="sourceId" 
     formControlName="requestType" placeholder="Source"  appearance="outline" 
     (change)="onSelectionChange($event);onSelectionChangeData($event)" aria-label="source"
      [inputAttrs]="{ 'placeholder':'','autocomplete': 'off','aria-label':'Request Type',autocorrect':'off' }">
    </ng-select>
  </div>
		---for radioButton--
    <mat-radio-group aria-label="Select an option" (change)="onChangeName()" 
       [(ngModel)]="name" [ngModelOptions]="{standalone: true}">
      <mat-radio-button value="Retail">Retail</mat-radio-button>
		<mat-radio-button value="Other">Other</mat-radio-button>
    </mat-radio-group>
```
### 5 : date change (dateChange)="onFromDateToDateChange($event)
``` title="html.file"
 <mat-form-field appearance="outline" class="example-full-width">
    <mat-label>From Date</mat-label>
     <input matInput [matDatepicker]="fromDatePicker" placeholder="MM/DD/YYYY" [(ngModel)]="fromDate"    
        appMaskDate (dateChange)="onFromDateToDateChange($event)"
         [max]="toDate" />
        <!-- (keyup)="formatDate($event)" -->
       <mat-datepicker-toggle matSuffix [for]="fromDatePicker"></mat-datepicker-toggle>
         <mat-datepicker #fromDatePicker></mat-datepicker>
  </mat-form-field>
            
```
``` title="ts.file"
 
	onFromDateToDateChange(event: MatDatepickerInputEvent<Date, unknown>): void {
    this.getInOrOutPatient();
  }
```