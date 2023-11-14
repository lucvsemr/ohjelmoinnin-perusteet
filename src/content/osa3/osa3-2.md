---
title: "Listat"
nav_order: 2
hidden: false
---

Ohjelmoinnissa törmää usein tilanteisiin, joissa halutaan käsitellä useita arvoja. Tähän mennessä olemme käyttäneet ratkaisuna erillisiä muuttujia, mutta tämä on epäkäytännöllistä.

```cpp
string word1;
string word2;
string word3;
// ...
string word10;
```

Yllä esitelty ratkaisu on käytönnössä hyödytön -- kuvittele tilanne, jossa sanoja on tuhansia.

Ohjelmointikielet tarjoavat työkaluja suurten määrien arvojen käsittelyyn. Seuraavaksi kurkistamme listaan (**List**), joka on tarkoitettu samantyyppisten arvojen säilyttämiseen.

**List** on valmiiksi tehty työkalu C#:ssa, joka auttaa listojen käsittelyssä. Se tarjoaa erilaisia metodeja, joilla voi lisätä arvoja listaan, poistaa arvoja listasta ja hakea arvoja listan tietyltä paikalta. Listan toteutus -- eli se, miten lista on ohjelmoitu -- on abstrahoitu metodien taakse, joten listaa käyttävän ohjelmoijan ei tarvitse huolehtia listan sisäisestä toiminnasta.

## Listojen käyttäminen ja luominen

Jotta listaa voidaan käyttää, se täytyy ensin ottaa käyttöön ohjelmassa. Tämä tapahtuu **using System.Collections.Generic;** -komennolla ohjelman alussa. Alla on esimerkki ohjelmasta, jossa **List** on otettu käyttöön.

Jotta listaa voidaan käyttää, se täytyy ensin alustaa. Alla on esimerkkki jossa luodaan List joka sisältää kokonaislukuja, nimeltään **numbers**.


```cpp
using System.Collections.Generic;

public class Program 
{
    public static void Main(string[] args) 
    {
      List<int> numbers = new List<int>();
      // Loput koodista...
    }
}

```

Uusi lista luodaan komennolla **List<tyyppi\> list = new List<tyyppi\>()**, jossa tyyppi on listaan tallennettavien arvojen tyyppi (esim. int). Luodaan esimerkiksi lista joka sisältää merkkijonoja.

```cpp
List<string> strings = new List<string>();
```

Listan itsensä tyyppi on **List**. Kun lista alustetaan, määritellään muuttujan tyypin lisäksi myös listaan tallennettavien arvojen tyyppi -- kaikki listaan tallennettavat muuttujat ovat saman tyyppisiä. Tällöin merkkijonoja sisältävä lista on **List<string\>**. Uusi lista luodaan komennolla **new List<\>();**.

## Listan alkioiden tyypin määrittäminen

Kun määrittelemme listan sisältämien alkioiden (eli listassa olevien asioiden) tyyppiä, kirjoitetaan tyyppi samalla tavalla kuin muuttujia määriteltäessä. Lista, joka sisältää int-tyyppisiä alkioita, määritellään muodossa **List<int\>**; ja lista, joka sisältää double-tyyppisiä muuttujia, määritellään muodossa **List<double\>**.

Alla on esimerkkejä erilaisia tyyppejä sisältävien listojen luomisesta.


```cpp
List<int> list = new List<int>();
list.Add(1);
```

```cpp
List<double> list = new List<double>();
list.Add(4.2);
```

```cpp
List<bool> list = new List<bool>();
list.Add(true);
```

```cpp
List<string> list = new List<string>();
lista.Add("String is text");
```

Kun lista on kerran luotu, List olettaa että kaikki siihen lisättävät alkiot ovat oikeaa tyyppiä. Tietysti voit lisätä listaan myös oikeaa tyyppiä olevia **muuttujia**. Tällöin muuttujan arvo tallentuu listan alkioksi.

```cpp
List<int> integers = new List<int>();
int integer = 1;
integers.Add(integer);

List<double> doubles = new List<double>();
double d = 4.2;
doubles.Add(d);
```

## Arvojen lisääminen ja hakeminen tietystä paikasta Listassa

Seuraava esimerkki demonstroi muutaman merkkijonon lisäämistä Listaan, joka sisältää merkkijonoja. Lisääminen tapahtuu listan metodia **Add** käyttämällä, jolle annetaan parametrina lisättävä arvo. Tämän jälkeen tulostetaan arvo paikassa 0. Alkion arvon hakeminen tietystä paikasta tapahtuu erikoismerkinnällä **list[index]**, jossa **list** on listan nimi ja **index** on paikka, josta arvo haetaan.


