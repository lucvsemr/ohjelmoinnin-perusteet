---
title: 'Metodit'
nav_order: 3
hidden: false
---

Ruudulle tulostaminen ja lukeminen on tehty **Console.WriteLine()** -käskyllä ja lukeminen **Console.ReadLine()** -käskyllä. Ehtolauseet ovat käyttäneet **if** -rakennetta, toistolauseet **while** - ja **for** -rakenteita. Huomaamme, että tulostaminen ja lukeminen eroavat hieman **if** -, **while** - ja **for** -rakenteista; tulostamis- ja lukemiskäskyt päättyvät sulkeisiin, ja välillä sulkeissa on myös käskyn parametreja. Nämä sulkeisiin päättyvät käskyt eivät ole varsinaisesti käskyjä, vaan metodeja.

Teknisesti ottaen, **metodi** on nimetty joukko lauseita - osa ohjelmaa, jota voidaan kutsua muualta ohjelmakoodista käyttämällä metodin nimeä. Esimerkiksi koodirivi

```cpp
Console.WriteLine("I am a parameter given to a method!");
```

kutsuu metodia joka käsittelee ruudulle tulostamista. Metodin sisäinen rakenne -- eli miten metodin kutsun yhteydessä annettu käskyjoukko suoritetaan -- on piilotettu, eikä ohjelmoijan tarvitse sitä käyttäessään tietää.

Tähän mennessä kaikki metodit joita olemme käyttäneet ovat olleet C#:n valmiita metodeja. Seuraavaksi opimme luoman omia metodeja.


## Omat metodit

Metodi tarkoittaa nimettyä joukkoa lauseita, jota voidaan kutsua muualta ohjelmakoodista sen nimellä. Ohjelmointikielten mukana tulee valmiita metodeja, mutta ohjelmoija voi myös kirjoittaa omiaan. Olisi itse asiassa melko erikoista, jos ohjelma ei käyttäisi lainkaan ohjelmoijan kirjoittamia metodeja, sillä metodit auttavat ohjelman rakenteen hahmottamisessa. Tästä eteenpäin lähes jokainen kurssilla tehtävä ohjelma sisältää siis ohjelmoijan kirjoittamia metodeja.

Koodin mallipohjassa metodit on kirjoitettu **Main** -metodin aaltosulkujen ulkopuolelle, mutta uloimpien aaltosulkujen sisälle. Ne voivat sijaita joko **Main** -metodin ylä- tai alapuolella.

```cpp
using System;

public class Program
{
  public static void Main(string[] args)
  {
      // Tänne tulisi koodia
  }

  // Omat metodit ovat täällä
}
```

Tarkastellaan uuden metodin luomista. Luodaan metodi **Greet**.

```cpp
public static void Greet()
{
  Console.WriteLine("Greetings from the method world!");
}
```

Ja laitetaan se metodille sopivaan paikkaan.


```cpp
using System;

public class Program
{
    public static void Main(string[] args)
    {
        // Tänne tulisi koodia
    }

    // Omat metodit ovat täällä
    public static void Greet()
    {
      Console.WriteLine("Greetings from the method world!");
    }
}
```

Metodin määritelmä koostuu kahdesta osasta. Ensimmäisen rivi sisältää metodin nimen, eli **Greet**. Nimen vasemmalla puolella ovat avainsanat **public static void**. Nimen alla on aaltosulkeiden ympäröimä koodilohko, jonka sisällä on metodin koodi -- käskyt, jotka suoritetaan kun metodia kutsutaan. Metodimme tekee vain yhden asian: kirjoittaa ruudulle yhden rivin tekstiä.

Oman metodin kutsuminen on yksinkertaista: kirjoitetaan metodin nimi, perään sulkumerkit ja puolipiste. Seuraavassa koodissa **Main** -metodi kutsuu **Greet** -metodia neljä kertaa.


```cpp
using System;

public class Program
{
  public static void Main(string[] args)
  {
    Console.WriteLine("Let's try if we can travel to the method world:");
    Greet();

    Console.WriteLine("Looks like we can, let's try again:");
    Greet();
    Greet();
    Greet();
  }

  // Omat metodit tänne
  public static void Greet()
  {
    Console.WriteLine("Greetings from the method world!");
  }
}
```

Ohjelman suoritus tuottaa seuraavan tulosteen:

```console
Let's try if we can travel to the method world: 
Greetings from the method world!
Looks like we can, let's try again:
Greetings from the method world!
Greetings from the method world!
Greetings from the method world!
```

Suoritusjärjestykseen kannattaa kiinnittää huomiota. Ohjelman suoritus tapahtuu suorittamalla **Main** -metodin (eli **Main**) rivit järjestyksessä ylhäältä alas, yksi kerrallaan. Käskyn ollessa metodikutsu, ohjelman suoritus siirtyy kutsuttavan metodin sisälle. Metodin käskyt suoritetaan ylhäältä alas, yksi kerrallaan. Tämän jälkeen suoritus palaa takaisin siihen kohtaan, josta metodikutsu tapahtui, ja jatkaa seuraavalla käskyllä.

