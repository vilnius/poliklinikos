# Public health data test

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_not_at_work.csv - Įstaigos šeimos daktarų sąrašas 
* [InstitutionCode]_family_doctors_list.csv - Laisvo registracijos pas šeimos gydytoją – sugeneruotas priėmimo grafikas
* [InstitutionCode]_free_registration.csv - Šeimos daktaro nebuvimo darbe periodas 


## Poliklininikoms:
Install GIT
Clone repo (only first time) 
```sh
$ git clone https://github.com/vilnius/poliklinikos.git
```

### Atnaujinimo procedūra
1.	Atnaujinti duomenis kataloge iš repo 
```sh
$ git pull origin master arba git pull –all
```
2.	Paleisti skriptą, kuris atnaujina *.csv failus
```sh
$ git Select Data
```
3. Add file contents to the index
```sh
$ git add . arba git add –all
```
4.	Record changes to the repository
```sh
$ git commit -m 'institution name automatic update' 
```

5.	Atnaujinti duomenys repo
```sh
$ git push --all arba origin master
```