```cpp
public class WordListExample 
{
  public static void Main(string[] args) 
  {
    // luodaan wordList, joka sisältää merkkijonoja
    List<string> wordList = new List<string>();

    // lisätään wordListiin kaksi arvoa
    wordList.Add("First");
    wordList.Add("Second");

    // haetaan arvo paikasta 0 ja tulostetaan se
    Console.WriteLine(wordList[0]);
  }
}
```

Ohjelmamme tulostaa:

```console
First
```

Kuten näkyy, jälkimmäinen metodi hakee listasta ensimmäisen arvon, kun sille annetaan parametriksi **0**. Tämä johtuu siitä, että listan paikat lasketaan nollasta alkaen. Ensimmäinen arvo löytyy siis kohdasta wordList[0], toinen kohdasta wordList[1] jne.


```cpp
public class WordListExample 
{
  public static void Main(string[] args) 
  {
    // luodaan wordList, joka sisältää merkkijonoja
    List<string> wordList = new List<string>();

    // lisätään wordListiin kaksi arvoa
    wordList.Add("First");
    wordList.Add("Second");

    // haetaan arvo paikasta 1 ja tulostetaan se
    Console.WriteLine(wordList[1]);
  }
}
```

Ohjelma tulostaa:

```console
Second
```

## Tiedon hakeminen "olemattomasta" kohdasta

Jos yrität hakea tietoa paikasta, jota ei ole olemassa, ohjelma tulostaa **ArgumentOutOfRangeException** -virheen. Seuraavassa esimerkissä listalle lisätään kaksi arvoa, minkä jälkeen yritetään tulostaa arvo paikasta 2.

```cpp
public class WordListExample 
{
  public static void Main(string[] args) 
  {
  public static void Main(string[] args) 
  {
    // luodaan wordList, joka sisältää merkkijonoja
    List<string> wordList = new List<string>();

    // lisätään wordListiin kaksi arvoa
    wordList.Add("First");
    wordList.Add("Second");

    // haetaan arvo paikasta 2 ja tulostetaan se
    Console.WriteLine(wordList[2]);
  }
}
```

Koska numerointi (eli indeksointi) listan alkioissa alkaa nollasta, ohjelma ei löydä mitään paikasta kaksi ja sen suoritus päättyy virheeseen. Alla on kuvaus virheestä, jonka ohjelma aiheuttaa.

```console
Unhandled exception. System.ArgumentOutOfRangeException: Index was out of range. Must be non-negative and less than the size of the collection. (Parameter 'index')
   at System.Collections.Generic.List`1.get_Item(Int32 index)
   at WordListExample.Program.Main(String[] args) in ... Program.cs:line 13
```

Virheviesti kertoo tarkalleen, mitä ja missä tapahtui. Ensin, virhe sisältää virheen tyypin, **ArgumentOutOfRangeException**. Sen jälkeen se antaa mahdollisen korjauksen. Seuraavaksi virhe sisältää, mikä metodi aiheutti virheen. Tässä tapauksessa se olisi **get_Item(Int32 index)**. Viimeiseksi virhe kertoo, mikä osa koodistamme aiheutti virheen.

Kuten huomataan, kun kutsutaan List[index], kutsutaan itse asiassa metodia **System.Collections.Generic.List`1.get_Item(Int32 index)**, joka on monimutkaisempi metodi, joka on jo valmiiksi rakennettu. Tämä on valmiiden metodien etu: meidän ei tarvitse huolehtia siitä, miten toteutamme metodin datan hakemiseksi listasta, koska se on jo valmiina.

## Numerointi ja indeksi

Numerointi eli indeksointi alkaa aina nollasta. Listan ensimmäinen arvo sijaitsee indeksissä 0, toinen indeksissä 1, kolmas indeksissä 2 jne. Ohjelmissa indeksiä merkitään muuttujalla **i**.

Esimerkiksi lista, joka sisältää kokonaislukuja, voisi sisältää seuraavaa:

|i|0|1|2|3|4|5|6|...|
|-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|value|6|1|2| 4| 4| 3||

Yllä olevassa listassa ensimmäinen arvo on 6 ja toinen arvo 1. Jos listaan lisättäisiin uusi arvo kutsumalla **Add-metodia** parametrinaan 8, luku 8 sijoittuisi indeksiin 6. Se olisi listan seitsemäs luku.


```cpp
numbers.Add(8);
```

|i|0|1|2|3|4|5|6|...|
|-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|value|6|1|2| 4| 4| 3|8|

Samoin, kutsumalla **numbers[index]** parametrilla 4, saataisiin listan viides luku.

Jokaisella C#:n tarjoamalla työkalulla on nimi ja sijainti. Ohjelma voi käyttää työkalua sen jälkeen, kun se on tuotu käyttöön **using** -komennolla. Komennolle annetaan halutun luokan sijainti ja nimi. Esimerkiksi **Console** löytyy **System** -luokasta, joten se tuodaan käyttöön komennolla **using System;** koodin alussa.


