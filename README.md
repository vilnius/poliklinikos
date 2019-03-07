# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_not_at_work.csv - Įstaigos šeimos daktarų sąrašas 
* [InstitutionCode]_family_doctors_list.csv - Laisvo registracijos pas šeimos gydytoją – sugeneruotas priėmimo grafikas
* [InstitutionCode]_free_registration.csv - Šeimos daktaro nebuvimo darbe periodas 


## poliklininikoms:
1.	Install GIT
2.	Clone repo (only first time) 
```sh
$ clone https://github.com/vilnius/poliklinikos.git
```
3.	Atnaujinti duomenis kataloge iš repo 
```sh
$ git pull origin master arba git pull –all
```
4.	Paleisti skriptą, kuris atnaujina *.csv failus
```sh
$ git Select Data
```
5. Add file contents to the index
```sh
$ git add . arba git add –all
```
6.	Record changes to the repository
```sh
$ git commt -m 'institution name automatic update' 
```

7.	Atnaujinti duomenys repo
```sh
$ git push --all arba origin master
```
