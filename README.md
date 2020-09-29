# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_excluded.csv - nevertinamų šeimos gydytojų (vidaus ligų, vaikų ligų) gydytojų (toliau - ŠG) sąrašas (nebuvimo darbe periodas: ŠG atostogos, laikinas nedarbingumas, kvalifikacijos tobulinimas)
| Laukas | Tipas | Pastabos |
| ------ | ----- | ---- |
| Įstaigos kodas | Bigint | |
| Gydytojo_id | Bigint | |
| Data nuo | Date | | 
| Data iki | Date | |
| Įrašo sukūrimo data |	Timestamp | |

* [InstitutionCode]_family_doctors_list.csv - Įstaigos ŠG sąrašas  (dalyvaujančių finansavimo programoje)
| Laukas | Tipas | Pastabos |
| ------ | ----- | ---- |
| Įstaigos kodas | Bigint | |
| Gydytojo_id | Bigint | |
| Įrašo sukūrimo data |	Timestamp | |
| Apylinkės tipas | Int | |
| Etatinis darbo krūvis | Double | įformintas darbo krūvis ataskaitinio laikotarpio 1 dieną |

* [InstitutionCode]_free_registrations.csv - Laisvos registracijos pirminiam vizitui pas ŠG, dalyvaujančių finansavimo programoje, priemimo grafikas (sugeneruotas priėmimo grafikas 30 k. d. į priekį neįskaitant pateikimo dienos)
| Laukas | Tipas | Pastabos |
| ------ | ----- | ---- |
| Įstaigos kodas | Bigint | |
| Gydytojo_id | Bigint | |
| Laisvos registracijos data| Timestamp | |
| Įrašo sukūrimo data |	Timestamp | |

* [InstitutionCode]_family_doctors_patients.csv - Duomenys teikiami pasibaigus ataskaitiniam laikotarpiui, t.y. einamojo laikotarpio pradžioje ne vėliau kaip iki 10 einamojo laikotarpio kalendorinės dienos
| Laukas | Tipas | Pastabos |
| ------ | ----- | ---- |
| Įstaigos kodas | Bigint | |
| Ataskaitinio laikotarpio pradžia | Date | |
| Ataskaitinio laikotarpio pabaiga | Date | |
| Gydytojo ID | Bigint | |
| Prisirašiusių prie gydytojo gyventojų skaičius | Int | prisirašiusių  privalomuoju sveikatos draudimu draustų gyventojų skaičius paskutinę dieną prieš ataskaitinio laikotarpio pirmo mėn. 1 d. (jeigu pavaduojant ilgalaikėse atostogose esantį gydytoją pacientai yra perskirstyti konkretiems gydytojams, tai jie priskiriami prisirašiusiems; jei pavadavimas trumpalaikis (atostogos, liga), arba jei pavaduoja bet kurie gydytojai, t.y. gyventojai nepriskirti konkretiems gydytojams, tuomet teikiamas tik prie to gydytojo prisirašiusių privalomuoju sveikatos draudimu draustų pacientų skaičius)  |
| Gydytojo viso ataskaitinio laikotarpio darbo valandų kiekis viso | Double | |
| Įrašo sukūrimo data |	Timestamp | |

* [InstitutionCode]_family_doctors_visits_hours (teikiama kiekvieną dieną už praėjusią dieną)
| Laukas | Tipas | Pastabos |
| ------ | ----- | ---- |
| Įstaigos kodas | Bigint | |
| Data | Date | |
| Gydytojo ID | Bigint | |
| Pirminių vizitų trukmė sveikatos įstaigoje minutėmis  | Int | tiesioginio kontakto ir nuotolinės konsultacijos |
| Priimtų pacientų pirminiams vizitams*** skaičius | Int | |
| Pirminių ir kitų (kartotinių) vizitų trukmė sveikatos įstaigoje trukmė minutėmis | Int | visų vizitų trukmė pagal darbo grafiką (įeina visi vizitai, taip pat ir nuotolinės konsultacijos be dokumentų tvarkymo, pertraukų laiko, papildomų laikų ir pan.) |
| Viso priimtų pacientų skaičius | Int | |
| Darbo laikas nuo | String | |
| Darbo laikas iki | String | |
| Įrašo sukūrimo data | Timestamp | |



Pastaba. Neturint Programinės įrangos iš kur paimti duomenis, juos suvesti rankiniu būdu pagal pateiktą formatą: https://github.com/vilnius/poliklinikos/tree/master/data/Template%20for%20doctos%20visits%20data

## Konfigūruojama interaktyvi lenta
[https://app.powerbi.com](https://app.powerbi.com/view?r=eyJrIjoiYzdkMTkzMzYtZDllZi00MjkxLTg3ZmItOTJkMTMyZDdmMWE3IiwidCI6ImFmZjM2MzMxLTNlNWUtNDdlOC1hZjkzLTE4NTFkNmQxZmUzYiIsImMiOjh9)

## Algoritmas
1) Kiekvienos kalendorinės dienos 6 val. ryte daromas duomenų atrinkimas skaičiavimams. 
2) Pasiimamas Šeimos gydytojo institucijos finansavimo programoje dalyvaujančių šeimos (vidaus ligų, vaikų ligų) ŠG sąrašas (family_doctors_list.csv).
3) Patikrinama, ar visi ŠG turi laisvų laikų „Laisvos registracijos pirminiam vizitui pas ŠG“ (free_registrations.csv) duomenų rinkinyje.
4) Jei ŠG neturi laisvų laikų, tuomet patikriname ar jis yra darbe „nevertinamų ŠG sąraše“ „(doctors_not_at_work.csv) „(_doctors_excluded.csv duomenų rinkinyje)“:
a) Jei ŠG tikrinimo periode yra nevertinamų ŠG sąrašo duomenų rinkinyje patikrinimo rezultatų lentelėje pažymimas atitinkamas požymis;
b) Jei ŠG nėra nevertinamų ŠG sąrašo duomenų rinkinyje tikrintam periodui, tuomet tikrinimo datai patikrinimo rezultatų lentelėje prie ŠG įrašomas požymis „Ne“ (neatitinka tvarkos aprašo punkto reikalavimo);
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

