# Duomenų centro PUE skaičiuoklė / simuliatorius

Interaktyvi **Power Usage Effectiveness (PUE)** skaičiuoklė, skirta duomenų centrų technologijų studijoms ir praktiniam supratimui apie energijos vartojimo efektyvumą.

Skirta naudoti studijų dalyke:

- **Studijų dalyko kodas:** ELKRB20713  
- **Studijų dalyko pavadinimas:** Duomenų centrų technologijos  
- **Institucija:** Vilniaus Gedimino technikos universitetas (VILNIUS TECH)

---

## 1. Pagrindinė idėja

Ši skaičiuoklė leidžia studentams:

- matyti, kaip **PUE** priklauso nuo skirtingų energijos vartojimo komponentų;
- suprasti **sąnaudų** (ne IT) energijos dalį;
- įvertinti **metines energijos sąnaudas (MWh)**;
- pamatyti, kokį poveikį turi PUE **metinei ir mėnesio sąskaitai už elektrą (€)**;
- naudoti **realias elektros kainas**, pvz., iš _Nord Pool_ biržos.

Visa logika realizuota tik **HTML + CSS + JavaScript** (be papildomų bibliotekų).

---

## 2. Funkcionalumas

### 2.1. IT ir papildomų sąnaudų energijos slankikliai

Skaičiuoklė turi šias kategorijas:

- **IT įranga** (serveriai, saugyklos, tinklo įranga) – PUE vardiklis.
- **Aušinimo sistemos** – šaldytuvai, sausieji aušintuvai, siurbliai, ventiliatoriai, aušinimo bokštai, drėkinimas.
- **Elektros nuostoliai** – UPS, transformatoriai, PDU, kabelių nuostoliai, skirstyklos, akumuliatorių įkrovimas.
- **Pastato infrastruktūra** – apšvietimas, apsauga, gaisrinė signalizacija, biuro patalpos, BMS ir monitoringas.
- **Atsarginės sistemos** – dyzeliniai generatoriai, jų pašildymas, kuro sistemos, emisijų kontrolė, akumuliatorių palaikymas.

Prie kiekvienos kategorijos yra **„?“ ikonėlė** su trumpu paaiškinimu (tooltip).

---

### 2.2. PUE ir energijos suvestinė

Dešinėje kortelėje realiu laiku rodoma:

- **PUE reikšmė** (su tekstine interpretacija: „Geras efektyvumas“, „Hyperscale lygio“ ir t.t.).
- **Energijos pasiskirstymo juosta**:
  - IT dalis (%),
  - sąnaudų dalis (%).
- Skaičiai MW:
  - IT apkrova,
  - visas duomenų centras (IT + sąnaudos),
  - Sąnaudos (MW ir % visos energijos).

Taip pat yra **gyva PUE formulė**, kuriai taikomos einamosios reikšmės:

PUE = (IT + Aušinimas + Elektros nuostoliai + Pastato inf. + Atsarginės) / IT  
PUE = ( ... ) / ... = ...

---

### 2.3. Energija ir pinigai (€/MWh)

Virš skaičiuotuvo įvedama:

- **Elektros kaina (€/MWh)** – vartotojas įrašo, pvz., _Nord Pool_ Lietuvos zonos spot kainą.

Skaičiuojama darant prielaidą, kad duomenų centras veikia **24/7, 365 dienas per metus (8760 val.)**:

- **Metinės IT energijos sąnaudos:** `IT_MW × 8760` → MWh  
- **Metinis viso DC suvartojimas:** `(IT_MW + Sąnaudų_MW) × 8760` → MWh  
- **Metinė sąskaita už elektrą:** `Metinis DC MWh × €/MWh`  
- **Mėnesio sąskaita (vidutinė):** `Metinė sąskaita / 12`

Rodoma atskiroje **„Elektros sąnaudos“** kortelėje.

---

### 2.4. Realūs scenarijai (preset mygtukai)

Yra keturi paruošti **scenarijai**, kurie automatiškai nustato slankiklių reikšmes:

1. **Senas serverių kambarys (~PUE 2,0)**
   - Mažesnė IT apkrova, didelės aušinimo ir elektros sąnaudos.
2. **Šiuolaikinis kolokacijos DC (~PUE 1,4)**
   - Tipinis komercinis duomenų centras (default scenarijus atidarius puslapį).
3. **Hyperscale DC (~PUE 1,15)**
   - Labai mažos sąnaudos, pavyzdys iš hyperscale parkų.
