---
title: 'Muuttujat'
nav_order: 2
hidden: false
---

Edellisessä osiossa esittelimme ensimmäisen **muuttujan** (englanniksi **variable**), **merkkijonomuuttujan** (**string**). Merkkijono ei ole ainoa muuttuja koodauksessa. Muuttujat ovat perustietovarastoja koodissa. Muuttujat voivat olla esimerkiksi tuttuja **merkkijonoja** tekstille, mutta myös **int**  kokonaisluvuille (**integer**), **double** desimaaliluvuille tai **boolean** totuusarvoille. Kuten aiemmin mainittiin, muuttujan arvo asetetaan käyttäen **yhtäsuuruusmerkkiä, =**.


```cpp
int truth = 42;
```

Yllä olevassa esimerkissä **esitellään** muuttuja nimeltä **truth** ja **annetaan sille arvo** **42**.

Tätä kokonaislukua voidaan liittää yhteen merkkijonon kanssa ohjelmassamme.


```cpp
int truth = 42;
double pie = 3.141592653;
bool valid = true;
string magic = "The magic number: ";
Console.WriteLine(magic + truth);
Console.WriteLine("Life of " + pie);
Console.WriteLine("This is awesome: " + valid);
```

Tulostaa koodin ajettaessa seuraavaa

```console
The magic number: 42
Life of 3.141592653
This is awesome: true
```

Muuttujien nimet täytyy olla yksilöllisiä koodilohkossa. Voit esitellä jokaisen muuttujaa vain kerran. Mutta, kuten nimi **muuttuja** viittaa, voit muuttaa niiden arvoa.


```cpp
int number = 42;
Console.WriteLine(number);
number = 21;
Console.WriteLine(number);
```

Tulostaa

```console
42
21
```

## Arvon määrittäminen muuttujalle

Katsotaanpa tarkemmin edellistä esimerkkiä...

```cpp
int number = 42;
Console.WriteLine(number);
number = 21;
Console.WriteLine(number);
```

Tulostaa

```console
42
21
```

Ensimmäisellä rivillä esitellään muuttuja ja annamme sille arvon. Tällä tiedolla kääntäjä luo **int** -muuttujan ja tallentaa arvon.

Toisella rivillä käytämme muuttujaa tallennetun tiedon hakemiseen. Voitaisiin sanoa, että muuttujan nimi on viittaus arvoon. Kun olemme saaneet arvon, komento tulostaa sen pyydettynä.

Aiemmin mainittiin, että muuttujan voi esitellä vain kerran. Tällä kertaa emme esittele sitä. Erotuksena on **int** ensimmäisellä rivillä. Kuten teimme toisella rivillä tulostaessamme arvon, kolmannella rivillä viittaamme jälleen kerran numeroon, emme esittele sitä uudelleen. **Yhtäsuuruusmerkillä** annamme muuttujalle **uuden arvon**.


## Muuttujien tyypitys

Muuttujat **C#** -koodissa ovat staattisesti tyypitettyjä. Tämä tarkoittaa, että kun muuttuja on esitelty tiettyyn tyyppiin, tyyppi ei muutu\*.

\* Nykypäivänä C#:ssa on avainsana **dynamic**, mutta se ei ole relevantti peruskoodauksessa. Tarkoituksiimme käsittelemme C#:aa staattisena tyypityksenä.

Esimerkiksi, tämä toimii:


```cpp
int magic = 42;
magic = 41;
```

Tämä taas ei...

```cpp
int magic = 42;
magic = "Magic";
```

Tästä on toki poikkeuksia olemassa. Esimerkiksi voit asettaa integer luvun doubleksi. 

```cpp
double decimal = 10; // Toimii

int number = 20;
decimal = number; // Toimii
```

... mutta ei toisinpäin, koska int viittaa kokonaislukuun!

```cpp
int number = 4.2; // Ei toimi

double decimal = 4.2;
number = decimal // Ei toimi myöskään näin
```

## Muuttujien nimeäminen

Kävimme aiemmin läpi koodin luettavuutta. Mietitäänpä seuraavaa esimerkkiä...

```cpp
double a = 3.14;
double b = 22.0;
double c = a * b * b;

Console.WriteLine(c);
```

Tulostaa...

```console
1519.76
```

```cpp
double pi = 3.14;
double radius = 22.0;
double area = pi * radius * radius;

Console.WriteLine(area);
```

Tulostaa...

```console
1519.76
```

Molemmat tuottavat saman tuloksen. Toisaalta toinen on paljon helpompi lukea, ja sen toiminnallisuus on helpompi ymmärtää. Molemmat koodit laskevat ympyrän pinta-alan. Ensin määritellään piin arvo, sitten säde, ja lopuksi lasketaan pinta-ala.

Muuttujien nimille on tietyt rajoitukset sekä käytänteet. Muuttujien nimet...

- eivät voi sisältää erikoismerkkejä, kuten **!**, **?**, **å** tai **ö**
- eivät voi sisältää tyhjiä välejä (englanniksi **whitespace**)
- alkavat pienellä alkukirjaimella
- tulisi kirjoittaa camelCasella

C#:n muuttujat kirjoitetaan yleensä [**camelCasella (täällä)**](https://fi.wikipedia.org/wiki/CamelCase). Tämä tarkoittaa, että muuttujan nimi alkaa pienellä kirjaimella, siinä ei ole muita merkkejä kuin kirjaimia ja numeroita, eikä se sisällä välimerkkejä tai tyhjiä välejä.

