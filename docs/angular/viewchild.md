---
hide:
 - toc
---


<details>
  <summary>Click to expand image</summary>
  <img src="/images/viewChild2.jpg" alt="Output image" style="max-width: 100%; height: auto;" />
</details>
<details>
  <summary>Click to expand image</summary>
  <img src="/images/viewChild.jpg" alt="Output image" style="max-width: 100%; height: auto;" />
</details>


```
@ViewChild  
→ child నుండి parent కి data transfer చేయాలంటే 3 ways ఉన్నాయి  
     1: @Output  2: viewchild() & 3: TempRefVariable

→ step 1: @ViewChild of Reference code ని మనం Angular/core నుండి import చేయాలి  
    ex: import { ViewChild } from '@angular/core'

→ ఇది మనం parent component.ts file lo importt చేయాల్సి vuntundi  bz manam [ C-P ] data send chestundan
    so.Parent component lo child data use cheskovali ankuntunam 
    so import in parent comp

→ a component ni use cheskovali ankuntunamo danni import cheyali   
    ex: import { HomeComp } from './comp/home.component';

→ §II: in general మనం oka value ని variable లో  yela store చేస్తాం  
    int x=10; x is a variable that we can use anywhere  
    @ViewChild(HomeComp) variable: string; //so e variable ni use chesi manam childComp lo vunna anni varibles/methods ni access cheskovachu

→ Note: a component lo aite manam <app-comp> ani istamo adi ChildCompoent  
   
   ex: <app-child></app-child> → child

----- head.ts file ---  [C-P] @ViewChild
    //this is child component.ts

  data = 'Hello';
    passToParent() {
       return this.data;
         }
----app.comp.ts -- ParentComponent
→ app.comp.ts → parent

    import { ViewChild } from '@angular/core'
    import { HeaderComp } from './header.component'

    @ViewChild(HeaderComp) header: any;

    test() {
        console.log(this.header.passToParent);
     }

→ app.html [parentHtml]
    <app-header></app-header>    ← child comp
    <button (click)="test()">Send</button>
```