```cpp
using System;

public class Program 
{  
    public static void Main(string[] args) 
    {  
        Console.WriteLine("Console has been imported");
    }  
}   
```

Sama pätee yleensä kaikkiin C#:n luokkiin. **Console** kutsutaan suoraan järjestelmästä, joten voimme tuoda sen käyttöön pelkällä **using System;** -komennolla. Jos haluamme käyttää Listoja, joudumme menemään syvemmälle ja käyttämään **using System.Collections.Generic;** -komennolla.

```cpp
using System;
using System.Collections.Generic;

public class Program 
{  
    public static void Main(string[] args) 
    {  
        Console.WriteLine("Console has been imported");
        List<string> list = new List<string>();
        list.Add("List can be now used, too.");
    }  
}   
```

<Note>
Nykyään C#:n kääntäjä ei välttämättä kaipaa yleisimpiä tuonteja, kuten System tai System.Colletions.Generic.
On kuitenkin tärkeää ymmärtää näiden olemassaolosta ja toiminnasta, jotta vanhempaa koodia lukiessa ei tule yllätyksiä.
</Note>

## Listan läpikäyminen

Seuraavaksi tutustumme metodeihin, joilla voidaan käydä läpi listan arvoja. Aloittakaamme yksinkertaisesta esimerkistä, jossa tulostetaan lista, joka sisältää neljä arvoa.

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

Console.WriteLine(teachers[0]);
Console.WriteLine(teachers[1]);
Console.WriteLine(teachers[2]);
Console.WriteLine(teachers[3]);
```

```console
Simon
Samuel
Ann
Anna
```

Esimerkki on huomattavan kömpelö. Entä jos listassa olisi enemmän arvoja? Tai vähemmän? Entä jos emme tiedä, montako arvoa listalla on?

Listan alkioiden määrä saadaan selville listan **Count** -ominaisuudella, joka palauttaa listan sisältämien alkioiden määrän. Määrä on kokonaisluku (int), ja sitä voidaan käyttää osana lauseketta tai tallentaa kokonaislukumuuttujaan myöhempää käyttöä varten.


```cpp
List<string> list = new List<string>();
Console.WriteLine("Number of values on the list: " + list.Count);

list.Add("First");
Console.WriteLine("Number of values on the list: " + list.Count);

int values = list.Count;

list.Add("Second");
Console.WriteLine("Number of values on the list: " + values);
```

```console
Number of values on the list: 0 
Number of values on the list: 1 
Number of values on the list: 1
```

<Note> 
Count ei ole metodi vaan ominaisuus. Tämä tarkoittaa, että Countia kutsuttaessa ei lisätä sulkeita loppuun!
</Note>

Tehdään ohjelmastamme uusi versio joka tulostaa jokaisen arvon listalta. Tässä väliversiossa käytämme **index** -muuttujaa pitämään kirjaa siitä, mikä paikka tulostetaan.

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

int index = 0;

if (index < teachers.Count) 
{
  Console.WriteLine(teachers[index]); // index = 0
  index = index + 1; // index = 1
}

if (index < teachers.Count) 
{
  Console.WriteLine(teachers[index]); // index = 1
  index = index + 1; // index = 2
}

if (index < teachers.Count) 
{
  Console.WriteLine(teachers[index]); // index = 2
  index = index + 1; // index = 3
}

if (index < teachers.Count) 
{
  Console.WriteLine(teachers[index]); // index = 3
  index = index + 1; // index = 4
}

if (index < index.Count) 
{
  // tätä ei suoriteta sillä index = 4 ja teachers.Count = 4
  Console.WriteLine(teachers[index]);
  index = index + 1;
}
```

Huomaamme, että yllä olevassa koodissa on paljon toistoa.

Voimme muuttaa if-lauseet while-silmukoiksi, jotka toistuvat niin kauan kuin ehto index < teachers.Count pitää paikkansa (eli muuttujan index arvo ei kasva liian suureksi).

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

int index = 0;
// Toista niin kauan kuin muuttujan `index`
// arvo on pienempi kuin teachers-listan koko
while (index < teachers.Count) 
{
  Console.WriteLine(teachers[index]);
  index = index + 1;
}
```

Nyt tulostus toimii riippumatta siitä, kuinka monta alkiota listalla on.

For-silmukka on erittäin kätevä tässä. Voimme muuttaa yllä olevan silmukan for-silmukaksi, jonka jälkeen ohjelma näyttää tältä.

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

for (int index = 0; index < teachers.Count; index++) 
{
    Console.WriteLine(teachers[index]);
}
```

```console
Simon
Samuel
Ann
Anna
```

