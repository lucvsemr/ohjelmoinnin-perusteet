---
title: "Taulukot"
nav_order: 3
hidden: false
---

Olemme tutustuneet listoihin, joilla on paljon toiminnallisuutta ohjelmoijan elämää helpottamaan. Ehkä tärkein ominaisuus on lisääminen: Ohjelmoijan näkökulmasta listan koko on rajaton. Todellisuudessa listoissa ei ole mitään taikatemppuja -- ne on ohjelmoitu kuten mikä tahansa ohjelma tai työkalu, jonka ohjelmointikieli tarjoaa. Kun luot listan, tietokoneen muistista varataan rajoitettu määrä tilaa. Kun lista loppuu, varataan suurempi tila ja edellisen tilan tiedot kopiodaan uuteen.

Vaikka lista on helppo käyttää, joskus tarvitsemme listan esivanhempaa, taulukkoa (englanniksi **Array**).

Taulukko sisältää rajallisen määrän kohtia (indeksejä) arvoille. Taulukon koko (tai pituus) on näiden kohtien määrä, eli kuinka monta arvoa taulukkoon voi sijoittaa. Taulukon arvoja kutsutaan elementeiksi (englanniksi **elements**).

## Taulukon luominen

On kaksi tapaa luoda taulukko. Ensimmäisessä täytyy määritellä taulukon koko luomisen yhteydessä. Näin luodaan taulukko, joka sisältää kolme kokonaislukua:

```cpp
int[] numbers = new int[3];
```

Taulukko luodaan käyttämällä lisäämällä hakasulkeet sen sisältämän elementtien tyypin perään (**elementtiTyyppi[]**). Uusi taulukko luodaan kutsumalla **new** jota seuraa elementtien tyyppi, hakasulkeet ja taulukon koko hakasulkeissa.

Taulukko johon mahtuu 5 merkkijonoa luodaan seuraavasti:

```cpp
string[] strings = new string[5];
```

## Taulukon elementtien sijoittaminen ja lukeminen

Taulukon elementtiin viitataan sen indeksillä. Seuraavassa esimerkissä luodaan taulukko, joka sisältää kolme kokonaislukua ja sijoitetaan indekseihin 0 ja 2 arvot. Tämän jälkeen tulostetaan taulukon arvot.


```cpp
int[] numbers = new int[3];
numbers[0] = 2;
numbers[2] = 5;
// numbers[1] on tyhjä, tai oikeammin arvoltaan 0

Console.WriteLine(numbers[0]);
Console.WriteLine(numbers[2]);
```

Muuttujan arvon sijoittaminen tiettyyn kohtaan taulukossa toimii hyvin samankaltaisesti kuin minkä tahansa muuttujan arvon sijoittaminen. Taulukossa täytyy kuitenkin määritellä indeksi, eli mihin kohtaan taulukkoa arvo sijoitetaan. Indeksi määritellään hakasulkeissa. Huomaa, että tämä on täsmälleen sama tapa kuin listoissa.

Indeksi on kokonaisluku, jonka arvo on välillä [0, taulukon koko - 1]. Esimerkiksi taulukko, joka sisältää 5 elementtiä, sisältää indeksit 0, 1, 2, 3 ja 4.

```cpp
int[] numbers = new int[5];
numbers[0] = 42;
numbers[1] = 13;
numbers[2] = 12;
numbers[3] = 7;
numbers[4] = 1;

Console.WriteLine("Which index should we access? ");
int index = Convert.ToInt32(Console.ReadLine());

Console.WriteLine(numbers[index]);
```

Taulukossa olevan arvon voi myös sijoittaa toisen muuttujan arvoksi.

```cpp
int[] numbers = new int[5];
numbers[0] = 42;
numbers[1] = 13;
numbers[2] = 12;
numbers[3] = 7;
numbers[4] = 1;

Console.WriteLine("Which index should we access? ");
int index = Convert.ToInt32(Console.ReadLine());

int number = numbers[index];
Console.WriteLine(number);
```

## Taulukon koko ja iterointi

