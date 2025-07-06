---
hide:
 - toc
---


```title="ts.file"
step:1 import matdilog
import { MatDialog, MatDialogRef } from '@angular/material/dialog';						  
 
step:2 use in constructor 
constructor(public dialogRef:MatDialogRef<any>,private dialog:MatDialog);

step:3 add oneMethod and inside it use it using thisKEYWORD
 addMedicationsFrom(medicationObj){
    const matDialog = this.dialog.open(MedicationEntryPopupComponent,{
      width:'80%',
      height:'80%',
      data: {
        medicationRowId: 0 ,
        actionType: 'Add',
        medicationType: 'Current',
        isShowMedicationTypeField: false,
        isClosed: true,
        medicationObj: medicationObj,
        // isPatchCurrentStartDate: isPatchCurrentStartDate,
      },
      disableClose: true
    })
    matDialog.componentInstance.getSavedMedications.subscribe({
      next:(res)=>{
      this.getCurrentMedicationData();
      },error:(err)=>{
        console.log(err,'Error ')
      }
    })
  }		

```