Tarkalleen ottaen **Main** -metodi itsessään on myös metodi. Kun ohjelma käynnistyy, käyttöjärjestelmä kutsuu **Main** -metodia. **Main** -metodi on siis ohjelman aloituspiste, sillä suoritus alkaa sen ensimmäiseltä riviltä. Ohjelman suoritus päättyy **Main** -metodin viimeiselle riville. 

## Metodien nimeämisestä

Kävimme läpi muuttujien nimeämistä edellisessä osassa. Myös metodien nimeämiseen on oma käytäntönsä. Metodien nimet kirjoitetaan **PascalCase** -tyylillä. Tämä tarkoittaa, että metodin nimi alkaa isolla kirjaimella, ja jokaisen sanan ensimmäinen kirjain on iso. Se on hyvin samankaltainen kuin camelCase jota käytetään muuttujille. Suurin ero on, että PascalCase **metodin nimet alkavat isolla kirjaimella**.

Alla olevassa esimerkissä metodi on huonosti nimetty. Se alkaa pienellä alkukirjaimella ja sanat on eroteltu \_ merkillä. Metodin nimen perässä olevissa sulkumerkeissä on väli ja metodin sisällä oleva koodilohko on sisennetty väärin.

```cpp
public static void this_method_says_woof ( ) {
Console.WriteLine("woof");
}
```

Vertailun vuoksi alla oleva metodi on nimetty oikein: nimi alkaa isolla kirjaimella ja sanat on yhdistetty PascalCase-tyylillä, eli jokainen sana alkaa isolla kirjaimella. Sulkumerkit ovat vierekkäin ja sisällä oleva koodilohko on sisennetty oikein (metodilla on oma koodilohkonsa, joten koodin sisennys on neljä merkkiä).

```cpp
public static void ThisMethodSaysWoof()
{
  Console.WriteLine("woof");
}
```

## Metodin parametrit

**Parametrit** (englanniksi **Parameters**) ovat metodille annettuja arvoja joita voidaan käyttää sen suorituksessa. Metodin parametrit määritellään metodin yläreunassa, metodin nimen perässä olevissa sulkumerkeissä. Parametreja voi olla useita tai ei yhtään. Parametrit ovat muuttujia, joiden arvot kopioidaan metodin suorituksen ajaksi.

Seuraavassa esimerkissä on määritelty parametrillinen metodi **Greet**. Metodin parametri on int -tyypinen muuttuja nimeltä **numOfTimes**.

```cpp
public static void Greet(int numOfTimes)
{
    int i = 0;
    while (i < numOfTimes)
    {
      Console.WriteLine("Greetings!");
      i++;
    }
}
```

Kutsumme metodia eri arvoilla. Parametri **numOfTimes** saa arvon **1** ensimmäisellä kutsulla ja **3** toisella.

```cpp
  public static void Main(string[] args)
  {
    Greet(1);
    Console.WriteLine("");
    Greet(3);
  }
```

```console
Greetings!

Greetings!
Greetings!
Greetings!
```

Aivan kuten valmiita metodeja kuten **Console.WriteLine()** kutsuttaessa, parametriksi voidaan antaa lauseke.

```cpp
  public static void Main(string[] args)
  {
    Greet(1 + 2);
  }
```

```console
Greetings!
Greetings!
Greetings!
```

Jos parametrina käytetään lauseketta, se evaluoidaan ennen metodikutsua. Yllä olevassa esimerkissä lauseke **evaluoituu arvoon 3** ja lopullinen metodikutsu on muotoa **Greet(3)**.

## Monta parametria 

Metodille voidaan antaa useita parametreja. Kun sellaista metodia kutsutaan, parametrit annetaan samassa järjestyksessä kuin ne on määritelty. 

```cpp
public static void Sum(int first, int second)
{
  Console.WriteLine("The sum of numbers " + first + " and " + second + " is " + (first + second));
}
```

```cpp
Sum(3, 5);

int number1 = 2;
int number2 = 4;

Sum(number1, number2);
```

```console
The sum of numbers 3 and 5 is 8
The sum of numbers 2 and 4 is 6
```

## Parametrien arvot kopioidaan metodia kutsuttaessa

Kun metodia kutsutaan, **parametrien arvot kopioidaan**. Käytännössä tämä tarkoittaa sitä, että sekä **Main** -metodin että kutsuttavan metodin voi käyttää samannimisiä muuttujia, mutta parametrin arvon muuttaminen kutsuttavassa metodissa ei vaikuta samannimiseen muuttujaan **Main** -metodissa. Tutkitaan tätä seuraavassa esimerkissä.

```cpp
public class Example {
  public static void Main(string[] args)
  {
      int min = 5;
      int max = 10;

      PrintNumbers(min, max);
      Console.WriteLine();

      min = 8;

      PrintNumbers(min, max);
  }

  public static void PrintNumbers(int min, int max)
  {
      while (min < max) {
          Console.WriteLine(min);
          min++;
      }
  }
}
```

