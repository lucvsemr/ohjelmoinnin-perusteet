---
title: 'Laskutoimitukset'
nav_order: 3
hidden: false
---

Laskutoimitukset kuten nämä pitäisi olla sinulle jo varsin tuttuja. Niitä suoritetaan samoilla operaattoreilla koodissa kuin matematiikassa: yhteenlasku **+**, vähennyslasku **-**, kertolasku **\*** ja jakolasku **/**. Laskujärjestys on myös hyvin perinteinen. Vasemmalta oikealle, ottaen huomioon mahdolliset sulkeet, ja kertolasku ja jakolasku ennen yhteen- tai vähennyslaskua.


```cpp
int first = 2;
Console.WriteLine(first); // tulostaa 2
int second = 4;
Console.WriteLine(second); // tulostaa 4

int sum = first + second; // muuttujaan summa tallennetaan first + second
Console.WriteLine(sum); // tulostaa 6
```

## Laskujärjestys sulkujen kanssa

Voit muuttaa laskurjärestystä käyttämällä sulkuja.

```cpp
int calcWithBrackets = (1 + 1) + 3 * (2 + 5);
Console.WriteLine(calcWithBrackets); // tulostaa 23

int calcWithoutBrackets = 1 + 1 + 3 * 2 + 5;
Console.WriteLine(calcWithoutBrackets); // tulostaa 13
```

## Lausekkeet

Lauseke on arvojen yhdistelmä, joka muuttuu arvoksi suorituksen aikana. Esimerkiksi,


```cpp
int calcWithoutBrackets = 1 + 1 + 3 * 2 + 5;
```

sisältää lausekkeen **1 + 1 + 3 \* 2 + 5**, joka lasketaan ennen kuin se annetaan muuttujalle. Laskenta tapahtuu aina ennen sijoitusta, joten laskenta suoritetaan ennen kuin arvo asetetaan muuttujalle.

Laskenta tapahtuu koodin muun osan kanssa samassa järjestyksessä, rivi riviltä, vasemmalta oikealle. Laskenta voidaan myös suorittaa tulostuksen yhteydessä, jos lauseketta käytetään tulostuksen parametrina.


```cpp
int first = 42;
int second = 2;

Console.WriteLine(first + second);
// Lauseke "first + second" lasketaan kun riviä kutsutaan.
// Tulostaa "44".
```

Lauseke ei muuta muuttujan arvoa, ellei lausekkeen tulosta aseteta arvoksi tai annetaan parametrina metodille, kuten tulostamiselle.


```cpp
int first = 42;
int second = 2;

first + second;
// Ei toimi, koska vastausta ei aseta muuttujan arvoksi tai anneta parametrina minnekään, esim. tulostukselle.
```

## Laskutoimitukset ja tulostus

Tähän mennessä olemme tarkastelleet tulostamisen ja laskutoimitusten perusteita. Nyt yhdistetään ne. Voit tulostaa muuttujan arvon **Console.WriteLine()**-funktiolla. Jos haluat liittää arvon merkkijonoon, se tehdään käyttämällä **\*+**-operaattoria ja asettamalla merkkijono lainausmerkkeihin.


```cpp
int truth = 42;

Console.WriteLine("The magic number is " + truth + ".");
```

```console
The magic number is 42.
```

Esimerkissämme yhdistimme merkkijonon, muuttujan arvon ja toisen merkkijonon. 

<Note>Ensimmäinen merkkijono päättyy välilyöntiin, joten sanan "is" ja arvon välissä on väli. Piste lopussa ei sisällä välilyöntiä, joten se on suoraan numeron vieressä.</Note>


```cpp
Console.WriteLine("The magic number is " + 42);
Console.WriteLine(42 + " is the magic number.");
```

```console
The magic number is 42.
42 is the magic number.
```

Jos yhden lisäyksen puolella on merkkijono, toinen puoli muutetaan myös merkkijonoksi ohjelman aikana. Seuraavassa esimerkin tilanteessa kokonaisluku **2** muuttuu merkkijonoksi **"2"** ja yhdistetään toiseen merkkijonoon. Toisessa tapauksessa demonstroimme uudelleen laskujärjestystä ja sulkeita, ja kuinka ne vaikuttavat tilanteeseen.


```cpp
Console.WriteLine("Four: " + (2 + 2));
Console.WriteLine("But! Twenty-two: " + 2 + 2);
```

```console
Four: 4
But! Twenty-two: 22
```

Kaiken tämän tiedon avulla voimme luoda lausekkeen, joka sisältää tekstiä ja muuttujan, joka koostetaan tulostuksen aikana.


```cpp
int x = 10;

Console.WriteLine("value of x is: " + x);

int y = 5;
int z = 6;

Console.WriteLine("y is " + y + " and z is " + z);
```

```console
value of x is 10
y is 5 and z is 6
```

## Kerto- ja jakolasku

Tähän mennessä olemme tehneet hyvin yksinkertaisia lisäyksiä. Kertolasku on myös melko yksinkertaista, sillä matemaattisesti katsottuna se on vain lisäyksen erikoistapaus (no, kaikki on). Esimerkiksi 3\*2 on sama kuin 2+2+2. Koodissa tämä voisi näyttää jotakuinkin tältä:


```cpp
Console.WriteLine(3*2);
Console.WriteLine(2+2+2);
```

```console
6
6
```

Emme mene syvemmälle kertolaskuun. Jakaminen on kiinnostavampaa.

Kun jaetaan koodissa, jaettavien muuttujien tyyppi määrää myös vastauksen tyypin. Esimerkiksi jos jaat kokonaislukuja, tulos on kokonaisluku.

Kokonaislukutyyppisten operandien osalta **/**-operaattorin tulos on kokonaislukutyyppinen ja vastaa kahden operandin osamaaraa pyöristettynä nollaan:


