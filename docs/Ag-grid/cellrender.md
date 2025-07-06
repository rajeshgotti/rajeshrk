---
hide:
 - toc
---
``` title="ts.file"
        {
            headerName: 'Copy To IP',
            field: 'CopyToIP',
            cellRenderer: () => {
            const icon = document.createElement('i');
            icon.className = 'fa fa-copy';
            icon.style.cursor = 'pointer';
            icon.style.color = 'black';
            return icon;
            },
          onCellClicked: (params) => {
            this.addMedicationsFrom(); //method
          }
        }
		----------
  addMedicationsFrom(medicationObj = null, isPatchCurrentStartDate: boolean = false){
      const matDialog = this.dialog.open(MedicationEntryPopupComponent,{
        width:'80%',
        height:'80%',
        data: {
          // type: 'from pharmacist',
          medicationRowId: 0 ,
          actionType: 'Add',
          medicationType: 'Current',
          isShowMedicationTypeField: false,
          isClosed: true,
          medicationObj: medicationObj,
          isPatchCurrentStartDate: isPatchCurrentStartDate
        },
        disableClose: true
      })
  
      matDialog.componentInstance.getSavedMedications.subscribe((res) => {
       console.log(res)
        
      }, (error) => {
      });
    }	
```
### onClick()
``` title="ts.file"
    {
        field: 'edit', headerName: 'Actions', headerTooltip: 'Edit', minWidth: 120,width:100,
          pinned:'right', filter: false,
        cellRenderer: params => {
          if (params.data) {
          const iconsHTML = 
                 <span class="d-flex" title="Edit">
                    <i class="fas fa-pen"></i>
                 </span>
                 <span class="d-flex" title="Delete">
                    <i class="far fa-trash-alt fa-icon-del-col"></i>
                 </span> ;
            const htmlContent = <div class="f-icon-div">
                                  ${iconsHTML}
                                </div>;
              return htmlContent;
          }
          return null;
      },
      
      onCellClicked: (params) => {
         // console.log(params)
        const clicked = params.event.target ;
         var element = clicked as HTMLElement;
         var className = element.className.toString();
           if (className==='fas fa-pen') {
             this.addNewNursingStation(params.data)
             }else if(className==='far fa-trash-alt fa-icon-del-col') {
              this.deleteNursingtation(params.data)
           }
         }
       }
```