Ohjelman tuloste on seuraava:

```console
5
6
7
8
9

8
9
```

Muuttujan arvon muuttaminen **PrintNumbers** -metodissa ei vaikuta **Main** -metodissa olevan muuttujan arvoon, vaikka muuttujat ovat samannimisiä.

Eli vaikka niillä on täsmälleen sama nimi, metodin parametrit ovat eri kuin muiden metodien muuttujat (tai parametrit). Kun metodikutsun yhteydessä muuttuja annetaan metodille parametrina, muuttujan arvo kopioidaan metodille parametrimuuttujaan, joka määritellään samalla kun metodi määritellään. Nämä kaksi muuttujaa ovat eri muuttujia, vaikka niillä olisikin sama nimi.

Tämä on helpointa ymmärtää esimerkin avulla. Määritellään **Main** -metodissa muuttuja **number** ja annetaan se parametrina metodille **IncrementByThree**.

```cpp
// Main-metodi
public static void Main(String[] args)
{
  int number = 1;
  Console.WriteLine("The value of the variable 'number' in the Main program: " + number);
  IncrementByThree(number);
  Console.WriteLine("The value of the variable 'number' in the Main program: " + number);
}

// Oma metodi
public static void IncrementByThree(int number)
{
  Console.WriteLine("The value of the method parameter 'number': " + number);
  number = number + 3;
  Console.WriteLine("The value of the method parameter 'number': " + number);
}
```

Ohjelman tuloste on seuraava:

```console
The value of the variable 'number' in the Main program: 1
The value of the method parameter 'number': 1
The value of the method parameter 'number': 4
The value of the variable 'number' in the Main program: 1
```

Muuttujan **number** arvon kasvattaminen metodin sisällä ei aiheuta ongelmaa. Tämä ei aiheuta muutoksia muuttujan **number** arvoon **Main** -ohjelmassa. Tämä jälkimmäinen **number** on eri muuttuja kuin **IncrementByThree** -metodissa oleva **number**.

Parametri **number** kopioidaan metodia kutsuttaessa -- eli uusi muuttuja nimeltä **number** luodaan metodille **IncrementByThree** ja sille annetaan arvoksi kutsun yhteydessä annettu muuttujan **number** arvo. Metodin **IncrementByThree** sisällä oleva muuttuja **number** on olemassa vain metodin suorituksen ajan, eikä sillä ole mitään tekemistä **Main** -ohjelman samannimisen muuttujan kanssa.

## Metodit voivat palauttaa arvoja

Metodin määrittely kertoo, palauttaako metodi arvoja. Jos metodi palauttaa arvoja, määrittelyssä ilmaistaan palautettavan arvon tyyppi. Muuten määrittelyssä käytetään avainsanaa **void**. Tähän mennessä luomamme metodit ovat määritelty avainsanalla **void**, joten ne eivät ole palauttaneet mitään arvoja.


```cpp
public static void IncrementByThree()
{
  ...
}
```

Avainsana **void** tarkoittaa, että metodi ei palauta mitään. Jos haluamme metodin palauttavan arvon, avainsana **void** korvataan palautettavan muuttujan tyypillä. Seuraavassa esimerkissä on metodi **AlwaysReturnsTen**, joka palauttaa kokonaislukutyyppisen (**int**) muuttujan arvon 10.

Konkreettisemmin, arvon palauttaminen tapahtuu komennolla **return** ja sen perässä olevalla palautettavalla arvolla (tai muuttujan nimellä, jonka arvo palautetaan).

```cpp
public static int AlwaysReturnsTen()
{
  return 10;
}
```

Yllä määritelty metodi palauttaa **int** -tyyppisen arvon **10** sitä kutsuttaessa. Palautettava arvo täytyy tallentaa, jotta sitä voidaan käyttää. Tämä tapahtuu samalla tavalla kuin muuttujan arvon tallentaminen -- yhtäsuuruusmerkillä.


```cpp
public static void Main(String[] args)
{
  int number = AlwaysReturnsTen();

  Console.WriteLine("the method returned the number " + number);
}
```

Metodin palauttama arvo sijoitetaan **int** -tyyppiseen muuttujaan aivan kuten mikä tahansa **int** -arvo. Palautettu arvo voidaan käyttää myös osana mitä tahansa lauseketta.


```cpp
double number = 4 * AlwaysReturnsTen() + (alwaysReturnsTen() / 2.0) - 8;

Console.WriteLine("the result of the calculation " + number);
```

Kaikki tähän mennessä näkemämme muuttujatyypit voidaan palauttaa metodista.

| Metodin paluuarvo                       | Esimerkki                                     |
| --------------------------------------- | ----------------------------------------------|
| Metodi ei palauta mitään                | public static void ReturnsNothing()           |
| Metodi palauttaa **int** -muuttujan     | public static int ReturnsInt()                |
| Metodi palauttaa **string** -muuttujan  | public static string ReturnsString()          |
| Metodi palauttaa **double** -muuttujan  | public static double ReturnsDouble()          |
| Metodi palauttaa **bool** -muuttujan    | public static bool ReturnsBool()              |
| Metodi palauttaa **muuttujaTyypin**     | public static "muuttujaTyyppi" NameOfMethod() |

