# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_not_at_work.csv - Šeimos daktaro nebuvimo darbe periodas
* [InstitutionCode]_family_doctors_list.csv - Įstaigos šeimos daktarų sąrašas
* [InstitutionCode]_free_registrations.csv - Laisvo registracijos pas šeimos gydytoją (sugeneruotas priėmimo grafikas)

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

If you change only files recomended
```sh
$ git add [InstitutionCode]_doctors_not_at_work.csv
$ git add [InstitutionCode]_family_doctors_list.csv 
$ git add [InstitutionCode]_free_registrations.csv
```
4.	Record changes to the repository
```sh
$ git commit -m 'institution name automatic update' 
```

5.	Atnaujinti duomenys repo
```sh
$ git push --all arba origin master
```

