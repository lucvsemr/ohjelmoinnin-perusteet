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

lista.add("First");
Console.WriteLine("Number of values on the list: " + list.Count);

int values = list.Count;

lista.add("Second");
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


Like other variables, a list, too, can be used as a parameter to a method. When the method is defined to take a list as a parameter, the type of the parameter is defined as the type of the list and the type of the values contained in that list. Below, the method **Print** prints the values in the list one by one.

```cpp
public static void Print(List<String> list)
{
  foreach (string value in list)
  {
    Console.WriteLine(value);
  }
}
```

We're by now familiar with methods, and it works in the same way here. In the example below we use the method that was implemented above.

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

The chosen parameter in the method definition is not dependent on the list that is passed as parameter in the method call. In the program that calls Print, the name of the list variable is **string**, but inside the method Print the variable is called **list** -- the name of the variable that stores the list could also be **printables**, for instance.

It's also possible to define multiple variables for a method. In the example the method receives two parameters: a list of numbers and a threshold value. It then prints all the numbers in the list that are smaller than the second parameter.

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

Here we see it in action:

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

As before, a method can also return a value. The methods that return values have the type of the return value in place of the **void** keyword, and the actual returning of the value is done by the **return** command. The method below returns the Count of the list.

```cpp
public static void Count(List<string> list)
{
  return list.Count;
}
```

You can also define own variables for methods. The method below calculates the average of the numbers in the list. If the list is empty, it returns the number -1.

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
## On Copying the List to a Method Parameter

Earlier we have used integers, floating point numbers, etc. as method parameters. When variables such as int are used as method parameters, the value of the variable is copied for the method's use. The same occurs in the case that the parameter is a list.

Lists, among practically all the variables that can store large amounts of information, are reference-type variables. This means that the value of the variable is a reference that points to the location that contains the information.

When a list (or any reference-type variable) is copied for a method's use, the method receives the value of the list variable, i.e., a reference. In such a case the **method receives a reference to the real value of a reference-type variable**, and the method is able to modify the value of the original reference type variable, such as a list. In practice, the list that the method receives as a parameter is the same list that is used in the program that calls the method.

Let's look at this briefly with the following method.

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
numbers.ForEach(Console.WriteLine);
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

As you can see, the methor **RemoveFirst** affects the list it was given as a parameter, directly.

<Note>Instead of doing Console.WriteLine(numbers), to get the values from the list, the annotation is numbers.ForEach(Console.WriteLine); </Note>

## A Summary of List Methods and Properties

You can find all the information about [**Lists here**](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=netframework-4.8). For the most part, we don't need all that information, but a hand selected part from it.

* Adding to a list is done with the method *Add** that receives the value to be added as a parameter.

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
```

* The number of elements in a list can be discovered with the property **Count**; it returns an integer.

```cpp
List<int> numbers = new List<int>();
int amount = numbers.Count;
Console.WriteLine("Amount of integers in numbers: " + amount);
```

* You can retrieve a value from a certain index with the method **list[index]** that is given the index at which the value resides as a parameter.

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
Console.WriteLine(numbers[0]);
```

* Removing elements is done with either **Remove** or **RemoveAt**, depending if we remove by value or index.

```cpp
List<string> list = new List<string>();
list.Add("First");
list.Add("Second");
list.Add("Third");
list.RemoveAt(0);
list.Remove("Third");
```

* Checking for the existence of a value is done with the method **Contains**. It's provided the value being searched for as a parameter, and it returns a boolean value.

```cpp
List<string> list = new List<string>();
list.Add("First");
list.Contains("First");
```

* To iterate a list, we use forEach

```cpp
List<int> numbers = new List<int>();
numbers.Add(3);
numbers.Add(2);

numbers.ForEach(Console.WriteLine);
```

# Tehtävät

<Exercise title={'001 Third from list'}>
The exercise contains a base that asks the user for strings and adds them to a list. The program stops reading when the user enters an empty string. The program then prints the first element of the list.

Your assignment is to modify the program so that instead of the first value, the third value on the list is printed. Remember that programmers start counting from zero! The program is allowed to malfunction if there are fewer than three entries on the list, so you don't need to prepare for such an event at all.

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

In the exercise template there is a program that reads integers from the user and adds them to a list. This ends when the user enters 0. The program then prints the first value on the list.