Lähdekoodin rivit jotka ovat rivin **return** jälkeen ei koskaan suoriteta. Jos ohjelmoija lisää lähdekoodia **return** -käskyn jälkeen, jota ei voi koskaan suorittaa, IDE tuottaa virheilmoituksen.

IDEn näkökulmasta seuraava metodi on virheellinen.


```cpp
public static int FaultyMethod()
{
  return 10;
  Console.WriteLine("I claim to return an integer, but I won't.");
}
```

Seuraava metodi toimii, koska jokainen lauseke voidaan saavuttaa -- vaikka **return** jälkeen onkin lähdekoodia.

```cpp
public static int FunctioningMethod(int parameter)
{
  if (parameter > 10) {
      return 10;
  }
  Console.WriteLine("The number received as parameter is ten or lesser.");

  return parameter;
}
```

Jos metodi on muotoa **public static void NameOfMethod()** siitä on mahdollista palata (return) -- eli lopettaa sen suoritus siinä kohdassa -- käyttämällä komentoa **return** ilman mitään arvoa. Esimerkiksi:

```cpp
public static void PrintEmptyLines(int parameter)
{
  if (parameter > 10)
  {
    return;
  }
  for (int i = 0; i < parameter; i++)
  {
    Console.WriteLine("");
  }
}
```

Tämä tulostaisi enintään 10 tyhjää riviä. Jos **parameter** on yli 10, metodi palaa eikä tulosta mitään. Esimerkki ei ehkä ole paras mahdollinen, mutta havainnollistaa ideaa...

## Muuttujien määrittäminen metodien sisällä

Muuttujan määrittäminen metodin sisällä tapahtuu samalla tavalla kuin **Main** -metodissa. Seuraavassa esimerkissä lasketaan kolmen luvun keskiarvo. Metodin sisällä määritellään muuttujat **sum** ja **avg** jotka auttavat laskennassa.


```cpp
public static double Average(int number1, int number2, int number3)
{
  int sum = number1 + number2 + number3;
  double avg = sum / 3.0;

  return avg;
}
```

Yksi tapa kutsua metodia on seuraavanlainen:

```cpp
public static void Main(String[] args)
{
  Console.Write("Enter the first number: ");
  int first = Convert.ToInt32(Console.WriteLine());

  Console.Write("Enter the second number: ");
  int second = Convert.ToInt32(Console.WriteLine());

  Console.Write("Enter the third number: ");
  int third = Convert.ToInt32(Console.WriteLine());

  double averageResult = Average(first, second, third);

  Console.Write("The average of the numbers: " + averageResult);
}
```

Metodissa määritellyt muuttujat ovat näkyvissä vain kyseisessä metodissa. Yllä olevassa esimerkissä tämä tarkoittaa sitä, että metodissa **Average** määritellyt muuttujat **sum** ja **avg** eivät ole näkyvissä **Main** -ohjelmassa. Tyypillinen virhe aloittelevalla ohjelmoijalla on yrittää käyttää metodia seuraavalla tavalla.


```cpp
public static void Main(String[] args)
{
  int first = 3;
  int second = 8;
  int third = 4;

  Average(first, second, third);

  // metodin sisäinen muuttuja avg yritetään tulostaa, EI TOIMI!
  Console.Write("The average of the numbers: " + avg);
}
```

Yllä ohjelmoija yrittää käyttää muuttujaa **avg** joka on määritelty **metodin Average sisällä**, ja tulostaa sen arvon. Muuttuja **avg** on kuitenkin olemassa vain **metodin Average sisällä**, eikä sitä voi käyttää sen ulkopuolella.

Myös seuraavanlainen virhe on yleinen.

```cpp
public static void Main(String[] args)
{
  int first = 3;
  int second = 8;
  int third = 4;

  // yritetään käyttää vain metodin nimeä, EI TOIMI!
  Console.Write("The average of the numbers: " + Average);
}
```

Yllä olevassa esimerkissä yritetään käyttää metodin **Average** nimeä ikään kuin se olisi muuttuja. Metodia täytyy kuitenkin kutsua.
Metodin tuloksen voi kuitenkin tallentaa muuttujaan, ja käyttää sitä myöhemmin. Toinen toimiva tapa on suorittaa metodikutsu suoraan tulostuksen yhteydessä.

```cpp
public static void Main(String[] args)
{
  int first = 3;
  int second = 8;
  int third = 4;

  // metodin kutsuminen tulostuksen sisällä, TOIMII!
  Console.Write("The average of the numbers: " + average(first, second, third));
}
```

Tässä metodin kutsu suoritetaan ensin ja se palauttaa arvon 5.0. Tämän jälkeen kyseinen arvo tulostetaan tulostuskomennossa.

## Paluuarvon laskeminen metodin sisällä

