---
hide:
 - toc
---


```
import { MatDialog, MatDialogRef } from '@angular/material/dialog';						  
 
constructor(public dialogRef:MatDialogRef<any>,private dialog:MatDialog);

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