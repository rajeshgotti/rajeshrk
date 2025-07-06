---
hide:
 - toc
---
```
---swal .fire--
STEP:1 SWAL & SNACKBAR 
import Swal from 'sweetalert2';
import { MatSnackBar } from '@angular/material/snack-bar';

step:2 use SnackBar in Constructor with private
constructor(private snackbar:MatSnackBar);

step:3 take one method here write code if result is success then res.value else to elsePart
 discontinueClick(item: any) {
    this.medStatus='D';
    Swal.fire({
      title: 'Are you sure want to Discontinue?',
      icon: 'warning',
      allowOutsideClick:false,
      showCancelButton: true,
      confirmButtonText: 'Yes, Discontinue it!',
      cancelButtonText: 'No, keep it'
    }).then((result) => {
      if (result.value) {
        this.erdashboard.createpresentMedicationStatus(item?.medicationRowId ,
        this.patientId,this.visitId,this.medStatus, item?.eventId).pipe(takeUntil(this.onDestroy$)).subscribe({
          next:(res)=>{
           this.getHomeMedications(); //your get method
          },error:(err)=>{
            console.log(err,'Error ')
          }
        })
          this.status = true;
 
      } else if (result.dismiss === Swal.DismissReason.cancel) {
        this.snackbar.open('Your record safe !','Ok',{  //snack-bar
          duration:2000
        })
  
      }
    })
 
  }

```