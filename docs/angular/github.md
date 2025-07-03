---
hide:
 - toc
---
```
git pull origin Dev_NG_18_Feature  --- this is for falcon-patient
git pull origin Dev-18  --this is for patient_portal

  set NODE_OPTIONS=--max_old_space_size=8192
 ---- git commands ---
 1.write msg in msg box 
 2.click on + symbol and dont click on commit just type cmd as 
 3. git stash save "rajesh"
 4. after that take git pull origin Dev_NG_18_Feature
 5.git stash apply stash@{0}--- here the data will come which will be selected 
-> git stash list ---- here the save list will come 
-> git pull origin Dev_NG_18_Feature (or) if ur in patient_portal then: git pull orign Dev-18
-> git stash drop stash@{0} -- to delete the perticular index data 
-> git stash clear -- to clear complete saved stash   
```