4. **LT klimatas – laisvas aušinimas (~PUE 1,25)**
   - Duomenų centras Lietuvoje, naudojantis laisvą aušinimą didelę metų dalį.

Paspaudus scenarijų:

- atnaujinami visi slankikliai;
- pakeičiamas scenarijaus aprašymas;
- perskaičiuojamas PUE, MWh ir €.

---

### 2.5. Poraštė (footer)

Puslapio apačioje rodoma studijų informacija:

- **Studijų dalyko kodas:** ELKRB20713  
- **Pavadinimas:** Duomenų centrų technologijos  
- **Vilniaus Gedimino technikos universitetas**

---

## 3. Diegimas ir paleidimas

Jokių specialių priklausomybių nereikia.

### 3.1. Failų struktūra

Minimalus variantas:

```text
projektas/
└── index.html    # Pagrindinis HTML failas su visu CSS ir JS
```

### 3.2. Paleidimas

1. Išsaugokite pateiktą HTML kodą į failą, pvz. `index.html`.
2. Atidarykite failą **bet kurioje modernioje naršyklėje** (Chrome, Firefox, Edge, Safari):
   - dukart spustelėkite `index.html`, arba
   - „Open With…“ → pasirinkite naršyklę.

Jokių serverių ar build įrankių nereikia.

---

## 4. Kaip naudoti paskaitose / laboratoriniuose

### 4.1. Pagrindinis demonstravimas

1. Pasirinkite scenarijų, pvz. **„Senas serverių kambarys“**.
2. Paprašykite studentų:
   - užrašyti IT, sąnaudų ir PUE reikšmes;
   - paaiškinti, kodėl PUE toks didelis.
3. Pakeiskite į **„Hyperscale DC“** ir palyginkite:
   - kiek % energijos dabar suvartoja papildomos sąnaudos;
   - kiek sutaupoma energijos (MWh) per metus.

### 4.2. „Pinigų“ užduotys

Paprašykite studentų:

1. Įrašyti **realų €/MWh** tarifą:
   - surasti _Nord Pool_ dienos kainą,
   - įvesti ją į skaičiuoklę.
2. Palyginti:
   - metinę sąskaitą esant PUE = 1,8 ir PUE = 1,3;
   - kiek € sutaupoma per metus.

---

## 5. Pavyzdinės užduotys studentams

### Užduotis 1 – PUE ir papildomos sąnaudos

> Pasirinkite scenarijų **„Šiuolaikinis kolokacijos DC (~1,4)“**.  
> a) Užrašykite IT apkrovą, papildomų sąnaudų galią ir PUE.  
> b) Pakeiskite aušinimo ir elektros nuostolių slankiklius taip, kad PUE būtų apie 1,2.  
> c) Paaiškinkite, kokias realias priemones reiktų įgyvendinti (min. 3 punktai).

### Užduotis 2 – Sąskaita už elektrą

> Pasirinkite **elektros kainą** iš Nord Pool (Lietuva, šiandienos vidurkis).  
> a) Su scenarijumi „Senas serverių kambarys“ apskaičiuokite metinę ir mėnesio sąskaitą.  
> b) Optimizuokite sąnaudas iki PUE ≈ 1,3.  
> c) Kiek € sutaupoma per metus?  
> d) Jei modernizacija kainuoja 500 000 €, per kiek metų ji atsipirktų?

### Užduotis 3 – Lietuvos klimato efektas

> a) Palyginkite scenarijus „Šiuolaikinis kolokacijos DC“ ir „LT klimatas – laisvas aušinimas“.  
> b) Įveskite tą pačią elektros kainą.  
> c) Kiek MWh ir € per metus sutaupoma vien dėl mažesnių aušinimo sąnaudų?  
> d) Kokie realūs techniniai sprendimai padeda tai pasiekti Lietuvos klimate?

---

## 6. Galimos plėtros idėjos

Jei norėsite projektą plėsti, galima pridėti:

- CO₂ emisijų skaičiavimą (kg CO₂/kWh, t CO₂ per metus).
- A/B palyginimą: „dabartinis DC“ vs „optimizuotas DC“.
- Paprastus grafikus (stulpelines diagramas) energijos pasiskirstymui vizualizuoti.
- „Tikslinio PUE“ režimą – studentai turi koreguoti slankiklius, kad pasiektų nustatytą PuE.

---

## 7. Licencija

Jei naudojama tik studijų reikmėms, nurodykite, kad projektas skirtas **mokymui VILNIUS TECH**.  