Saat selville taulukon koon käyttämällä taulukon ominaisuutta **Length**. Pääset tähän käsiksi kirjoittamalla taulukon nimen, pisteen ja ominaisuuden, eli esimerkiksi **numbers.Length**. Huomaa, että tämä ei ole metodikutsu, lopussa ei ole sulkeita.

```cpp
int[] numbers = new int[4];

numbers[0] = 12;
numbers[1] = 42;
numbers[2] = 37;
numbers[3] = 9;

Console.WriteLine("The array has " + numbers.Length + " elements:");
for (int i = 0; i < numbers.Length; i++)
{
  Console.WriteLine(numbers[i]);
}
```

```console
The array has 4 elements:
12
42
37
9
```

Yllä olevassa esimerkissä iteroimme indeksit 0, 1, 2 ja 3, ja jokaisen indeksin jälkeen tulostimme arvon joka oli talletettu indeksiin. Ensimmäisenä koodi tulostaa **numbers[0]**, sitten **numbers[1]** ja niin edelleen. Iterointi loppuu, kun silmukan ehto **i < numbers.Length** on epätosi, eli indeksille varatun muuttujan arvo on suurempi tai yhtä suuri kuin taulukon pituus. Huomaa, että iterointi ei lopu sillä hetkellä kun indeksin arvo on liian suuri; ehto evaluoidaan vain silmukan alussa.

Jos indeksi osoittaa taulukon ulkopuolelle, eli elementtiä ei ole olemassa, saamme **IndexOutOfRangeException** -virheen. Tämä virhe kertoo, että taulukossa ei ole olemassa haluttua indeksiä. Et voi hakea tietoa taulukon ulkopuolelta, eli indeksistä joka on alle nollan, tai enemmän kuin taulukon koko.

Seuraavassa esimerkissä on ohjelma joka ensin kysyy käyttäjältä kuinka monta lukua hän haluaa syöttää, sitten kysyy käyttäjältä luvut ja lopuksi tulostaa luvut samassa järjestyksessä. Luvut tallennetaan taulukkoon.


```cpp
Console.WriteLine("How many numbers? ");
int howMany = Convert.ToInt32(Console.ReadLine());

int[] numbers = new int[howMany];

Console.WriteLine("Enter the numbers:");

int index = 0;
while (index < numbers.length) {
    numbers[index] = Convert.ToInt32(Console.ReadLine());
    index = index + 1;
}


Console.WriteLine("Here are the numbers again:");

index = 0;
while (index < numbers.length) {
    Console.WriteLine(numbers[index]);
    index = index + 1;
}
```
Ohjelman suoritus näyttäisi kutakuinkin tältä:

```console
How many numbers? 
> 4 
Enter the numbers: 
> 4 
> 8
> 2 
> 1 
Here are the numbers again: 
4 
8 
2 
1
```

## Elementtien tyypit

Voit luoda taulukon lisäämällä hakasulkeet sen sisältämän elementtien tyypin perään (**elementtiTyyppi[]**). Tämän takia taulukon elementit voivat olla mitä tahansa tyyppiä. Tässä pari esimerkkiä:


```cpp
string[] months = new string[12];
double[] approximations = new double[100];

months[0] = "January";
approximations[0] = 3.14;
```

Jokaisen ohjelmoijan tulisi tietää hieman tietokoneohjelman muistin rakenteesta. Jokainen muuttuja -- oli se sitten primitiivi tai viittaus -- tallennetaan muistiin. Jokaisella muuttujalla on koko, eli määritelty määrä bittejä (nollia ja ykkösiä) jotka se vie muistissa. Muuttujan arvo on myös esitetty bittejä.

Viittaus taulukkoon on itseasiassa tietoa datan sijainnista. Komennolla **taulukko[0]** viittaamme taulukon ensimmäiseen elementtiin. Tämä voidaan myös lukea muodossa *"Mene taulukon alkuun ja siirry eteenpäin 0 kertaa muuttujan kokoisia bittejä -- ja palauta pala dataa muuttujan kokoisena."*

