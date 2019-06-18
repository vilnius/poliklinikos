# Public health data

## Duomenų rinkiniai:
* [InstitutionCode]_doctors_excluded.csv - nevertinamų šeimos gydytojų sąrašas (nebuvimo darbe periodas, atostogos arba pavadavimas kito daktaro)
    - A – atostogos, kvalifikacijos tobulinimas
    - AI – periodai iki ir po atostogų / kvalifikacijos tobulinimo + atostogos/ kvalifikacijos tobulinimo periodas (kai gydytojas nedirba 6 ir daugiau darbo dienų dėl atostogų ar kvalifikacijos tobulinimo,  nevertinami 5 darbo dienų iki planuoto nedarbo laikotarpio ir 5 darbo dienų po planuoto nedarbo laikotarpio duomenys. 
    - N - nedarbingumas
    - NI – nedarbingumas + periodas po nedarbingumo (kai gydytojas nedirba 6 ir daugiau darbo dienų dėl laikinojo nedarbingumo, nevertinami nedarbo laikotarpio ir 5 darbo dienų po laikino nedarbingumo duomenys.
    - P – pavadavimas (kai gydytoją jam nesant 2 – 5 darbo dienas pavaduoja ne daugiau kaip 2 gydytojai, šių gydytojų duomenys tomis dienomis nevertinami).
    - PI – pavadavimas + periodas po pavadavimo (kai gydytoją jam nesant 6 ir daugiau darbo dienų pavaduoja ne daugiau kaip 2 gydytojai, šių gydytojų duomenys pavadavimo laikotarpį ir 5 darbo dienas po jo nevertinami).

* [InstitutionCode]_family_doctors_list.csv - Įstaigos šeimos gydytojų sąrašas 
    - Taip - požymis, kurie dalyvauja finansavimo programoje
    - Ne - požymis, kurie nedalyvauja finansavimo programoje
* [InstitutionCode]_free_registrations.csv - Laisvos registracijos pas šeimos gydytoją (sugeneruotas priėmimo grafikas 30 k. d. į priekį neįskaitant pateikimo dienos)

Pastaba. Neturint Programinės įrangos iš kur paimti duomenis, juos suvesti rankiniu būdu pagal pateiktą formatą: https://github.com/vilnius/poliklinikos/tree/master/data/Templates%20for%20doctors%20financial%20control

## Konfigūruojama kontrolės interaktyvi lenta 

## Algoritmas finansavimo sutikrinimui
Kiekvieną darbo diena daromas duomenų atrinkimas ir skaičiavimas (6 val. ryte).
Skaičiuojant 7 dienas, neturi būti išskaičiuojami savaitgaliai, nes patekimas turi būti per 7 kalendorines dienas.

1. Pasiimamas Įstaigos šeimos daktarų sąrašas (family_doctors_list.csv).
2. Patikrinama, ar visi finansavimo programoje dalyvaujantys šeimos gydytojai turi laisvų laikų „Laisvos registracijos pas šeimos daktarą“ (free_registrations.csv) duomenų rinkinyje.
3. Jei gydytojai neturi laisvų laikų, tuomet patikriname ar jis yra įtrauktas į nevertinamų šaimos gydytojų sąrašą (doctors_excluded.csv) duomenų rinkinyje.
    - Jei šeimos gydytojas tikrinimo periode yra įtrauktas į nevertinamų šeimos gydytojų sąrašą (doctors_excluded.csv) duomenų rinkinyje, tuomet  patikrinimo rezultatų lentelėje pažymima atitinkamas požymis kartu su jo reikšme (A, AI, N, NI ...) (ir atliekami atitinkami pataisymai rezultatų patikrinimo lentoje istoriniams duomenims pagal pateisinimo specifiką(+5,-5 dienos ir t.t.));
    - Jei šeimos gydytojo nėra nedarbo periodo duomenų rinkinyje tikrintam periodui, tuomet tikrinimo datai patikrinimo rezultatų lentelėje prie gydytojo įrašomas požymis „Ne“ (neatitinka tvarkos aprašo punkto reikalavimo);
    - Jei gydytojas turi laisvų laikų, vykdomas 4 žingsnis. 
4) Toliau tikrinami visi laikai „Laisvos registracijos“ duomenų rinkinyje. Nustatoma kiekvieno gydytojo artimiausia data, kada jis gali priimti pacientą.
5) Jei nustatytas artimiausios datos ir patikrinimo datos skirtumas yra mažiau arba lygu 7 dienom, tuomet tikrinima nevertinamų šeimos gydytojų sąraše esantis požymis tai datai. Pagal  nurodytus terminus ir reikšmė. Jei reikšmė atitinka, tai pažymime patikrinimo rezultatų lentelėje (prie gydytojo įrašomas požymis „Taip“). Jei datos skirtumas yra daugiau nei 7 dienos, įrašoma „Ne“.


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