Palautettavan arvon ei tarvitse olla kokonaan määritelty etukäteen -- se voidaan myös laskea: **return** -käskyä joka palauttaa arvon metodista voidaan käyttää myös lausekkeen kanssa. 

Seuraavassa esimerkissä määritellään metodi **Sum** joka laskee kahden muuttujan arvon yhteen ja palauttaa summan. Summattavien muuttujien arvot saadaan metodin parametreina.

```cpp
public static int Sum(int first, int second)
{
  return first + second;
}
```

Kun metodin suoritus saavuttaa lausekkeen **return first + second;**, lauseke **first + second** evaluoidaan, ja sen arvo palautetaan myöhemmin.

Metodia kutsutaan seuraavalla tavalla. Metodin **Sum** avulla lasketaan yhteen luvut 2 ja 7. Metodin palauttama arvo sijoitetaan muuttujaan **sumOfNumbers**.


```cpp
int sumOfNumbers = Sum(2, 7);
// sumOfNumbers on nyt 9
```

Laajennetaan edellistä esimerkkiä niin, että luvut annetaan käyttäjän syötteinä:

```cpp
public static void Main(String[] args)
{
  Console.Write("Enter the first number: ");
  int first = Convert.ToInt32(Console.ReadLine());

  Console.Write("Enter the second number: ");
  int second = Convert.ToInt32(Console.ReadLine());

  Console.Write("The combined sum of the numbers is: " + Sum(first, second));
}

public static int Sum(int first, int second)
{
  return first + second;
}
```

Yllä olevassa esimerkissä metodin palauttamaa arvoa ei tallenneta muuttujaan, vaan se käytetään suoraan osana tulostusta.

Metodille annetut arvot kopioidaan sen parametreihin. Tämän vuoksi metodin parametrien nimillä ja metodin kutsun yhteydessä määriteltyjen muuttujien nimillä ei ole mitään tekemistä toistensa kanssa. Edellisessä esimerkissä sekä **Main** -ohjelman muuttujat että metodin parametrit olivat nimetty samalla tavalla (**first** ja **second**) "sattumalta". Seuraava koodi toimii täysin samalla tavalla vaikka muuttujat olisivat nimetty eri tavalla:

```cpp
public static void Main(String[] args)
{
  Console.Write("Enter the first number: ");
  int number1 = Convert.ToInt32(Console.ReadLine());

  Console.Write("Enter the second number: ");
  int number2 = Convert.ToInt32(Console.ReadLine());

  Console.Write("The combined sum of the numbers is: " + Sum(number1, number2));
}

public static int Sum(int first, int second)
{
  return first + second;
}
```

Nyt muuttujan **number1** arvo kopioidaan parametrin **first** arvoksi ja muuttujan **number2** arvo kopioidaan parametrin **second** arvoksi.


## Metodikutsujen suorittaminen ja kutsupino (call stack)

Miten tietokone muistaa, mihin palataan metodin suorituksen jälkeen?

C#:n lähdekoodin suoritusympäristö pitää kirjaa siitä, mikä metodi on suorituksessa kutsupinossa (englanniksi **call stack**). Kutsupino sisältää kehyksiä, joista jokainen sisältää tietoa yhdestä metodista: sen sisäiset muuttujat ja niiden arvot. Kun metodia kutsutaan, kutsupinoon luodaan uusi kehys (englanniksi **frame**), joka sisältää kyseisen metodin muuttujat. Kun metodin suoritus päättyy, kyseinen kehys poistetaan kutsupinosta, ja suoritus jatkuu edellisessä metodissa.

Kun metodia kutsutaan, suoritus odottaa kutsutun metodin suorituksen päättymistä. Tämä voidaan visualisoida kutsupinolla. Kutsupino viittaa metodikutsujen muodostamaan pinoon -- suorituksessa oleva metodi on aina pinon päällimmäisenä, ja metodin suorituksen päättyessä suoritus jatkuu pinon seuraavassa metodissa. Tutkitaan seuraavaa ohjelmaa:


```cpp
public static void Main(String[] args)
{
  Console.WriteLine("Hello world!");
  PrintNumber();
  Console.WriteLine("Bye bye world!");
}

public static void PrintNumber() {
  Console.WriteLine("Number");
}
```

Suoritus alkaa **Main** -metodista, kun ohjelma käynnistetään. Teksti "Hello world!" tulostetaan komennolla ensimmäisellä rivillä. Kutsupino näyttää tältä:

```console
Main
```

Kun tulostuskomento on suoritettu, seuraava rivi kutsuu metodia **PrintNumber**. Metodin kutsu siirtää ohjelman suorituksen metodin **PrintNumber** alkuun. Tällä välin **Main** -metodi odottaa, että **PrintNumber** -metodin suoritus päättyy. Metodin **PrintNumber** suorituksen aikana kutsupino näyttää tältä:

```console
PrintNumber
Main
```