Indeksin muuttuja for-silmukassa on tyypillisesti nimetty **i**:

```cpp
for (int i = 0; i < teachers.Count; i++) 
{
    Console.WriteLine(teachers[index]);
}
```

Mietitään tilannetta jossa haluamme käsitellä listaa, joka sisältää kokonaislukuja. Toiminnallisuus on pitkälti sama kuin edellisessä esimerkissä. Suurin ero on listan alustamisessa -- listan sisältämän arvon tyyppi määritellään int:ksi, ja tulostettava arvo tallennetaan muuttujaan nimeltä number ennen tulostamista.

```cpp
List<int> numbers = new List<int>();

numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
numbers.Add(4);

for (int i = 0; i < numbers.Count; i++) 
{
    int number = numbers[i];
    Console.WriteLine(number);
    // vaihtoehtoisesti: Console.WriteLine(numbers[i]);
}
```

```console
1
2
3
4
```

Numeroiden tulostaminen päinvastaisessa jäjestyksessä olisi myös suoraviivaista.

```cpp
List<int> numbers = new List<int>();

numbers.Add(1);
numbers.Add(2);
numbers.Add(3);
numbers.Add(4);

int index = numbers.Count - 1;
while (index >= 0)
{
  int number = numbers[index];
  Console.WriteLine(number);
  index = index - 1;
}
```

```console
4
3
2
1
```

Kokeile toteuttaa edellinen esimerkki for-silmukalla!

## Listan iterointi For-Each -silmukalla

Jos ei ole tarvetta pitää kirjaa indeksistä, jolla ollaan menossa listan arvoja läpi käydessä, voidaan käyttää **for-each** -silmukkaa. Se eroaa edellisistä silmukoista siinä, että siinä ei ole erillistä ehtoa toistolle tai inkrementaatiolle.

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

foreach (string teacher in teachers)
{
  Console.WriteLine(teacher);
}
```

Käytännössä, for-each -silmukka kätkee osan for-silmukosta, jota harjoittelimme aiemmin. For-each -silmukka näyttäisi tältä, jos se toteutettaisiin for-silmukkana:

```cpp
List<string> teachers = new List<string>();

teachers.Add("Simon");
teachers.Add("Samuel");
teachers.Add("Ann");
teachers.Add("Anna");

for (int i = 0; i < teachers.Count; i++) 
{
    string teacher = teachers[i];
    Console.WriteLine(teacher);
}
```

Käytännössä for-each -silmukka tarkastelee listan arvoja yksi kerrallaan. Lausekkeessa **foreach (muuttujaTyyppi muuttujaNimi in listanNimi)**, **muuttujaTyyppi** on listan elementin tyyppi, ja **muuttujaNimi** on muuttuja, joka käytetään listan arvon tallentamiseen, kun käydään sitä läpi.

## Listasta poistaminen ja arvon olemassaolon tarkistaminen

Listan metodi **RemoveAt(index)** poistaa parametrina annetussa indeksissä olevan arvon. Parametrina annetaan kokonaisluku.


```cpp
// luo lista merkkijonoja varten
List<string> list = new List<string>();

// lisää listaan kolme arvoa
list.Add("First");
list.Add("Second");
list.Add("Third");

// poista arvo indeksistä 1
list.RemoveAt(1);

// hae arvot indekseistä 0 ja 1 ja tulosta ne
Console.WriteLine(list[0]);
Console.WriteLine(list[1]);
```

```console
First
Third
```

Voimme myös käyttää metodia **Remove**, jos tiedämme poistettavan arvon:

```cpp
// luo lista merkkijonoja varten
List<string> list = new List<string>();

// lisää listaan kolme arvoa
list.Add("First");
list.Add("Second");
list.Add("Third");

// poista arvo jonka sisältö on "Second"
list.Remove("Second");

// hae arvot indekseistä 0 ja 1 ja tulosta ne
Console.WriteLine(list[0]);
Console.WriteLine(list[1]);
```

```console
First
Third
```

Metodi toimii täsmälleen samoin numeroilla, joten ole varovainen mitä metodia käytät!

```cpp
// luo lista kokonaislukuja varten
List<int> list = new List<int>();

// lisää listaan kolme arvoa
list.Add(1);
list.Add(3);
list.Add(2);

// poista arvo indeksistä 1
list.RemoveAt(1);

// hae arvot indekseistä 0 ja 1 ja tulosta ne
Console.WriteLine(list[0]);
Console.WriteLine(list[1]);
```

```console
1
2
```

```cpp
// luo lista kokonaislukuja varten
List<int> list = new List<int>();

// lisää listaan kolme arvoa
list.Add(1);
list.Add(3);
list.Add(2);

// poista arvolla
list.Remove(1);