```cpp
Console.WriteLine(13 / 5);    // tulos: 2
Console.WriteLine(-13 / 5);   // tulos: -2
Console.WriteLine(13 / -5);   // tulos: -2
Console.WriteLine(-13 / -5);  // tulos: 2
```

Jos muutamme toisen (tai molemmat) numeroista olemaan desimaalilukuja, tulos on myös desimaaliluku:


```cpp
Console.WriteLine(13 / 5.0);       // tulos: 2.6
int x = 13;
int y = 5;
Console.WriteLine((double)x / y);  // tulos: 2.6
```

Jos haluamme laskea keskiarvon, voimme tehdä sen vaikka näin:

```cpp
int first = 13;
int second = 6;
int third = 42;
double average = (first + second + third) / 3.0; //divide by the amount of numbers
Console.WriteLine(average);  // prints 20.333333333333332
```

<Note> Keskiarvon jakaja on 3.0, joka on desimaaliluku. Vaikka julistamme keskiarvon desimaaliluvuksi, jos kaikki operandit ovat kokonaislukuja, keskiarvon arvo lasketaan 20:ksi.</Note>

## Yleisiä väärinkäsityksiä muuttujista

Kun tietokone suorittaa lähdekoodia, koodi suoritetaan yksi komento kerrallaan, edeten tarkalleen niin kuin koodi määrää. Kun arvo asetetaan muuttujaan, tapahtuma on aina sama: yhtäsuuruusmerkin oikealla puolella oleva arvo kopioituu muuttujan arvoksi vasemmalle. Yleisimmät väärinkäsitykset tämän toimenpiteen yhteydessä ovat:

- Arvo siirretään kopioimisen sijaan. Esimerkiksi, jos lähdekoodissa on lausunto:


```cpp
first = second;
```

Voisit ajatella, että **second**-muuttujalla ei ole enää arvoa, ja arvo on siirretty **first**-muuttujaan. Tämä on väärin, sillä kun **first = second** arvioidaan, muuttujan **second** viittaama arvo **kopioituu** arvoksi **first**-muuttujalle.

- Muuttujan arvon asettamisen käsittäminen riippuvuutena sen sijaan, että arvo kopioitaisiin: Sama esimerkki:


```cpp
first = second;
```

Voisit ajatella, että mikä tahansa muutos **second**-muuttujaan vaikuttaa myös **first**-muuttujaan. Tämä ei pidä paikkaansa. Kun koodirivi on suoritettu, **first** ja **second** välillä ei ole vuorovaikutusta. Arvon kopioiminen tehdään vain kerran.

- Kolmas ja yleisin väärinkäsitys on kopioinnin järjestys. Usein koodin alussa on helppo sekoittaa sijoituksen suuntaa. Esimerkiksi, saatat haluta kirjoittaa


```cpp
42 = int truth;
42 = 21;
```

Mikä ei tietenkään toimi. Muuttujien käyttäytymisen koodissa ymmärtämiseksi voi olla tarpeellista ottaa kynä ja paperin, ja kirjoittaa ylös mitä koodissa tapahtuu, rivi riviltä. Esimerkiksi tässä koodissa tapahtuu melko paljon:


```cpp
rivi 1: int first = (1 + 1);
rivi 2: int second = first + 3 * (2 + 5);
rivi 3:
rivi 4: first = 5;
rivi 5:
rivi 6: int third = first + second;
rivi 7: Console.WriteLine(first);
rivi 8: Console.WriteLine(second);
rivi 9: Console.WriteLine(third);
```

Seuraavassa konsolissa voit nähdä, mitä tapahtuu, rivi riviltä. Ohjelma ei toki tulosta kaikkea tätä, mutta konsoli-ikkuna voi olla helpompi lukea kuin pelkkä teksti.