Kun metodin **PrintNumber** suoritus päättyy, palataan metodin **PrintNumber** alla olevaan metodiin kutsupinossa -- tässä tapauksessa metodiin **Main**. Metodi **PrintNumber** poistetaan kutsupinosta, ja suoritus jatkuu **Main** -metodin **PrintNumber** -kutsun jälkeisellä rivillä. Kutsupinon tilanne on nyt seuraava:


```console
Main
```

## Kutsupino ja metodin parametrit

Tarkastellaan seuraavaksi kutsupinoa tilanteessa, jossa metodille on määritelty parametreja.

```cpp
public static void Main(String[] args)
{
  int beginning = 1;
  int end = 5;

  PrintStarts(beginning, end);
}

public static void PrintStars(int beginning, int end) {
  while (beginning < end) {
      Console.Write("*");
      beginning++; // sama kuin beginning = beginning + 1
  }
}
```

Ohjelman suoritus alkaa **Main** -metodin ensimmäiseltä riviltä. Seuraavat kaksi riviä luovat muuttujat **beginning** ja **end** ja asettavat niille arvot. Ohjelman tilanne ennen metodin **PrintStars** kutsumista:


```console
Main beginning = 1 end = 5
```

Kun metodia **PrintStars** kutsutaan, **Main** -metodi siirtyy odottamaan. Metodin kutsu aiheuttaa uusien muuttujien **beginning** ja **end** luomisen metodille **PrintStars**; parametreina annetut arvot kopioidaan niihin. Nämä arvot kopioitiin muuttujista **beginning** ja **end** **Main** -metodissa. Ohjelman tilanne metodin **PrintStars** suorituksen ensimmäisellä rivillä:

```console
PrintStars beginning = 1 end = 5
Main beginning = 1 end = 5
```

Kun komento beginning++ suoritetaan toistolauseessa, muuttujan **beginning**, joka kuuluu tällä hetkellä suoritettavalle metodille, arvo muuttuu.

```console
PrintStars beginning = 2 end = 5
Main beginning = 1 end = 5
```

Eli muuttujien arvot **Main** -metodissa pysyvät muuttumattomina. Metodin **PrintStars** suoritus jatkuu jonkin aikaa. Kun sen metodin suoritus päättyy, suoritus jatkuu **Main** -metodissa.


```console
Main beginning = 1 end = 5
```

## Kutsupino ja metodin palauttama arvo

Tarkastellaan seuraavaksi tilannetta, jossa metodi palauttaa arvon. **Main** -metodi kutsuu metodia **Start**, jonka sisällä luodaan kaksi muuttujaa, kutsutaan metodia **Sum** ja tulostetaan palautettu arvo.


```cpp
public static void Main(String[] args)
{
  Start();
}

public static void Start()
{
  int first = 5;
  int second = 6;

  int sum = Sum(first, second);

  Console.WriteLine("Sum: " + sum);
}

public static int Sum(int number1, int number2) {
  return number1 + number2;
}
```

Metodin **Start** suorituksen alussa kutsupino näyttää seuraavalta, sillä metodia **Start** kutsutaan **Main** -metodista. Metodilla **Main** ei ole omia muuttujia tässä esimerkissä:

```console
Start
Main
```

Kun muuttujat **first** ja **second** on luotu metodissa **Start** (metodin ensimmäiset kaksi riviä on suoritettu), tilanne näyttää seuraavalta:

```console
Start first = 5 second = 6
Main
```

Komento **int sum = Sum(first, second);** luo muuttujan **sum** metodissa **Start**, ja kutsuu metodia **Sum**. Metodi **Start** siirtyy odottamaan. Koska parametrit **number1** ja **number2** on määritelty metodissa **Sum**, ne luodaan heti metodin suorituksen alussa, ja niiden arvot kopioidaan parametreiksi annetuista muuttujista.


```console
Sum number1 = 5 number2 = 6
Start first = 5 second = 6
sum // no value
Main
```

Metodin **Sum** suoritus laskee yhteen muuttujien **number1** ja **number2** arvot. Komento **return** palauttaa summattujen muuttujien arvon metodille, joka on seuraavaksi kutsupinossa, eli tässä tapauksessa metodi **Start**. Palautettu arvo asetetaan arvoksi muuttujalle **sum**.

```console
Start first = 5 second = 6
sum = 11
Main
```

Tämän jälkeen suoritetaan tulostuskoment, ja palataan **Main** -metodiin. Kun suoritus saavuttaa metodin **Main** lopun, kutsupino on tyhjä ja ohjelman suoritus loppuu.

## Metodi kutsuu toista metodia

Kuten olemme jo aiemmin huomanneet, metodia voi kutsua toisen metodin sisältä. Lisäesimerkki tästä tekniikasta on annettu alla. Luomme metodin **MultiplicationTable** joka tulostaa kertotaulun annetusta luvusta. Metodi tulostaa rivit **PrintMultiplicationTableRow** -metodin avulla.