// hae arvot indekseistä 0 ja 1 ja tulosta ne
Console.WriteLine(list[0]);
Console.WriteLine(list[1]);
```

```console
3
2
```

<Note> 
Metodi Remove poistaa ensimmäisen osuman jonka se löytää. Eli jos listassasi on monta alkiota samalla arvolla, vain ensimmäinen poistetaan!
</Note>

Listan metodia **Contains** voidaan käyttää tarkistamaan arvon olemassaoloa listassa. Metodi saa parametrinaan arvon, jota etsitään, ja se palauttaa boolean-tyyppisen arvon (True tai False), joka kertoo, löytyikö arvo listasta vai ei.

```cpp
// luo lista merkkijonoja varten
List<string> list = new List<string>();

// lisää listaan kolme arvoa
list.Add("First");
list.Add("Second");
list.Add("Third");

Console.WriteLine("Can we find First: " + list.Contains("First"));


if (list.Contains("Second"))
{
  Console.WriteLine("We found second!");
}
```

```console
Can we find First: True
We found second!
```

## Lista metodin parametrina

Kuten muitakin muuttujia, myös listoja voidaan käyttää metodien parametreina. Kun metodi määritellään ottamaan listan parametrina, parametrin tyyppi määritellään listan tyypiksi ja listassa olevien arvojen tyypiksi. Alla olevassa esimerkissä metodi **Print** tulostaa listan arvot yksi kerrallaan.


```cpp
public static void Print(List<String> list)
{
  foreach (string value in list)
  {
    Console.WriteLine(value);
  }
}
```

Olemme jo tottuneet metodeihin, ja se toimii samalla tavalla tässäkin. Alla olevassa esimerkissä käytämme yllä määriteltyä metodia.

```cpp
List<string> strings = new List<string>();

strings.Add("First");
strings.Add("Second");
strings.Add("Third");

Print(strings);
```

```console
First
Second
Third
```

Valittu parametri metodin määrittelyssä ei ole riippuvainen listasta, joka annetaan parametrina metodin kutsussa. Ohjelmassa, joka kutsuu Print-metodia, listamuuttujan nimi on **strings**, mutta metodissa Print muuttujan nimi on **list** -- muuttujan nimi, joka tallentaa listan, voisi olla myös **printables**.

On myös mahdollista määritellä useita muuttujia metodin parametreiksi. Esimerkissä metodi saa kaksi parametria: listan numeroita ja raja-arvon. Metodi tulostaa kaikki listan luvut, jotka ovat pienempiä kuin toinen parametri.

```cpp
public static void PrintSmallerThan(List<int> numbers, int threshold) 
{
  foreach(int number in numbers)
  {
    if (number < threshold) 
    {
      Console.WriteLine(number);
    }
  }
}
```

Tässä näemme sen toiminnassa:

```cpp
List<int> list = new List<int>();

list.Add(1);
list.Add(2);
list.Add(3);
list.Add(2);
list.Add(1);

PrintSmallerThan(list, 3);
```

```console
1
2
2
1
```

Kuten aiemminkin, metodi voi myös palauttaa arvon. Metodille, joka palauttaa arvon, määritellään palautettavan arvon tyypin kohdalle **void** -sanan sijaan, ja itse palauttaminen tapahtuu **return** -käskyllä. Alla oleva metodi palauttaa listan Countin.


```cpp
public static void Count(List<string> list)
{
  return list.Count;
}
```

Voit myös määrittää omia muuttujia metodeille. Alla oleva metodi laskee listan arvojen keskiarvon. Jos lista on tyhjä, se palauttaa luvun -1.


```cpp
public static double Average(List<int> numbers) 
{
  if (numbers.Count == 0) 
  {
      return -1.0;
  }

  int sum = 0;
  foreach(int number in numbers) 
  {
      sum = sum + number;
  }

  return 1.0 * sum / numbers.Count;
}
```

## Listan kopioiminen metodin parametriksi

Aiemmin olemme käyttäneet kokonaislukuja, liukulukuja jne. metodien parametreina. Kun muuttujia, kuten int, käytetään metodin parametreina, muuttujan arvo kopioituu metodin käyttöön. Sama tapahtuu, kun parametrina on lista.

Listat, kuten käytännössä kaikki muuttujat jotka voivat tallentaa suuria määriä tietoa, ovat viittaus-tyyppisiä muuttujia. Tämä tarkoittaa, että muuttujan arvo on viittaus, joka osoittaa paikkaan, jossa tieto sijaitsee.

Kun lista (tai mikä tahansa viittaus-tyyppinen muuttuja) kopioidaan metodin käyttöön, metodi saa listan arvon, eli viittauksen. Tämä tarkoittaa, että **metodi saa viittauksen muuttujan todelliseen arvoon**. Metodi voi muuttaa alkuperäisen muuttujan arvoa. Käytännössä lista, joka annetaan metodin parametrina, on sama lista, jota käytetään ohjelmassa, joka kutsuu metodia.

Katsotaan tätä nopeasti seuraavassa metodissa.


```cpp
public static void RemoveFirst(List<int> numbers)
{
if (numbers.Count == 0)
{
return;
}
numbers.RemoveAt(0);
}
```

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
numbers.Add(2);
numbers.Add(6);
numbers.Add(-1);

Console.WriteLine("First print: ");
numbers.ForEach(Console.WriteLine);

RemoveFirst(numbers);

Console.WriteLine("Second print: ");
numbers.ForEach(Console.WriteLine);

RemoveFirst(numbers);
RemoveFirst(numbers);
RemoveFirst(numbers);

Console.WriteLine("Third print: ");
numbers.ForEach(Console.WriteLine); // Lyhyempi tapa tehdä listan forEach
```

