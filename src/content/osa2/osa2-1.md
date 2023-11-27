---
title: 'Aliongelmat'
nav_order: 1
hidden: false
---

## Käyttäjän syötteen lukeminen

Ratkaisumalli ohjelmointitehtävissä käyttäjän syötteen (englanniksi **input**) lukemiseen on suoraviivainen. Tähän tehtävään käytämme **System.Console.ReadLine();** -komentoa. Useimmissa tapauksissa haluamme käyttää komentoa useammin kuin kerran, tai käyttää muita **System**:n metodeja. Tätä varten meillä on ohjelmassa **using System;**:

```cpp
using System;

public class Program
{
  public static void Main(string[] args)
  {
    Console.ReadLine();
    // More code...
  }
}

```

Tässä materiaalissa oletamme tämän perusrakenteen olevan olemassa, eikä sitä sisällytetä esimerkkikoodeihin.

## Laskeminen

Ohjelmassa tarvitsemme usein laskutoimituksia, kuten keskiarvon tai summan laskemista. Ratkaisumalli tällaisen ongelman ratkaisemiseen on seuraava:

- Määrittele laskutoimituksessa tarvittavat syötteet ja varaa niille muuttujat. Syöte tarkoittaa laskutoimituksessa käytettäviä arvoja. Syötteiden tyypin voi yleensä päätellä ongelman kuvauksesta.
- Määrittele laskutoimitus ja varaa muuttuja laskutoimituksen tulokselle. Suorita laskutoimitus syötteillä ja sijoita tulos sille varattuun muuttujaan. Tuloksen tyyppi voidaan yleensä päätellä ongelman kuvauksesta.  
- Kun laskutoimitus on suoritettu, tee sen tulokselle jotain. Tämä voi tarkoittaa tuloksen tulostamista, tai esimerkiksi keskiarvon laskemisessa summan jakamista lukujen määrällä.

Esimerkiksi, jos haluamme **luoda ohjelman joka laskee kahden kokonaisluvun summan**, ratkaisumalli on seuraava:


```cpp
// Tunnistetaan syötteet ja varataan niille muuttujat
int first = 1;
int second = 2;

// Tunnistetaan laskutoimitus ja varataan muuttuja tulokselle
int sum = first + second;

// Tulostetaan laskutoimituksen tulos
Console.WriteLine("The sum of " + first + " and " + second + " is " + sum);
```

Ohjelma joka sekä lukee ja laskee yhdistää nämä ratkaisumallit. Ohjelma joka laskee kahden kokonaisluvun tulon näyttää tältä:


```cpp
// Tunnistetaan syötteet ja varataan niille muuttujat
int first = 1;
int second = 2;

// Nimitetään käyttäjän syöte muuttujiin
first = Convert.ToInt32(Console.ReadLine());
second = Convert.ToInt32(Console.ReadLine());

// Tunnistetaan laskutoimitus ja varataan muuttuja tulokselle
int product = first * second;

// Tulostetaan laskutoimituksen tulos
Console.WriteLine("The product of " + first + " and " + second + " is " + product);
```
Yllä olevassa esimerkissä, ohjelma on toteutettu niin että muuttujat määritellään ensin, jonka jälkeen arvot luetaan niihin. Muuttujien määrittely ja arvojen lukeminen niihin voidaan myös yhdistää yhdeksi.

```cpp
int first = Convert.ToInt32(Console.ReadLine());
int second = Convert.ToInt32(Console.ReadLine());

int product = first * second;

Console.WriteLine("The product of " + first + " and " + second + " is " + product);

```

## Vähän vaihtoehtoista toimintaan

Ongelmat sisältävät usein jonkin vaihtoehtoisen toiminnon, ja tällöin käytämme ehtolauseita. Ehtolause alkaa **if** -komennolla, jonka jälkeen tulee sulkujen sisään lauseke. Lauseke arvioi joko todeksi tai epätodeksi. Jos lauseke arvioi todeksi, suoritetaan seuraava aaltosulkeilla rajattu lohko.


```cpp
// Jos arvo on enemmän kuin viisi
if (value > 5)
{
    // sitten...
}
```

Ohjelma joka tulostaa "ok" jos muuttujan arvo on suurempi kuin 42, ja muuten tulostaa "not ok" näyttää tältä:

```cpp
int value = 15;
if (value > 42)
{
    Console.WriteLine("ok");
}
else
{
    Console.WriteLine("not ok");
}
```

Voit myös ketjuttaa useita ehtoja. Tällöin ongelma muuttuu muotoon "jos a, niin b; muuten jos c, niin d; muuten jos e, niin f; muuten g". Ketju koostuu if-lauseesta, jota seuraa else if-lauseita, joissa kussakin on oma lauseke ja lohko.


```cpp
// Jos arvo on enemmän kuin viisi
if (value > 5)
{
    // Toiminnallisuus kun arvo on suurempi kuin viisi
}
else if (value < 0)
{
    // Toiminallisuus kun arvo on pienempi kuin nolla
    // ja arvo EI OLE suurempi kuin viisi
}
else // muussa tapauksessa
{
    // Toiminnallisuus muissa tapauksissa
}
```

Ehdollinen toiminnallisuus voidaan yhdistää muihin ratkaisumalleihin. Katsotaan ongelma **"Lue kaksi kokonaislukua käyttäjältä. Jos lukujen summa on yli 100, tulosta too much. Jos summa on alle 0, tulosta too little. Muuten tulosta ok."** Ohjelma alla yhdistää lukemisen, laskemisen ja ehdollisen toiminnallisuuden.


```cpp
// Julistetaan muuttujat ja luetaan käyttäjän syöte niihin
int first = Convert.ToInt32(Console.ReadLine());
int second = Convert.ToInt32(Console.ReadLine());

// Tunnistetaan laskutoimitus ja varataan muuttuja tulokselle
int sum = first + second;

// Tehdään tuloksella jotain. Tässä tapauksessa
// tulosta käytetään ehdollisissa operaatioissa.

if (sum > 100) // jos summa on yli 100
{
    Console.WriteLine("too much");
}
else if (sum < 0) // jos summa on alle 0
{
    Console.WriteLine("too little");
}
else // muussa tapauksessa
{
    Console.WriteLine("ok");
}
```

# Tehtävät

<Exercise title={'001 Second power'}>

Kirjoita ohjelma, joka lukee kokonaisluvun käyttäjältä, ja tulostaa luvun toisen potenssin, eli luvun kerrottuna itsellään.

```console
> 4
16
```

```console
> 5
25
```

```console
> -3
9
```

</Exercise>

<Exercise title={'002 Square root of sum'}>

Kirjoita ohjelma, joka lukee kaksi kokonaislukua käyttäjältä, ja tulostaa näiden lukujen summan neliöjuuren. Ohjelman ei tarvitse toimia negatiivisilla luvuilla.

Saat neliöjuuren laskettua kokonaisluvusta komennolla Math.Sqrt tähän tapaan:

```cpp
int number = 42;
double squareRoot = Math.Sqrt(number);
Console.WriteLine(squareRoot);
```

```console
> 1 
> 0 
1
```

```console
> 5 
> 4 
3
```

```console
> 1 
> 35 
6
```

</Exercise>

<Exercise title={'003 Absolute value'}>

Kirjoita ohjelma, joka lukee kokonaisluvun käyttäjältä. Jos luku on alle 0, tulosta luku kerrottuna -1:llä. Muussa tapauksessa tulosta luku sellaisenaan. Muutama esimerkki ohjelman odotetusta toiminnasta:

```console
> -3
3
```

```console
> 1
1
```

```console
> 0
0
```

</Exercise>


<Exercise title={'004 Comparison'}>

Kirjoita ohjelma joka lukee kaksi kokonaislukua käyttäjältä. Jos ensimmäinen luku on suurempi kuin toinen, tulosta "(first) is greater than (second)." Jos toinen luku on suurempi kuin ensimmäinen, tulosta "(first) is less than (second)." Muussa tapauksessa tulosta "(first) is equal to (second)." (first) ja (second) tulee korvata käyttäjän antamilla luvuilla.

Muutama esimerkki ohjelman odotetusta toiminnasta:

```console
> 8 
> 4 
8 is greater than 4.
```

```console
> -3 
> 5 
-3 is less than 5.
```

```console
> 1 
> 1 
1 is equal to 1.
```

</Exercise>
