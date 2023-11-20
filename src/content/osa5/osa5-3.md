---
title: "Muuttujatyypit"
nav_order: 3
hidden: false
---


On olemassa kahdentyyppisiä muuttujia C#:ssa: **arvomuuttujia** ja **viittausmuuttujia**. Arvomuuttujat sisältävät suoraan arvonsa, kun taas viittausmuuttujat sisältävät viittauksen arvoonsa, joka on **olio** tai **objekti**.

Vittausmuuttujilla on mahdollista, että kaksi muuttujaa viittaavat samaan objektiin, ja siten on mahdollista, että toisen muuttujan operaatiot vaikuttavat toisen muuttujan viittaamaan objektiin.

Arvomuuttujilla jokaisella muuttujalla on oma kopio datasta, eikä toisen muuttujan operaatioilla ole mahdollista vaikuttaa toisen muuttujan arvoon.

Ohjelmoijan näkökulmasta arvomuuttujan data on tallennettu muuttujan arvoksi, kun taas viittausmuuttujan data on viittaus dataan. Tutkitaan näitä eri tyyppejä kahdella esimerkillä.

```cpp
int number = 10;
Console.WriteLine(number);
```

```console
10
```

```cpp
namespace Exercise001
{
  public class Name
  {
    private string name;

    public Name(string name)
    {
      this.name = name;
    }
  }
}
```

```cpp
  Name john = new Name("John");
  Console.WriteLine(john);
```


```console
Exercise001.Name
```

Ensimmäisessä esimerkissä luomme yksinkertaisen **int** muuttujan, ja siihen tallennetaan arvoksi numero 10. Kun välitämme muuttujan **Console.WriteLine** metodille, tulostuu arvo 10. Toisessa esimerkissä luomme **viittausmuuttujan** nimeltä john. Kun kutsutaan **Name** luokan konstruktoria, se tallettaa arvon muuttujan arvoksi. Kun tulostamme muuttujan, tulostuu **Exercise001.Name**. Mikä on syynä tähän?

Metodi **Console.WriteLine** tulostaa muuttujan arvon. Arvomuuttujan arvo on konkreettinen, kun taas viittausmuuttujan arvo on viittaus. Viittausmuuttujan tapauksessa tulostetaan olion **ToString** representaatio. Oletusarvoisesti **Object.ToString** metodi tulostaa olion nimen **namespace.ClassName**, joten saamme **Exercise001.Name**.

Edellinen esimerkki on tapaus, jossa ohjelmoija ei ole muuttanut muuttujan oletustulostusta. Voit muuttaa oletustulostusta määrittelemällä **ToString** metodin kyseisen olion luokassa. Metodi kertoo, mitä merkkijonoa tulostetaan, kun luokan instanssi tulostetaan. Alla olemme määritelleet **public override string ToString()** metodin **Name** luokassa: se palauttaa instanssimuuttujan **name**. Nyt kun tulostamme **Name** luokan instanssin **Console.WriteLine** komennolla, tulostuu **ToString** metodin palauttama merkkijono.


```cpp
namespace Exercise001
{
  public class Name
  {
    private string name;

    public Name(string name)
    {
      this.name = name;
    }

    public override string ToString() {
      return this.name;
    }
  }
}
```

```cpp
Name john = new Name("John");
Console.WriteLine(john);
```

```console
John
```

## Arvomuuttujat

Arvomuuttuja on joko tietue (**struct type**) tai  numeroituva (**enumeration type**). C# tarjoaa joukon esimääriteltyjä tietueita, joita kutsutaan **yksinkertaisiksi tyypeiksi**. Yksinkertaiset tyypit tunnistetaan varattujen sanojen avulla.

Tietyn tyyppinen muuttuja sisältää tyyppinsä instanssin. Tämä eroaa viittausmuuttujasta, joka sisältää viittauksen tyypin instanssiin. Oletuksena arvo kopioidaan kun muuttuja alustetaan, parametri välitetään metodille tai metodin paluuarvo palautetaan. Arvomuuttujan tapauksessa vastaava tyyppi instanssi kopioidaan.