```console
First print: 
3
2
6
-1
Second print: 
2
6
-1
Third print: 
```

Kuten näkyy, metodi **RemoveFirst** vaikuttaa suoraan listaan, joka annetaan parametrina. 


<Note>
Sen sijaan että käyttäisimme Console.WriteLine(numbers) saadaksemme arvot listasta, käytämme annotaatiota numbers.ForEach(Console.WriteLine);
</Note>

## Yhteenveto listan metodeista ja ominaisuuksista

Löydät kaiken mahdollisen tiedon [**Listoista täältä**](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-7.0). Suurimman osan ajasta emme tarvitse kaikkea tätä tietoa, vaan valikoidun osan siitä.

* Listalle lisääminen tapahtuu **Add** -metodilla, joka saa parametrina lisättävän arvon.

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
```

* Listan alkioiden määrän saa selville **Count** -ominaisuudella, joka palauttaa kokonaisluvun.


```cpp
List<int> numbers = new List<int>();
int amount = numbers.Count;
Console.WriteLine("Amount of integers in numbers: " + amount);
```
* Voit hakea arvon tietystä indeksistä **list[index]** -lausekkeella, jolle annetaan haluttu indeksi parametrina.


```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
Console.WriteLine(numbers[0]);
```

* Alkion poistaminen tehdään joko **Remove** tai **RemoveAt** -metodilla, riippuen siitä, poistetaanko arvolla vai indeksillä.

```cpp
List<string> list = new List<string>();
list.Add("First");
list.Add("Second");
list.Add("Third");
list.RemoveAt(0);
list.Remove("Third");
```

* Tarkistaaksemme löytyykö arvo listalta, käytämme **Contains** -metodia, joka saa parametrina arvon, jota etsitään. Metodi palauttaa boolean-arvon.

```cpp
List<string> list = new List<string>();
list.Add("First");
list.Contains("First");
```

* Listan iteroimiseen voidaan käyttää **forEach**

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
numbers.Add(2);

numbers.ForEach(Console.WriteLine);
```

# Tehtävät

<Exercise title={'001 Third from list'}>
Tehtävässä on pohja ohjelmalle, joka lukee käyttäjältä merkkijonoja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää tyhjän merkkijonon. Ohjelma tulostaa listan ensimmäisen alkion.

Tehtävänäsi on muokata ohjelmaa siten, että tulostetaan ensimmäisen alkion sijaan kolmas alkio. Muista, että ohjelmoijat aloittavat laskemisen nollasta! Ohjelma saa toimia väärin, jos listalla on vähemmän kuin kolme alkiota, joten sinun ei tarvitse varautua sellaiseen tilanteeseen ollenkaan.

```console
> Tom 
> Emma 
> Alex 
> Mary
>
Alex
```

```console
> Emma 
> Alex 
> Mary
>

Mary
```

</Exercise>

<Exercise title={'002 Sum of second and third'}>

Ohjelmapohjassa on ohjelma, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun 0. Ohjelma tulostaa listan ensimmäisen arvon.

Muokkaa ohjelmaa siten, että tulostetaan toisen ja kolmannen luvun summa.  Ohjelma saa toimia väärin, jos listalla on vähemmän kuin kolme alkiota, joten sinun ei tarvitse varautua sellaiseen tilanteeseen ollenkaan.

```console
> 1 
> 3 
> 5 
> 7 
> 0 
8
```

```console
> 2 
> 3 
> 4 
> 0 
7
```

</Exercise>

<Exercise title={'003 Exception'}>

Tehtäväpohjassa on ohjelma joka käyttää listaa. Muokkaa sitä siten, että ohjelma aiheuttaa poikkeuksen `ArgumentOutOfRangeException` aina kun sitä suoritetaan. Käyttäjän ei pitäisi antaa syötettä ohjelmalle (esim. kirjoittamalla jotain näppäimistöllä).

