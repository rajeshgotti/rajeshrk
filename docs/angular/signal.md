---
hide:
 - toc
---
``` title="LocalDataSourceService.ts"
 in this service class create your signal y to create in service file only means if u create in 
 service then only one object will be created 
	

step:1 export class LocalDataSourceService {
		currentMedSignal=signal<any>(null); //creating signal
		currentMedData(data: any) {
			this.currentMedSignal.set(data);
			}	
			}
Step:2  a component lo data manaki kavlao a comp.ts file ki velli  ex:
     constructro(private localDataService:LocalDataSourceService){}
		currentMedications:any;
		getCurrentMedicationData() {
			this.linkedMedications.getCurrentMedications(this.patientId).subscribe(res => {
      this.currentMedications = res.body;
      this.localdataService.currentMedData(this.currentMedications);//so here manki res.body lo 
	  vachina data ni signal lo petam 
	  }
	  }
Step:3   in which componet you want in that ts file inside constuctor u have to write
		constructro(private localDataService:LocalDataSourceService){
			effect(() => {
			let transmitData=this.localdataService.currentMedSignal()
				console.log(transmitData,'data using signal'); //here u will get data that ur can use 
				were u want in this compont
       }) 
  }	  

```