Mielenkiintoisimpia (ja meille tärkeimpiä) ovat **yksinkertaiset tyypit**. Useimmat muuttujat, joita olemme käsitelleet tähän mennessä, ovat osa yksinkertaista tyyppiä: int, bool ja double ovat kaikki yksinkertaisia tyyppejä. Se tarkoittaa, että ne ovat itse asiassa **avainsanoja**, jotka on **varattu** edustamaan tiettyjä tyyppejä **System namespacesta**.

Koska yksinkertaiset tyypit aliasoivat tietueen tyypin, jokaisella yksinkertaisella tyypillä on jäseniä. Esimerkiksi **int** sisältää **System.Int32** ja **System.Object** määrittelemät jäsenet, ja seuraavat lauseet ovat sallittuja:

```cpp
int i = int.MaxValue;    // System.Int32.MaxValue vakio
string s = i.ToString(); // System.Int32.ToString() instanssimetodi
string t = 123.ToString(); // System.Int32.ToString() instanssimetodi
```

Toisinsanottuna, kaikki perusmuuttujat, joita olemme käyttäneet, ovat itse asiassa vain helpompia tapoja käyttää System:sta löytyviä metodeja.

Arvomuuttujan alustaminen varaa tietyn kokoisen alueen tietokoneen muistista. Koko määräytyy muuttujan tyypin mukaan, ja muistipaikka on se paikka, johon muuttujan arvo tallennetaan. Alla olevassa esimerkissä luomme kolme muuttujaa. Jokaisella on oma muistipaikka, johon sille annettu arvo kopioidaan.

```cpp
int first = 10;
int second = first;
int third = second;
Console.WriteLine(first + " " + second + " " + third);
second = 5;
Console.WriteLine(first + " " + second + " " + third);
```

```console
10 10 10
10 5 10
```

Muuttujan nimi kertoo muistipaikan, johon sen arvo on tallennettu. Kun muuttujalle annetaan arvo yhtäsuuruusmerkillä, oikeanpuoleinen arvo kopioidaan muuttujan muistipaikkaan. Esimerkissä **int first = 10** varaa muistipaikan nimeltä **first** ja kopioi siihen arvon 10. Vastaavasti **int second = first** varaa muistipaikan nimeltä **second** ja kopioi siihen arvon, joka on muistipaikassa **first**. Lopuksi **int third = second** varaa muistipaikan nimeltä **third** ja kopioi siihen arvon, joka on muistipaikassa **second**.

Muuttujien arvot kopioidaan myös metodikutsuissa. Käytännössä tämä tarkoittaa sitä, että muuttujan arvoa, joka välitetään metodin parametrina, ei muuteta metodissa, joka kutsuu toista metodia.

## Viittausmuuttujat

C#:n viittaustyyppejä ovat luokka (**class**), rajapinta (**interface**), taulukko (**array**) ja delegaatti (**delegate**).

Viittautyyppisen muuttujan arvo on viittaus sentyyppiseen **instanssiin**, joka on **olio** tai **objekti**. Erityinen arvo **null** on yhteensopiva kaikkien viittaustyyppien kanssa ja ilmaisee instanssin puuttumista. Ohjelmoija voi myös luoda omia muuttujatyyppejä määrittelemällä uusia luokkia. Käytännössä mikä tahansa luokasta instansioitu olio on viittausmuuttuja.

Tarkastellaan taas esimerkkiä, jossa luomme **Name** luokan instanssin nimeltä John.


```cpp
Name john = new Name("John");
```

Kutsu koostuu seuraavista osista:

* Kun uusi muuttuja luodaan, pitää ensin määrittää muuttujan tyyppi. Alla esimerkissä määritämme muuttujan tyypiksi **Name**. Jotta ohjelma voisi suorittaa, pitää **Name** luokan olla saatavilla.


```cpp
Name ...
```

* Muuttujan nimi pitää myös määrittää. Voit myöhemmin käyttää muuttujaa viittaamaan sen arvoon. Alla esimerkissä muuttujan nimi on **john**.

```cpp
Name john ...
```

* Voit tallettaa muuttujaan arvon. Voit luoda instanssin luokasta kutsumalla luokan konstruktoria, joka määrittää instanssimuuttujien arvot sillä hetkellä, kun olio luodaan. Alla oletamme luokan **Name** konstruktorin ottavan merkkijonon parametrina.

```cpp
... new Name("John");
```