</Exercise>

<Exercise title={'004 Counting names'}>

Tehtäväpohjassa on ohjelma joka lukee käyttäjältä merkkijonoja ja lisää ne listalle. Muokkaa sen toimintaa siten, että lopettaessaan lukemisen (antamalla tyhjän syötteen), ohjelma tulostaa listalla olevien alkioiden määrän.


```console
> Tom 
> Emma 
> Alex 
> Mary
>
In total: 4
```

```console
> Juno 
> Elizabeth 
> Mason 
> Irene
> Olivia
> Liam
> Ida
> Christopher
> Mark
> Sylvester
> Oscar
>
In total: 11
```

<Note>
Muista käyttää listan Count-ominaisuutta.
</Note>

</Exercise>

<Note>
Seuraavien tehtävien tarkoituksena on oppia käyttämään listoja ja indeksejä. Vaikka tehtävät voisi tehdä ilman listoja, keskity harjoittelemaan listojen käyttöä. Tehtävien toiminnallisuus on toteutettava syötteiden lukemisen jälkeen.
</Note>

<Exercise title={'005 Last from list'}>

Tehtäväpohjassa on ohjelma, joka lukee käyttäjältä merkkijonoja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää tyhjän merkkijonon.

Tehtävänäsi on muokata ohjelmaa siten, että tulostetaan viimeisenä luettu merkkijono. Tulosta arvo lukemalla listan viimeisen alkion arvo. Count auttaa tässä. Sinun ei tarvitse huomioida tyhjää listaa, voit olettaa että käyttäjä antaa ainakin yhden syötteen.


```console
> Tom 
> Emma 
> Alex 
> Mary
>
Mary
```

```console
> Juno 
> Elizabeth 
> Mason 
> Irene
> Olivia
> Liam
> Ida
> Christopher
> Mark
> Sylvester
> Oscar
>
Oscar
```

</Exercise>

<Exercise title={'006 First and last'}>

Tehtäväpohjassa on ohjelma, joka lukee käyttäjältä merkkijonoja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää tyhjän merkkijonon.

Muokkaa ohjelmaa siten, että tulostetaan ensimmäinen ja viimeinen luettu merkkijono. Voit olettaa että käyttäjä antaa ainakin kaksi syötettä.

```console
> Tom 
> Emma 
> Alex 
> Mary
>
Tom
Mary
```

```console
> Juno 
> Elizabeth 
> Mason 
> Irene
> Olivia
> Liam
> Ida
> Christopher
> Mark
> Sylvester
> Oscar
>
Juno
Oscar
```

```console
> Tom 
> Mary
>
Tom
Mary
```

</Exercise>

<Exercise title={'007 Numbers from list'}>

Tehtäväpohja sisältää ohjelman, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun -1.

Laajenna toiminnallisuutta siten, että ohjelma tulostaa kaikki luetut luvut. Lukua, joka käytetään lopettamiseen, ei tulosteta.


```console
> 72
> 2
> 8
> 11
> -1 
72
2
8
11
```

</Exercise>

<Exercise title={'008 Numbers from and to'}>

Tehtäväpohja sisältää ohjelman, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun -1.

Laajenna toiminnallisuutta siten, että käyttäjältä kysytään alku- ja loppuarvot kun numeroiden kysyminen on lopetettu. Tämän jälkeen ohjelma tulostaa kaikki luetut luvut, jotka ovat annetulla välillä (molemmat rajat mukaan lukien). Voit olettaa, että käyttäjä antaa vähintään yhden luvun, joka on annetulla välillä.


```console
> 72
> 2
> 8
> 11
> -1 
From where?
> 1
Where to?
> 9 
2 
8
```

```console
> 72
> 8
> 2
> 11
> -1 
From where?
> 0 
Where to?
> 20  
8
2
11 
```

</Exercise>

<Exercise title={'009 Greatest number'}>

Tehtäväpohja sisältää ohjelman, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun -1.

Jatketaan ohjelman kehittämistä siten, että ohjelma tulostaa listalla olevista luvuista suurimman. Ohjelman tulisi toimia seuraavasti.


```console
> 72
> 2
> 8
> 93
> 11
> -1
The greatest number: 93
```

Voit olettaa, että käyttäjä antaa ainakin yhden luvun, joka on suurempi kuin -1.

Voit käyttää seuraavaa koodia inspiraationa. Se etsii listan pienimmän luvun.


```cpp
// Oletetaan että meillä on lista kokonaislukuja

int smallest = list[0];

for(int i = 0; i < list.Count; i++) {
    int number = list[i];
    if (smallest > number) {
        smallest = number;
    }
}

Console.WriteLine("The smallest number: " + smallest);
```

</Exercise>

