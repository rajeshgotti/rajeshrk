---
hide:
 - toc
---

```title="html.file"

<hello name="{{ name }}"></hello>
<p>
  Start editing to see some magic happen 
</p>
<div [formGroup]="orderForm">
<div formArrayName="items"
  *ngFor="let item of orderForm.get('items').controls; let i = index;">
  <div [formGroupName]="i">
    <input formControlName="name" placeholder="Item name">
    <input formControlName="description" placeholder="Item description">
    <input formControlName="price" placeholder="Item price">
  </div>

  Chosen name: {{ orderForm.controls.items.controls[i].controls.name.value }}
</div>
</div>
<button (click)="addItem()">Add</button>

```

``` title="ts.file"
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, FormArray, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent  {
  orderForm: FormGroup;
items: FormArray;

constructor(private formBuilder: FormBuilder) {}

ngOnInit() {
  this.orderForm = new FormGroup({
    items: new FormArray([])
  });
}

createItem(): FormGroup {
  return this.formBuilder.group({
    name: '',
    description: '',
    price: ''
  });
}

addItem(): void {
  this.items = this.orderForm.get('items') as FormArray;
  this.items.push(this.createItem());
}
}
```
<details>
  <summary>FormArray Using ForEach()</summary>
  <img src="images/formArray.png" alt="Output image" style="max-width: 100%; height: auto;" />
</details>

<!-- <details>
  <summary>RealTime Notes</summary>
  <img src="images/formArray.png" alt="Output image" style="max-width: 100%; height: auto;" /> -->
</details>

### RealTimeEx

``` title="html.file"
Note: first we need to write the formgroup, formarrayName,formgroupname in that controlers

<form [formGroup]="formArray" class="custom-form" (ngSubmit)="onSubmit()">
  <h4 class="form-title">User Information</h4>

  <div formArrayName="userDetails" *ngFor="let user of userDetails.controls; let i = index">
    <div [formGroupName]="i" class="form-group">

      <!-- Firstname -->
      <label for="firstname">First Name</label>
      <input type="text" formControlName="firstname" placeholder="Enter first name">

      <!-- Lastname -->
      <label for="lastname">Last Name</label>
      <input type="text" formControlName="lastname" placeholder="Enter last name">

      <!-- Gender -->
      <label>Gender</label>
      <div class="radio-group">
        <label for="genderMale">
          <input type="radio" formControlName="gender" value="Male" id="genderMale"> Male
        </label>
        <label for="genderFemale">
          <input type="radio" formControlName="gender" value="Female" id="genderFemale"> Female
        </label>
      </div>

      <!-- Message -->
      <label for="textme">Message</label>
      <textarea formControlName="textme" placeholder="Enter your message" rows="5"></textarea>

      <!-- Preferences -->
      <label>Preferences</label>
      <div class="checkbox-group">
        <label for="checkYes">
          <input type="checkbox" formControlName="yes" id="checkYes"> Yes
        </label>
        <label for="checkNo">
          <input type="checkbox" formControlName="no" id="checkNo"> No
        </label>
      </div>

      <!-- Remove Button for this form group -->
      <button type="button" (click)="removeUser(i)">Remove</button>
    </div>
  </div>

  <button type="button" (click)="addUser()">Add User</button>
  <button type="submit" class="submit-btn">Submit</button>
</form>


```
### after completing the form array in the html 
``` title="ts.file"
step 1 - 

     ngOnInit(): void {
        this.formarray()
      }

        formarray(){
            this.formArray = this.fb.group({
                userDetails: this.fb.array([this.createUser()])
          });
        }(formarray is the group ) it is creating intially -- by using this method (this.creatUser())


        createUser(): FormGroup {
        return this.fb.group({
            firstname: [''],
            lastname: [''],
            gender: [''],
            textme: [''],
            yes: [false],
            no: [false],
        });
        }
step 2 - add button 
        get userDetails() {
       return (this.formArray.get('userDetails') as FormArray);
       } 

    //adding the controllers 

        addUser(){
        this.userDetails.push(this.createUser());
        }

        this.creatUser is added sucessfully and used 

        // remove form array 
        removeUser(index: number) {
        this.userDetails.removeAt(index);
        }

step 3 post --

    this.userDetails.controls.forEach(control => {
      const formData = this.extractFormData(control);
      formarradtaa.push(formData);
    });

      private extractFormData(control: AbstractControl): any {
    return {
      firstname: control.get('firstname')?.value,
      lastname: control.get('lastname')?.value,
      gender: control.get('gender')?.value,
      checkboxYes: control.get('yes')?.value,
      checkboxNo: control.get('no')?.value,
    };
  }
//  here the data is pushed as per the loop 
 
step 4 get and patch 
    patchValue() {
    // Iterate over each object in getdata
    this.getdata.forEach((data, index) => {
      // Get the specific FormGroup from the FormArray by index
      const formGroup = this.userDetails.at(index) as FormGroup;

      // Patch values into the FormGroup
      formGroup.patchValue({
        firstname: data.firstname,
        lastname: data.lastname,
        gender: data.gender,
        yes: data.checkboxYes,
        no: data.checkboxNo,
      });
    });
  }




```