* Konstruktorikutsu palauttaa viittauksen luotuun instanssiin. Yhtäsuuruusmerkki kertoo ohjelmalle, että oikeanpuoleinen arvo talletetaan vasemmanpuolimmaiseen muuttujaan. Viittaus vastaluotuun muuttujaan, jonka konstruktorikutsu on palauttanut, kopioidaan muuttujan **john** arvoksi.

```cpp
Name john = new Name("John");
```

Suurin ero arvo- ja viittausmuuttujien välillä on se, että arvomuuttujat ovat (lähes poikkeuksetta) muuttumattomia. Toisaalta viittausmuuttujien sisäistä tilaa voidaan tyypillisesti muuttaa. Tämä ilmiö selittyy sillä, että arvomuuttujan arvo tallennetaan suoraan muuttujaan, kun taas viittausmuuttujan arvo on viittaus muuttujan dataan, eli muuttujan sisäiseen tilaan.

Aritmeettiset operaatiot, kuten yhteen-, vähennys- ja kertolasku, voidaan suorittaa arvomuuttujilla -- nämä operaatiot eivät muuta muuttujan alkuperäistä arvoa. Aritmeettiset lausekkeet luovat uusia arvoja, jotka tallennetaan muuttujiin tarvittaessa. Huomaa, että viittausmuuttujien arvoja ei voida muuttaa näillä aritmeettisillä lausekkeilla.

Viittausmuuttujan arvo, eli itse viittaus, osoittaa muistipaikkaan, jossa muuttujan data on tallennettuna. Oletetaan että meillä on luokka Person käytössä, ja se sisältää instanssimuuttujan age. Jos luokasta on luotu olio, voimme löytää age muuttujan seuraamalla olion viittausta. Tämän age muuttujan arvoa voidaan muuttaa tarvittaessa.

[**Voit lukea lisää muuttujatyypeistä täältä**](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/types). Tämä tiedon kaninkolo on *hyvin syvä* ja saattaa vaatia aikaa ymmärtää.

## Arvomuuttuja tai viittausmuuttuja metodin parametrina

Aiemmin totesimme, että arvomuuttujan arvo on suoraan tallennettu muuttujaan, kun taas viittausmuuttujan arvo on viittaus muuttujan dataan. Totesimme myös, että yhtäsuuruusmerkki kertoo ohjelmalle, että oikeanpuoleinen arvo kopioidaan vasemmalla olevaan muuttujaan.

Samantapainen kopiointi tapahtuu kun metodia kutsutaan. Riippumatta siitä onko muuttuja arvo- vai viittausmuuttuja, sen arvo kopioidaan metodille välitettäessä. Arvomuuttujan tapauksessa arvo kopioidaan suoraan, kun taas viittausmuuttujan tapauksessa viittaus kopioidaan.

Katsotaan käytännön esimerkkiä. Oletetaan että meillä on seuraava **Person** luokka käytössä.

```cpp
public class Person
{
  private string name;
  public int birthYear { get; set; }

  public Person(string name)
  {
    this.name = name;
    this.birthYear = 1970;
  }

  public override string ToString()
  {
    return this.name + " (" + this.birthYear + ")";
  }
}
```

Katsotaan ohjelman toimintaa askel askeleelta.


```cpp
static void Main(string[] args)
{

  Person first = new Person("First");

  Console.WriteLine(first);
  MakeYounger(first);
  Console.WriteLine(first);

  Person second = first;
  MakeYounger(second);

  Console.WriteLine(first);
}

public static void MakeYounger(Person person)
{
  person.birthYear++;
}
```

```console
First (1970)
First (1971)
First (1972)
```

Ohjelman suoritus alkaa **Main** metodin ensimmäiseltä riviltä. Ensimmäisellä rivillä esitellään **Person** tyyppinen muuttuja **first**, ja **Person** luokan konstruktorin palauttama arvo kopioidaan sen arvoksi. Konstruktori luo olion, jonka syntymävuosi on 1970, ja nimi on saatu parametrina. Ensimmäisen rivin suorituksen jälkeen ohjelman tilanne on seuraava -- muistiin on luotu **Person** tyyppinen olio, ja **Main** metodissa on viittaus siihen ensimmäisessä muuttujassa.


![Ensimmäinen askel kuvana](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/part5-3-first-1-tm.png)