<Exercise title={'010 Index'}>

Tehtäväpohja sisältää ohjelman, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun -1.

Laajennetaan toiminnallisuutta siten, että ohjelma kysyy käyttäjältä lukua. Ohjelma tulostaa listalla olevien lukujen indeksin, joka vastaa käyttäjän antamaa lukua. Jos lukua ei löydy, ohjelma ei tulosta mitään.

<Note>Numero voi esiintyä useamminkin kuin kerran</Note>

```console
> 72 
> 2 
> 8 
> 8 
> 11 
> -1
Search for? 
> 2 
2 is at index 1
```

```console
> 72 
> 2 
> 8 
> 8 
> 11 
> -1
Search for? 
> 8 
8 is at index 2
8 is at index 3
```

</Exercise>

<Exercise title={'011 Smallest and index'}>

Luo ohjelma joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun 9999. Tämän jälkeen ohjelma tulostaa listalla olevista luvuista pienimmän sekä kaikki indeksit, joissa pienin luku esiintyy. 

<Note>Pienin numero voi esiintyä useamminkin kuin kerran</Note>


```console
> 72
> 2
> 8
> 8
> 11
> 9999
Smallest number: 2 
Found at index: 1
```

```console
> 72
> 44
> 8
> 8
> 11
> 9999
Smallest number: 8 
Found at index: 2 
Found at index: 3
```

<Note> 
Voit aiempia tehtäviä inspiraationa, yhdistämällä niiden toiminnallisuutta. Etsi ensin pienin numero, sen jälkeen sen kaikki indeksit.
</Note>

</Exercise>

<Exercise title={'012 Sum of list'}>

Tehtäväpohja sisältää ohjelman, joka lukee käyttäjältä kokonaislukuja ja lisää ne listalle. Lukeminen lopetetaan kun käyttäjä syöttää luvun -1.


Muokkaa ohjelmaa siten, että ohjelma tulostaa listalla olevien lukujen summan.

```console
> 72
> 2
> 8
> 11
> -1
Sum: 93
```

</Exercise>

<Exercise title={'013 Finding names'}>

Tehtäväpohjassa on ohjelma, joka lukee käyttäjältä merkkijonoja kunnes käyttäjä syöttää tyhjän merkkijonon. Lisää seuraava toiminnallisuus: ohjelma kysyy käyttäjältä vielä yhtä merkkijonoa. Ohjelma kertoo käyttäjälle, löytyikö merkkijono listalta vai ei.


```
> Tom
> Emma
> Alex
> Mary
Search for?
> Mary
Mary was found!
```

```
> Tom
> Emma
> Alex
> Mary
Search for?
> Logan
Logan was not found!
```

</Exercise>

<Exercise title={'014 Numbers in range'}>

Luo metodi `public static void PrintNumbersInRange(List<int> numbers, int lowerLimit, int upperLimit)` tehtäväpohjaan. Metodi tulostaa listan luvut, joiden arvot ovat annetulla välillä [lowerLimit, upperLimit]. Muutama esimerkki metodin käytöstä on annettu alla.

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
numbers.Add(2);
numbers.Add(6);
numbers.Add(-1);
numbers.Add(5);
numnbers.Add(1);

Console.WriteLine("The numbers in the range [0, 5]");
PrintNumbersInRange(numbers, 0, 5);

Console.WriteLine("The numbers in the range [3, 10]");
PrintNumbersInRange(numbers, 3, 10);
```

```console
The numbers in the range [0, 5] 
3 
2 
5 
1 
The numbers in the range [3, 10] 
3 
6 
5
```

</Exercise>

<Exercise title={'015 Sum method'}>

Luo metodi `public static int Sum(List<int> numbers)` tehtäväpohjaan. Metodin tulisi palauttaa parametrina annetun listan lukujen summa.


```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
numbers.Add(2);
numbers.Add(6);
numbers.Add(-1);
Console.WriteLine(Sum(numbers));

numbers.Add(5);
numbers.Add(1);
Console.WriteLine(Sum(numbers));
```

```console
10
16
```

</Exercise>

<Exercise title={'016 Remove last method'}>

Luo metodi `public static void RemoveLast(List<string> strings)` tehtäväpohjaan. Metodin tulisi poistaa parametrina annetun listan viimeinen arvo. Jos lista on tyhjä, metodi ei tee mitään.

```cpp
List<string> strings = new List<string>();

strings.Add("First");
strings.Add("Second");
strings.Add("Third");

// Muista, tällä tavoin voi tulostaa listan kaikkien alkioiden arvot
strings.ForEach(Console.WriteLine);

RemoveLast(strings);
RemoveLast(strings);

strings.ForEach(Console.WriteLine);
```

```console
First
Second
Third
First
```

</Exercise>