```cpp
public static void MultiplicationTable(int max)
{
  int number = 1;

  while (number <= max)
  {
    PrintMultiplicationTableRow(number, max);
    number++;
  }
}

public static void PrintMultiplicationTableRow(int number, int coefficient)
{
  int printable = number;
  while (printable <= number * coefficient)
  {
    Console.Write("  " + printable);
    printable += number;
  }
  Console.WriteLine("");
}
```

Tulostus metodikutsulla **MultiplicationTable(3)** näyttää seuraavalta:

```console
1 2 3
2 4 6
3 6 9
```

# Tehtävät

<Exercise title={'009 Print phrase'}>

Luo metodi **PrintPhrase** joka tulostaa lauseen "In a hole in the ground there lived a method" ja rivinvaihdon (käytä WriteLine eikä Write).

```cpp
public static void Main(string[] args)
{
  // Kutsu metodia tässä:
  PrintPhrase();

}

// Kirjoita metodi tähän:
public static void PrintPhrase() 
{

}
```

```console
In a hole in the ground there lived a method
```

</Exercise>

<Exercise title={'010 How many times'}>

Laajenna edellistä ohjelmaa siten, että Main-metodi kysyy käyttäjältä kuinka monta kertaa ("How many times?") lause tulostetaan (eli kuinka monta kertaa metodia kutsutaan).

```cpp
public static void Main(string[] args)
{
  // kysy käyttäjältä kuinka monta kertaa lause tulostetaan
  // käytä while-komentoa kutsuaksesi metodia sopiva määrä kertoja
  

}

// Kirjoita metodisi tähän:
public static void PrintPhrase() 
{

}
```

```console
How many times?
> 3
In a hole in the ground there lived a method
In a hole in the ground there lived a method
In a hole in the ground there lived a method
```

</Exercise>


<Note>
Tästä lähtien, kun esittelemme metodeja, emme välttämättä mainitse erikseen, että ne täytyy sijoittaa oikeaan paikkaan. Metodeja ei voi määritellä esim. toisten metodien sisällä.
</Note>

<Exercise title={'011 Print until number'}>

Luo seuraava metodi: `public static void PrintUntilNumber(int number)`. Se tulostaa numerot yhdestä annettuun lukuun asti. Kaksi esimerkkiä metodin käytöstä on annettu alla.


```cpp
public static void Main(string[] args) 
{
  PrintUntilNumber(5);
}
```

```console
1
2
3
4
5
```

```cpp
public static void Main(string[] args) 
{
  PrintUntilNumber(3);
}
```

```console
1
2
3
```

</Exercise>

<Exercise title={'012 From number to one'}>

Luo tehtäväpohjaan seuraava metodi: `public static void PrintFromNumberToOne(int number)`. Se tulostaa numerot annetusta luvusta alaspäin yhteen. Kaksi esimerkkiä metodin käytöstä on annettu alla.

```cpp
public static void Main(string[] args) 
{
  PrintFromNumberToOne(5);
}
```

```console
5
4
3
2
1
```

```cpp
public static void Main(string[] args) 
{
  PrintFromNumberToOne(2);
}
```

```console
2
1
```

</Exercise>

<Exercise title={'013 Division'}>

Kirjoita metodi `public static void Division(int numerator, int denominator)` joka tulostaa jakolaskun tuloksen (numerator / denominator). Muista että kokonaislukujen jakolasku palauttaa kokonaisluvun -- tässä tapauksessa haluamme tuloksen olevan liukuluku (double).


</Exercise>

<Exercise title={'014 Divisible in range'}>

Kirjoita metodi `public static void DivisibleByThreeInRange(int beginning, int end)` joka tulostaa kaikki luvut annetulta väliltä jotka ovat jaollisia kolmella. Luvut tulostetaan pienimmästä suurimpaan.

```cpp
public static void Main(string[] args) 
{
  DivisibleByThreeInRange(3, 6);
}
```

```console
3
6
```

```cpp
public static void Main(string[] args) 
{
  DivisibleByThreeInRange(2, 10);
}
```

```console
3
6
9
```

</Exercise>

<Exercise title={'015 Number uno'}>

Kirjoita metodi `public static void NumberUno()` joka palauttaa arvon 1.

</Exercise>

<Exercise title={'016 Word'}>

Kirjoita metodi `public static string Word()` joka palauttaa haluamasi merkkijonon (string).

</Exercise>

<Exercise title={'017 Sum'}>

Laajennetaan metodia `Sum` tehtäväpohjassa siten, että se laskee ja palauttaa parametreina annettujen lukujen summan.
Käytä seuraavaa rakennetta:


```cpp
public static int Sum(int number1, int number2, int number3, int number4) 
{
  // Kirjoita koodisi tänne
  // Muista palauttaa arvo (return)!
}

public static void Main(string[] args) 
{
    int answer = Sum(4, 3, 6, 1);
    Console.WriteLine("Sum: " + answer);
}
```
Esimerkin tuloste:

```console
Sum: 14
```

</Exercise>

<Exercise title={'018 Smallest'}>

Luo metodi `Smallest` kahdella parametrilla, joka palauttaa pienemmän parametrina annetuista arvoista.