Muuttujan int koko C#:ssa on 32 bittiä. Yksi bitti on varattu etumerkille (plus tai miinus), joten suurin mahdollinen luku int muuttujalle on 2^31 -1. Kun luot int taulukon, joka sisältää 4 elementtiä, varataan muistista 4 \* 32 bittiä muistia. Kun käytät **taulukko[2]**, luetaan 32 bittiä alkaen taulukon alusta + 2 \* 32 bittiä.

Jotkin ohjelmointikielet yrittävät varmistaa, että ohjelmoija ei mene *"väärälle alueelle"*. Jos kääntäjä ei aiheuttaisi poikkeusta kun sanomme **taulukko[-1]**, voisimme lukea datan joka sijaitsee juuri ennen taulukkoa ohjelman muistissa. Tässä tapauksessa ei olisi mitään estettä kirjoittaa ohjelma, joka lukee koko ohjelman muistin.

## Taulukko metodin parametrina

Voit käyttää taulukoita parametrina metodissa aivan kuten mitä tahansa muuttujaa. Koska taulukko on viittaus tyyppi, taulukon arvo on viittaus taulukon sisältämään informaatioon. Kun käytät taulukkoa parametrina metodissa, metodi saa kopion viittauksesta taulukkoon.

```cpp
public static void ListElements(int[] integerArray)
{
  Console.WriteLine("the elements of the array are: ");
  int index = 0;
  while (index < integerArray.Length)
  {
    int number = integerArray[index];
    Console.Write(number + " ");
    index = index + 1;
  }

  Console.WriteLine("");
}
```

Käytännössä:

```cpp
int[] numbers = new int[3];
numbers[0] = 1;
numbers[1] = 2;
numbers[2] = 3;

ListElements(numbers);
```

```console
the elements of the array are: 
1 2 3 
```

Kuten jo aiemmin todettiin, voit vapaasti valita parametrin nimen metodissa, nimi ei tarvitse olla sama kuin muuttujan nimi kun kutsut metodia. Yllä olevassa esimerkissä kutsuja on nimennyt taulukon **integerArray**, kun taas metodia kutsuttaessa parametrin nimi on **numbers**.

Array on **olio** (englanniksi **object**), eli kun muutat taulukkoa metodissa, muutokset säilyvät myös metodin suorituksen jälkeen.

## Lyhyempi tapa luoda taulukko

On olemassa myös oikotie taulukon luomiseen. Tässä luodaan taulukko, joka sisältää kolme kokonaislukua ja alustetaan se arvoilla 100, 1 ja 42:

```cpp
int[] numbers = {100, 1, 42};
```

Eli osana **new** kutsua, voimme myös alustaa taulukon arvot antamalla pilkuilla erotetut arvot. Tämä toimii kaikille tyypeille: alla luodaan taulukko merkkijonoja, sitten taulukko liukulukuja. Lopuksi arvot tulostetaan.

```cpp
string[] arrayOfStrings = {"Mike L.", "Mike P.", "Mike V."};
double[] arrayOfFloatingpoints = {1.20, 3.14, 100.0, 0.6666666667};

for (int i = 0; i < arrayOfStrings.Length; i++) {
    Console.WriteLine(arrayOfStrings[i] + " " +  arrayOfFloatingpoints[i]);
}
```

```console
Mike L. 1.2
Mike P. 3.14
Mike V. 100
```

Kun alustat taulukon arvojen kanssa, taulukon pituus on tarkalleen ottaen arvojen määrä. Arvot sijoitetaan taulukkoon järjestyksessä, eli ensimmäinen arvo sijoitetaan indeksiin 0, toinen indeksiin 1 jne.

```cpp
// indeksi         0   1    2    3   4   5     6     7
int[] numbers = {100,  1,  42,  23,  1,  1, 3200, 3201};

// tulostaa numeron indeksissä 0, eli numeron 100
Console.WriteLine(numbers[0]);
// tulostaa numeron indeksissä 2, eli numeron 42
Console.WriteLine(numbers[2]);
```