Metodin kolmannella rivillä tulostamme muuttujan first arvon. Metodikutsu **Console.WriteLine** etsii parametrina annetusta viittausmuuttujasta **ToString** metodin. **Person** luokalla on **ToString** metodi, joten se kutsutaan ensimmäisen muuttujan osoittaman olion kohdalla. Olion name muuttujan arvo on "First", ja syntymävuoden arvo on 1970. Tulostettava merkkijono on "First (1970)".

Neljännellä rivillä ohjelma kutsuu **MakeYounger** metodia, ja sille välitetään parametrina muuttuja **first**. Kun **MakeYounger** metodia kutsutaan, sille välitetyn muuttujan arvo kopioidaan metodin käyttöön. **MakeYounger** metodin suorituksen aikana **Main** metodin suoritus jää odottamaan kutsupinon päälle. Koska muuttuja first on viittausmuuttuja, aiemmin luotu viittaus kopioidaan metodin käyttöön. Metodin suorituksen lopussa tilanne on seuraava -- metodi lisää yhdellä parametrina saamansa olion syntymävuotta.

![Toinen askel kuvana](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/part5-3-first-2-tm.png)

Kun metodin MakeYounger suoritus päättyy, palaamme Main metodiin. Metodin MakeYounger suorituksen aikana tehdyt muutokset katoavat kutsupinon päältä.


![Askel kolme](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/part5-3-first-3-tm.png)

Kun palataan Main metodiin, tulostetaan vielä muuttujan first arvo. Olio, johon first muuttuja viittaa, on muuttunut MakeYounger metodin suorituksen aikana -- olion syntymävuosi on lisääntynyt yhdellä. Tulostettava merkkijono on "First (1971)".

Tämän jälkeen ohjelma esittelee uuden muuttujan **second**. Muuttujan arvoksi kopioidaan muuttujan first arvo. Toisin sanoen, muuttujan second arvo on viittaus samaan olioon kuin muuttujan first arvo. 
Then the program introduces a new Person type variable called second. The value of the variable first is copied into the variable second: in other words, the value of the variable second is a reference to the already existing Person object.

![Askel neljä](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/part5-3-first-4-tm.png)


Tämän jälkeen ohjelma kutsuu MakeYounger metodia, ja sille välitetään parametrina muuttuja second. Metodin suorituksen aikana muuttujan second arvo kopioidaan metodin käyttöön. Metodin suorituksen lopussa tilanne on seuraava -- metodi lisää yhdellä parametrina saamansa olion syntymävuotta.

![Askel viisi](https://github.com/centria/ohjelmoinnin-perusteet/raw/master/src/images/part5-3-first-5-tm.png)

Lopulta metodin suoritus loppuu ja palaamme Main metodiin. Tulostamme vielä muuttujan first arvon. Tulostettava merkkijono on "First (1972)".

Materiaalissa esitetyt yksityiskohdat muuttujista ja tietokoneen muistista ovat yksinkertaistettuja. Esittelemme muistia koskevia asioita sopivalla abstraktiotasolla ohjelmoinnin oppimisen kannalta. Esimerkiksi kurssin tavoitteiden kannalta seuraava lause on riittävä: **lause int number = 5** varaa **muistista** **paikan** muuttujalle number, ja **kopioi siihen arvon 5**.

Tietokoneen toiminnan kannalta, lauseen int number = 5 suorituksen aikana tapahtuu paljon enemmän. Suoritus vaatii 32-bittisen muistipaikan varaamisen arvolle 5, ja toisen 32-bittisen muistipaikan varaamisen muuttujalle number. Muistipaikan koko määräytyy muuttujan tyypin mukaan. Tämän jälkeen muistipaikassa, jossa on arvo 5, oleva data kopioidaan muuttujan number muistipaikkaan.

Tämän lisäksi, muuttuja number ei ole suoraan muistipaikka tai laatikko, johon tietoa säilötään. Muuttujan arvo on muistipaikan osoite, jossa tieto sijaitsee. Muuttujan tyyppi, joka sisältyy muuttujaan itseensä, kertoo kuinka paljon dataa tulee hakea osoitteesta. Esimerkiksi kokonaisluvun (int) tapauksessa tarvittava määrä on 32 bittiä.