Vaikka **snake_case** alaviivalla olisi sallittu muuttujanimi, tällaista nimeämiskäytäntöä ei suositella, eikä sitä tule käyttää tämän kurssin aikana.


```cpp
int 9var = 42; // Ei toimi
int var9 = 42; // Toimii, mutta ei kovin selvä nimeämistapa
```

Muuttujat voidaan esitellä vain kerran (kuten yllä opittiin)

```cpp
string camelCase = "Camels are fun!";
string camelCase = "Camels are nice"; // Ei toimi, koska muuttuja jo esitelty ylemmällä rivillä
```

## Erilaisten muuttujien lukeminen käyttäjältä

Aiemmin tutustuimme, miten **merkkijonomuuttuja** kysytään käyttäjältä

```cpp
public class Program
{
   public static void Main()
   {
      Console.Write("Give a message: ");
      string message = Console.ReadLine();
      Console.WriteLine(message);
   }
}
```

```console
Give a message: I want to print this
I want to print this
```

Kaikki muut muuttujat, kuten kokonaisluvut, desimaaliluvut tai totuusarvot, luetaan myös käyttäjältä merkkijonoina. Meidän täytyy muuntaa ne oikeaan tyyppiin käyttämällä sisäänrakennettuja metodeja.


```cpp
Console.Write("Give integer value: ");

// Esittele muuttuja tekstiksi ja lue käyttäjältä teksti
string userInput = Console.ReadLine();

// Konvertoi käyttäjän syöttämä syöte kokonaisluvuksi
int intValue = Convert.ToInt32(userInput);

Console.WriteLine("You gave " + intValue);

Console.Write("Give double value: ");

// Aseta uusi arvo jo esiteltyyn muuttujaan
userInput = Console.ReadLine();

// Konvertoi käyttäjän syöte desimaaliluvuksi
double doubleValue = Convert.ToDouble(userInput);

Console.WriteLine("You gave " + doubleValue);
```

This would print

```console
Give integer value: 42
You gave: 42
Give double value: 4.2
You gave: 4.2
```

Yllä olevassa esimerkissä luemme sekä kokonaisluvun että desimaaliluvun. Kuten näet, menetelmien välillä ei ole suurta eroa, vain metodin nimi eroaa koodauksen näkökulmasta.

Jos haluamme muuntaa totuusarvon merkkijonosta, on kaksi vaihtoehtoa: **True** ja **False**.


```cpp
string truth = "True";
bool booleanValue = System.Convert.ToBoolean(truth);
Console.WriteLine(booleanValue);

truth = "False";
booleanValue = System.Convert.ToBoolean(truth);
Console.WriteLine(booleanValue);
```

Antaa meille

```console
True
False
```

**Convert-luokkaa** voidaan käyttää muuntamaan merkkijonoja myös moniin muihin tyyppeihin. Käsittelemme niitä niiden ilmetessä, mutta uteliaisuudesta kiinnostuneille, lisätietoja löytyy [** täältä**](https://learn.microsoft.com/en-us/dotnet/api/system.convert?view=net-7.0).


# Tehtävät

<Note>Huom! Tee harjoitukset englanniksi, katso mallia harjoitusten esimerkeistä, miten koodin tulee toimia ja mitä sen tulee tulostaa (englanniksi)</Note>

<Exercise title={'011 Print variables'}>

Harjoituksessa on valmis pohja, joka tulostaa seuraavaa:

```console
Days to summer:
100
Hours to lunch:
1
Coding is fun:
Are you sure?
```

Muuta muuttujien `arvoja` jotta ohjelma tulostaa

```console
Days to summer:
200
Hours to lunch:
3.5
Coding is fun:
It sure is!
```

Älä muuta mitään muuta kuin muuttujien arvoja!

</Exercise>

<Exercise title={'012 Print integer'}>

Luo ohjelma, joka kysyy käyttäjältä `kokonaislukua`. Käyttäjän syötön jälkeen ohjelma tulostaa `kokonaisluvun`. Esimerkki:


```console
Give a number!
> 11
You gave 11
```

```console
Give a number!
> 42
You gave 42
```

<Note>Käytä WriteLine tulostukseen, ei pelkkä Write!</Note>

</Exercise>

<Exercise title={'013 Print double'}>

Luo ohjelma, joka kysyy käyttäjältä `desimaalilukua`. Käyttäjän syötön jälkeen ohjelma tulostaa `desimaaliluvun`. Esimerkki:


```console
Give a number!
> 11.11
You gave 11.11
```

```console
Give a number!
> 41.999999
You gave 41.999999
```

</Exercise>

<Exercise title={'014 Print truth'}>

Luo ohjelma, joka kysyy käyttäjältä `totuusarvoa`. Käyttäjän syötön jälkeen ohjelma tulostaa `totuusarvon`. Esimerkki:



```console
Give me the truth!
> tRuE
True
```

```console
Give me the truth!
> false
False
```

</Exercise>

<Exercise title={'015 Asking multiple inputs'}>

Kootaan nyt lopuksi kaikki tieto yhteen! Luo ohjelma, joka kysyy käyttäjältä merkkijonoa, kokonaislukua, desimaalilukua ja totuusarvoa, ja tulostaa ne seuraavasti:



```console
Give a string:
> This is a masterpiece!
Give an integer:
> 42
Give a double:
> 3.1415
Give a boolean:
> True
Your string: This is a masterpiece!
Your integer: 42
Your double: 3.1415
Your boolean: True
```
</Exercise>