Kuten listoissa, et voi käyttää indeksiä joka on taulukon ulkopuolella. Voit kokeilla seuraavaa esimerkkiä omalla koneellasi.


```cpp
string[] arrayOfStrings = {"Mike L.", "Mike P.", "Mike V."};
double[] arrayOfFloatingpoints = {1.20, 3.14, 100.0, 0.6666666667};

for (int i = 0; i < arrayOfFloatingpoints.Length; i++) {
    Console.WriteLine(arrayOfStrings[i] + " " +  arrayOfFloatingpoints[i]);
}
```

# Tehtävät

<Exercise title={'017 Swap indices'}>

Tehtäväpohjassa on valmiina ohjelma, joka luo taulukon ja tulostaa sen arvot kahdesti. Muokkaa ohjelmaa niin, että ensimmäisen tulostuksen jälkeen ohjelma kysyy käyttäjältä kaksi indeksiä. Ohjelma vaihtaa näiden indeksien arvot keskenään ja tulostaa taulukon arvot uudelleen.


```console
1 
3 
5 
7 
9

Give two indices to swap: 
> 2 
> 4

1 
3 
9 
7 
5
```

```console
1 
3 
5 
7 
9

Give two indices to swap: 
> 0 
> 1

3 
1 
5 
7 
9
```

Voit olettaa, että käyttäjä antaa oikeanlaisia indeksejä.


<Note>
Tarvitset lisämuuttujan, johon tallennat toisen arvon hetkeksi.
</Note>

</Exercise>

<Exercise title={'018 Searching array'}>

Tehtäväpohjassa on valmiina taulukko jossa on numeroita. Täydennä ohjelmaa siten, että ohjelma kysyy käyttäjältä lukua, jonka jälkeen ohjelma kertoo löytyykö luku taulukosta. Jos luku löytyy, ohjelma kertoo myös monennellako indeksillä luku on taulukossa. Jos lukua ei löydy, ohjelma kertoo, ettei lukua löytynyt.


```console
Search for? 
> 3 
3 is at index 4.
```

```console
Search for? 
> 7 
7 is at index 7.
```

```console
Search for? 
> 22 
22 was not found.
```

</Exercise>

<Exercise title={'019 Sum of numbers in array'}>

Tehtäväpohjassa on metodi `public static int SumOfNumbersInArray(int[] array)`. Täydennä metodia siten, että se laskee ja palauttaa taulukon arvojen summan.

Voit testata toiminnallisuutta tällä:

```cpp
int[] numbers = {5, 1, 3, 4, 2};
int sum = SumOfNumbersInArray(numbers);
Console.WriteLine(sum);
```

```console
15
```

</Exercise>

<Exercise title={'020 Print neatly'}>


Täydennä metodi `public static void PrintNeatly(int[] array)` siten, että se tulostaa taulukon arvot siististi. Taulukon arvot tulostetaan yhdelle riville ja jokaisen arvon perään tulee pilkku ja välilyönti. Viimeisen arvon perään ei tule pilkkua, vaan rivinvaihto.

Tulosta numerot yhdelle riville käyttämällä `Console.Write`.

Voit kokeilla tulostusta tällä:


```cpp
int[] array = {5, 1, 3, 4, 2};
PrintNeatly(array);
```

```console
5, 1, 3, 4, 2
```

</Exercise>

<Exercise title={'021 Array in stars'}>

Täydennä metodi `public static void PrintArrayInStars(int[] array)` siten, että se tulostaa taulukon arvot tähtinä. Taulukon arvon suuruinen rivi tähtiä tulostetaan jokaiselle arvolle.

Voit kokeilla tulostusta tällä:

```cpp
int[] array = {5, 1, 3, 4, 2};
PrintArrayInStars(array);
```

```
***** 
* 
*** 
**** 
**
```

Taulukon nollas elementti on 5, joten ensimmäisellä rivillä on 5 tähteä. Seuraavalla rivillä on 1 tähti, sitten 3 tähteä jne.

</Exercise>
