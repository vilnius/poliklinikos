# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_excluded.csv - nevertinamu šeimos gydytojų (toliau - ŠG) sąrašas (nebuvimo darbe periodas, atostogos arba pavadavimas kito daktaro)
* [InstitutionCode]_family_doctors_list.csv - Įstaigos gydytojų sąrašas  (dalyvaujančių finansavimo programoje)
* [InstitutionCode]_free_registrations.csv - Laisvo registracijos pas šeimos gydytoją, dalyvaujančių finansavimo programoje, priemimo grafikas (sugeneruotas priėmimo grafikas 30 k. d. į priekį neįskaitant pateikimo dienos)

Pastaba. Neturint Programinės įrangos iš kur paimti duomenis, juos suvesti rankiniu būdu pagal pateiktą formatą: https://github.com/vilnius/poliklinikos/tree/master/data/Template%20for%20doctos%20visits%20data

## Konfiguruojamas kontroles interaktyvi lenta
[https://app.powerbi.com](https://app.powerbi.com/view?r=eyJrIjoiYzdkMTkzMzYtZDllZi00MjkxLTg3ZmItOTJkMTMyZDdmMWE3IiwidCI6ImFmZjM2MzMxLTNlNWUtNDdlOC1hZjkzLTE4NTFkNmQxZmUzYiIsImMiOjh9)

## Algoritmas
1) Kiekvieną naktį daromas duomenų atrinkimas skaičiavimams (6 val. ryte). 
2) Pasiimamas Šeimos gydytojo institucijos finansavimo programoje dalyvaujančių šeimos (vidaus ligų, vaikų ligų) gydytojų sąrašas (family_doctors_list.csv).
3) Patikrinama, ar visi ŠG turi laisvų laikų „Laisvos registracijos pirminiam vizitui pas ŠG“ (free_registrations.csv) duomenų rinkinyje.
4) Jei ŠG neturi laisvų laikų, tuomet patikriname ar jis yra darbe „nedarbo periodai“ (doctors_not_at_work.csv) duomenų rinkinyje.
a) Jei ŠG tikrinimo periode yra nedarbo periodo duomenų rinkinyje patikrinimo rezultatų lentelėje pažymimas atitinkamas požymis;
b) Jei ŠG nėra nedarbo periodo duomenų rinkinyje tikrintam periodui, tuomet tikrinimo datai patikrinimo rezultatų lentelėje prie ŠG įrašomas požymis „Ne“ (neatitinka tvarkos aprašo punkto reikalavimo);
c) Jei ŠG turi laisvų laikų pirminiam vizitui, vykdomas 5 žingsnis. 
5) Toliau tikrinami visi laikai „Laisvos registracijos pirminiam vizitui pas ŠG“ duomenų rinkinyje. Nustatoma kiekvieno ŠG artimiausia data, kada jis gali priimti pacientą.
6) Jei nustatyta artimiausia datos ir patikrinimo datos skirtumas yra mažiau arba lygu 7 kalendorinėm dienom, tuomet tikrinimo datai patikrinimo rezultatų lentelėje prie ŠG įrašomas požymis „Taip“. Jei datos skirtumas yra daugiau nei 7 kalendorinės dienos, įrašoma „Ne“. 
Skaičiuojama kiekvieną kalendorinę dieną.

## Poliklininikoms:
Susikuria github.com paskyra pavadinimu "antakalnio-poliklinika" 

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
[InstitutionCode]_doctors_excluded.csv
[InstitutionCode]_family_doctors_list.csv 
[InstitutionCode]_free_registrations.csv
```
3. Add file contents to the index

If you change only files recomended
```sh
$ git add [InstitutionCode]_doctors_excluded.csv
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