```cpp
public static int Smallest(int number1, int number2) 
{
  // Kirjoita koodisi tänne
  // Älä tulosta metodin sisällä mitään

  // Loppuun return!
}

public static void Main(string[] args) 
{
  int answer =  Smallest(2, 7);
  Console.WriteLine("Smallest: " + answer);
}
```

Esimerkkituloste:

```console
Smallest: 2
```

</Exercise>

<Exercise title={'019 Greatest'}>

Luo metodi `Greatest` kolmella parametrilla, joka palauttaa suurimman parametrina annetuista arvoista.

```cpp
public static int Greatest(int number1, int number2, int number3) 
{
  // Kirjoita koodisi tänne
  // Älä tulosta metodin sisällä mitään

  // Loppuun return!
}

public static void Main(string[] args) 
{
  int answer =  Greatest(2, 7, 3);
  Console.WriteLine("Greatest: " + answer);
}
```

Esimerkkituloste:

```console
Greatest: 7
```

</Exercise>

<Exercise title={'020 Stars'}>

* Osa 1

Luo metodi `PrintStars(int number)` joka tulostaa annetun määrän tähtiä ja rivinvaihdon. 

Kirjoita metodi seuraavaan pohjaan:

```cpp
public static void PrintStars(int number)
{
  // Voit tulostaa yhden tähden komennolla
  // Console.Write("*");
  // Kutsu komentoa number kertaa
  // Loppuun rivinvaihto komennolla
  // Console.WriteLine("");
}

public static void Main(string[] args) 
{
  PrintStars(5);
  PrintStars(3);
  PrintStars(9);
}
```

Esimerkkituloste:

```console
***** 
*** 
*********
```

* Osa 2

Määritä metodi `PrintSquare(int size)` joka tulostaa sopivan neliön metodin `PrintStars` avulla. Eli metodi kutsu `PrintSquare(4)` tuottaa seuraavan tulostuksen:

```console
****
****
****
****
```

* Osa 3

Kirjoita metodi `PrintRectangle(int width, int height)` joka tulostaa sopivan suorakulmion metodin `PrintStars` avulla. Eli metodi kutsu `PrintRectangle(17, 3)` tuottaa seuraavan tulostuksen:


```console
***************** 
***************** 
*****************
```

* Osa 4

Luo metodi `PrintTriangle(int size)` joka tulostaa kolmion metodin `PrintStars` avulla. Eli metodi kutsu `PrintTriangle(4)` tuottaa seuraavan tulostuksen:


```console
*
**
***
****
```

</Exercise>

<Exercise title={'021 Christmas tree'}>

* Osa 1

Luo metodi `PrintSpaces(int number)` joka tulostaa parametrina annetun määrän välilyöntejä. Metodi ei tulosta rivinvaihtoa.

Sinun tarvitsee myös joko kopioida `PrintStars` metodi edellisestä tehtävästä tai toteuttaa se uudelleen tässä tehtävässä.

* Osa 2

<Note> 
Kommentti tässä ja seuraavissa esimerkeissä ei ole osa tulostusta, vaan vain korostamassa eroa edelliseen tehtävään.
</Note>

Luo metodi `PrintRightTriangle(int size)` joka käyttää metodeja `PrintSpaces` ja `PrintStars` oikealle nojaavan suorakulmaisen kolmion tulostamiseen. Eli metodi kutsu `PrintRightTriangle(4)` tuottaa seuraavan tulostuksen:

```cpp  
// HUOMAA VÄLILYÖNTIEN MÄÄRÄ    
   *  // Kolme välilyöntiä alussa
  **  // Kaksi
 ***  // Yksi
****  // Ei yhtään 
```  
<Note> 
Jos kolmio ei näytä nojaavan oikealle, kokeile toisella selaimella. Välillä Safari ja mobiiliselaimet eivät näytä merkkejä oikein.
</Note>



* Osa 3

Määritä metodi `ChristmasTree(int height)` joka tulostaa oikeanlaisen joulukuusen. Joulukuusi koostuu kolmiosta, jonka korkeus on parametrina annettu luku, sekä kuusen jalasta. Jalka on kaksi tähteä korkea ja kolme tähteä leveä, ja se sijaitsee kolmion pohjalla keskellä. Puu rakennetaan käyttämällä metodeja `PrintSpaces` ja `PrintStars`.

Esimerkiksi kutsu `ChristmasTree(4)` tuottaa seuraavan tulostuksen:


```cpp
// HUOMAA VÄLILYÖNTIEN MÄÄRÄ
   * 
  *** 
 *****
******* 
  *** 
  ***
```

Kutsu `ChristmasTree(10)` tuottaa seuraavan tulostuksen:


```cpp
// HUOMAA VÄLILYÖNTIEN MÄÄRÄ
         * 
        *** 
       ***** 
      ******* 
     ********* 
    *********** 
   ************* 
  *************** 
 ***************** 
******************* 
        *** 
        ***
```
<Note> 
Alle 3 korkeiden puiden ei tarvitse toimia oikein!
</Note>



</Exercise>