```console
rivi 1: luodaan muuttuja first
rivi 1: arvioidaan laskutoimitus 1 + 1 ja annetaan arvo muuttujalle first
rivi 1: muuttujan first arvo on nyt 2
rivi 2: luodaan muuttuja second
rivi 2: lasketaan 2 + 5, 2 + 5 -> 7
rivi 2: lasketaan 3 * 7, 3 * 7 -> 21
rivi 2: lasketaan first + 21
rivi 2: kopioi muuttujan first arvon laskentaan, muuttujan first arvo on 2
rivi 2: lasketaan 2 + 21, 2 + 21 -> 23
rivi 2: annetaan muuttujalle second arvoksi 23
rivi 2: muuttujan second arvo on nyt 23
rivi 3: (tyhjä, ei tee mitään)
rivi 4: annetaan muuttujalle first arvoksi 5
rivi 4: muuttujan first arvo on nyt 5
rivi 5: (tyhjä, ei tee mitään)
rivi 6: luodaan muuttuja third
rivi 6: lasketaan first + second
rivi 6: kopioi muuttujan first arvon laskentaan, muuttujan first arvo on nyt 5
rivi 6: lasketaan 5 + second
rivi 6: kopioi muuttujan second arvon laskentaan, muuttujan second arvo on nyt 23
rivi 6: lasketaan 5 + 23 -> 28
rivi 6: annetaan muuttujalle third arvoksi 28
rivi 6: muuttujan third arvo on nyt 28
rivi 7: tulostetaan muuttuja first
rivi 7: kopioi muuttujan first arvon tulostusta varten, muuttujan first arvo on nyt 5
rivi 7: tulostetaan arvo 5
rivi 8: tulostetaan muuttuja second
rivi 8: kopioi muuttujan second arvon tulostusta varten, muuttujan second arvo on nyt 23
rivi 8: tulostetaan arvo 23
rivi 9: tulostetaan muuttuja third
rivi 9: kopioi muuttujan third arvon tulostusta varten, muuttujan third arvo on nyt 28
rivi 9: tulostetaan arvo 28

```

# Tehtävät

<Note>Huom! Tee harjoitukset englanniksi, katso mallia harjoitusten esimerkeistä, miten koodin tulee toimia ja mitä sen tulee tulostaa (englanniksi)</Note>

<Exercise title={'016 Seconds in days'}>

Luo ohjelma, joka kysyy käyttäjältä päivien määrää ja tulostaa kyseisen päivämäärän kokonaismäärän sekunteina, antaa vastauksen ja lopettaa.

Esimerkkitulostus:



```console
How many days?
> 2
172800
```

```console
How many days?
> 7
604800
```

</Exercise>

<Exercise title={'017 Input two integers'}>

Luo ohjelma, joka kysyy käyttäjältä kaksi kokonaislukua ja laskee niiden summan.

Muista, että syöte on merkkijono, joten sinun on muunnettava se kokonaisluvuksi!

Esimerkkitulos:



```console
Give the first number!
> 8
Give the second number!
> 3
The sum is 11
```

```console
Give the first number!
> 3
Give the second number!
> -1
The sum is 2
```

</Exercise>

<Exercise title={'018 Input three integers'}>

Laajenna hieman edellistä harjoitusta. Luo nyt ohjelma, joka pyytää kolmea kokonaislukua käyttäjältä ja laskee niiden summan.

Esimerkkitulos voisi olla:


```console
Give the first number!
> 3
Give the second number!
> -1
Give the third number!
> 2
The sum is 4
```

</Exercise>

<Exercise title={'019 Sum of two integers'}>

Luo ohjelma, joka kysyy käyttäjältä kaksi kokonaislukua ja laskee niiden summan. Tällä kertaa tulosta myös laskutoimitus käyttäjälle.

Esimerkkitulos:



```console
Give the first number!
> 3
Give the second number!
> 1
3 + 1 = 4
```

```console
Give the first number!
> 5
Give the second number!
> -1
3 + -1 = 2
```

</Exercise>

<Exercise title={'020 Multiply two integers'}>

Luo ohjelma, joka kysyy käyttäjältä kaksi `kokonaislukua` ja kertoo ne keskenään. Tulosta laskutoimitus ja vastaus käyttäjälle.

Esimerkkitulos:

```console
Give the first number!
> 3
Give the second number!
> 2
3 * 2 = 6
```

```console
Give the first number!
> 50
Give the second number!
> -2
50  * -2 = -100
```

</Exercise>

<Exercise title={'021 Average of two integers'}>

Luo ohjelma, joka kysyy käyttäjältä kaksi kokonaislukua ja laskee niiden keskiarvon desimaalilukuna `(double)`.

Esimerkkitulos:


```console
Give the first number!
> 3
Give the second number!
> 2
The average is 2.5
```

</Exercise>

<Exercise title={'022 Average of three integers'}>

Luo ohjelma, joka kysyy käyttäjältä kolme `kokonaislukua` ja laskee niiden keskiarvon desimaalilukuna `(double)`.

Esimerkkitulos:


```console
Give the first number!
> 3
Give the second number!
> 2
Give the third number!
> 1
The average is 2.0
```

</Exercise>

<Exercise title={'023 Tiny calculator'}>

Luodaan ohjelma, joka suorittaa kaikki peruslaskutoimitukset käyttäjän syöttämien `kokonaislukujen` avulla! Kysy kaksi kokonaislukua ja suorita ja tulosta laskutoimitukset niiden avulla.
Muista tulostaa laskutoimitukset näkyville.

Esimerkkitulos:


```console
Give the first number!
> 3
Give the second number!
> 2
3 + 2 = 5
3 - 2 = 1
3 * 2 = 6
3 / 2 = 1.5
```

</Exercise>