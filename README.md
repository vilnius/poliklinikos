# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_not_at_work.csv - Įstaigos šeimos daktarų sąrašas 
* [InstitutionCode]_family_doctors_list.csv - Laisvo registracijos pas šeimos gydytoją – sugeneruotas priėmimo grafikas
* [InstitutionCode]_free_registrations.csv - Šeimos daktaro nebuvimo darbe periodas 

## Konfiguruojamas kontroles interaktyvi lenta (test version)
[https://app.powerbi.com](https://app.powerbi.com/view?r=eyJrIjoiYjYyODQ3NDYtOGFlNS00YWE5LWIxMTktNTA3ZjRhNzgwNmM5IiwidCI6ImFmZjM2MzMxLTNlNWUtNDdlOC1hZjkzLTE4NTFkNmQxZmUzYiIsImMiOjh9)

## Poliklininikoms:
Install GIT
Clone repo (only first time) 
```sh
$ git clone https://github.com/vilnius/poliklinikos.git
```

### Atnaujinimo procedūra
1.	Update data from repo 
```sh
$ git pull origin master arba git pull –all
```
2.	Run script, which create and update *.csv files
```sh
[InstitutionCode]_doctors_not_at_work.csv
[InstitutionCode]_family_doctors_list.csv 
[InstitutionCode]_free_registrations.csv
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