Modify the program so that instead of the first value, the program prints the sum of the second and third numbers. The program is allowed to malfunction if there are fewer than three entries on the list, so you don't need to prepare for such an event at all.

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

There is a program that uses a list in the exercise template. Modify it so that its execution always produces the error `ArgumentOutRangeException`. The user should not have to give any inputs to the program (e.g. write something on the keyboard)

</Exercise>

<Exercise title={'004 Counting names'}>

In the exercise template is a program that reads input from the user. Modify its working so that when the program quits reading (with an empty line), the program prints the number of values on the list.

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

<Note>Be sure to use the Count property of the list.</Note>

</Exercise>

<Note>The next exercises are meant for learning to use lists and indices. Even if you could complete the execises without a list, concentrate on training to use lists. The functionality in the exercises is to be implemented after reading the inputs.</Note>

<Exercise title={'005 Last from list'}>

In the exercise template there is a program that reads inputs from the user and adds them to a list. Reading is stopped once the user enters an empty string.

Your task is to modify the method to print the last read value after it stops reading. Print the value that was read last from the list. Use the Count to help you. You do not have to take into consideration empty lists, you can assume that the user always gives at least one input.

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

In the exercise template there is a program that reads inputs from the user and adds them to a list. Reading is stopped once the user enters an empty string.

Modify the program to print both the first and the last values after the reading ends. You may suppose that at least two values are read into the list.

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

The exercise template contains a base that reads numbers from the user and adds them to a list. Reading is stopped once the user enters the number -1.

Expand the functionality of the program so that after reading the numbers, it prints all the numbers received from the user. The number used to indicate stopping should not be printed.

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

The exercise template contains a base that reads numbers from the user and adds them to a list. Reading is stopped once the user enters the number -1.

Expand the program to ask for a start and end values once it has finished asking for numbers. After this the program shall prints all the numbers in the list that fall in the specified range (between the values given by the user, inclusive). You may assume that the user gives values that match some numbers in the list.

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

The exercise template contains a base that reads numbers from the user and adds them to a list. Reading is stopped once the user enters the number -1.

Continue developing the program so that it ends the greatest number in the list and prints its value after reading all the numbers. The programming should work in the following manner.

```console
> 72
> 2
> 8
> 93
> 11
> -1
The greatest number: 93
```
You can assume that user always gives atleast one viable number.

You can use the source code below as an inspitation. It is used to find the smallest number.

```cpp
// assume we have a list that contains integers

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

The exercise template contains a base that reads numbers from the user and adds them to a list. Reading is stopped once the user enters the number -1.

Expand the program that then asks the user for a number, and reports that number's index in the list. If the number is not found, the program should not print anything.

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

Write a program that reads numbers from the user. When number 9999 is entered, the reading process stops. After this the program will print the smallest number in the list, and also the indices where that number is found. Notice: the smallest number can appear multiple times in the list.

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

<Note> You can combine the programs you wrote for the exercises "Greatest number in the list" and "Index of the requested number". First find the smallest number, and then find the index of that number. </Note>

</Exercise>

<Exercise title={'012 Sum of list'}>

The exercise template contains a base that reads numbers from the user and adds them to a list. Reading is stopped once the user enters the number -1.

Modify the program so that after reading the numbers it calculates and prints the sum of the numbers in the list.

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

In the exercise template there is a program that reads inputs from the user until an empty string is entered. Add the following functionality to it: after reading the inputs one more string is requested from the user. The program then tell whether that string was found in the list or not.

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

Create the method `public static void PrintNumbersInRange(List<int> numbers, int lowerLimit, int upperLimit)` in the exercise template. The method prints the numbers in the given list whose values are in the range [lowerLimit, upperLimit]. A few examples of using the method are supplied below.

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

Create the method `public static int Sum(List<int> numbers)` in the exercise template. The method is to return the sum of the numbers in the parameter list.

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

create the method `public static void RemoveLast(List<string> strings)` in the exercise template. The method should remove the last value in the list it receives as a parameter. If the list is empty, the method does nothing.

```cpp
List<string> strings = new List<string>();

strings.Add("First");
strings.Add("Second");
strings.Add("Third");

// Remember, this is how you print all the items in a list
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
