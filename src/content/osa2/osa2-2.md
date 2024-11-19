---
title: 'Lisää silmukoita'
nav_order: 2
hidden: false
---

Osassa 1 tutustuimme yksin kertaiseen while-silmukkaan

```cpp
while (true)
{
  // Tee jotain
}
```

Tämä on erittäin hyödyllinen kun ohjelman täytyy toistaa jotain toiminnallisuutta kunnes käyttäjä antaa tietyn syötteen.


Seuraavaksi tutustumme muutamaan muuhun tapaan toteuttaa silmukoita.

## While-silmukka ehdolla

Tähän asti olemme käyttäneet silmukkaa "true" ehdolla, jolloin silmukka toistuu ikuisesti (tai kunnes silmukka lopetetaan "break" komennolla).

Todellisuudessa silmukan sulkeet sisältävät ehtolauseen, tai ehdon, aivan kuten "if-lauseen" sulkeet. True arvo voidaan korvata lausekkeella, joka arvioidaan ohjelman suorituksen aikana. Lauseke määritellään samalla tavalla kuin ehtolauseen ehto.

Seuraava koodi tulostaa numerot 1,2,...,5. Kun muuttujan "number" arvo on yli 5, while-ehdon arvo arvoidaan olevan false ja suoritus päättyy.


```cpp
int number = 1;

while (number < 6)
{
  Console.WriteLine(number);
  number++;
}
```
Yllä oleva koodi voidaan lukea "Niin kauan kuin muuttujan "number" arvo on pienempi kuin 6, tulosta muuttujan "number" arvo ja lisää muuttujan "number" arvoa yhdellä".

Koodissa on myös uusi tapa lisätä muuttujan arvoa. Yllä olevassa koodissa muuttujan "number" arvoa lisätään yhdellä joka kerta kun silmukan sisältö suoritetaan.

Koodi tulostaa kuten alla.

```console
1
2
3
4
5
```

## For-silmukka (for-loop)

Yllä opimme kuinka "while-silmukkaa" ehdolla voidaan käyttää käymään läpi numeroita tietyllä välillä.

Tällaisen silmukan rakenne on seuraava.

```cpp
int i = 0;
while (i < 10)
{
  Console.WriteLine(i);
  i++;
}
```

Yllä oleva silmukka voidaan jakaa kolmeen osaan. Ensin määritellään muuttuja "i", jota käytetään silmukan toistojen laskemiseen, ja asetetaan sen arvoksi 0: **int i = 0;**. Tämän jälkeen määritellään silmukan ehto -- silmukka toistuu niin kauan kuin muuttujan "i" arvo on pienempi kuin 10: **i < 10**. Silmukan sisältö sisältää toiminnallisuuden joka suoritetaan **Console.WriteLine(i);**, jota seuraa muuttujan "i" arvon lisääminen yhdellä i++.

Sama voidaan saavuttaa **for-silmukalla** näin.

```cpp
for (int i = 0; i < 10; i++)
{
  Console.WriteLine(i);
}
```

For-silmukka koostuu neljästä osasta:

- määritellään muuttuja jota käytetään silmukan toistojen laskemiseen;
- silmukan ehto;
- muuttujan arvon lisääminen (tai vähentäminen tai muuttaminen); ja
- toiminnallisuus joka suoritetaan.

```cpp
for (*muuttujan määrittely*; *ehto*; *muuttujan kasvattaminen*)
{
  // Toiminnallisuus
}
```

Tarkastellaan tätä toiminnassa:

```cpp
for (int i = 0; i < 5; i++)
{
  Console.WriteLine(i);
}
```

Yllä oleva esimerkki tulostaa numerot nollasta neljään. Välillä voidaan käyttää myös muuttujia -- alla oleva esimerkki käyttää muuttujia "start" ja "end" määrittelemään numeroiden välillä, jotka silmukka käy läpi.

```cpp
int start = 3;
int end = 7;
for (int i = start; i < end; i++)
{
  Console.WriteLine(i);
}
```

Jatkamme harjoittelua silmukoilla tehtävissä. Voit käyttää joko while-silmukkaa ehdolla tai for-silmukkaa.

## Silmukan suorituksen lopettaminen

Silmukka ei lopeta suoritustaan välittömästi kun sen ehto arvioidaan todeksi. Silmukan ehto arvioidaan silmukan suorituksen alussa, eli

- kun seuraava suoritettava lauseke on silmukka, ja
- silmukan sisältö on suoritettu.

Katsotaan seuraavaa silmukkaa.

```cpp
int number = 1;

while (number != 2)
{
  Console.WriteLine(number);
  number = 2;
  Console.WriteLine(number);
  number = 1;
}
```

Tämä tulostaa

```console
1
2
1
2
... keeps on going forever
```

Vaikka **number** on yhtä kuin 2 jossain vaiheessa, silmukka suoritetaan ikuisesti.

**Silmukan ehto arvioidaan silmukan suorituksen alussa ja silmukan suorituksen päästessä sulkevaan aaltosulkeeseen.** Jos ehto on tosi, suoritus jatkuu silmukan alusta. Jos ehto on epätosi, suoritus jatkuu ensimmäisestä lausekkeesta aaltosulkeiden jälkeen (eli silmukan jälkeen).

Tämä pätee myös for-silmukkaan. Alle olevassa esimerkissä, silmukan suoritus -- väärin ymmärrettynä -- pitäisi loppua kun i on yhtä kuin 100. Kuitenkin, se ei lopu.


```cpp
for (int i = 0; i != 100; i++)
{
  Console.WriteLine(i);
  i = 100;
  Console.WriteLine(i);
  i = 0;
}
```

Yllä oleva silmukka ei koskaan lakkaa suoritusta.

## Toiminnallisuuden toistaminen

Yksi yleinen ohjelmatyyppi on "tee jotain tietty määrä kertoja". Yhteistä näille ohjelmille on toistuvuus. Jotain toiminnallisuutta toistetaan, ja laskuri muuttuja käytetään pitämään kirjaa toistoista.

Seuraava ohjelma laskee tulon 4\*3 hieman kömpelösti, eli summana 3 + 3 + 3 + 3:

```cpp
int result = 0;

int i = 0;
while (true)
{
  result += 3; // lyhenne lausekkeelle result = result + 3
  i++;  // lyhenne lausekkeelle i = i + 1

  if (i == 4)
  {
      break;
  }
}

Console.WriteLine(result);
```

Sama toiminnallisuus voidaan saavuttaa seuraavalla koodilla.

```cpp
int result = 0;

int i = 0;
while (i < 4)
{
  result += 3; // lyhenne lausekkeelle result = result + 3
  i++;  // lyhenne lausekkeelle i = i + 1
}

Console.WriteLine(result);
```

Tai käyttämällä for-silmukkaa kuten seuraavassa nähdään.

```cpp
int result = 0;

for (int i = 0; i < 4; i++)
{
  result += 3;
}

Console.WriteLine(result);
```

While-silmukan suoritus on visualisoitu alla.

Kun muuttujien määrä kasvaa, ohjelman ymmärtäminen vaikeutuu. Ohjelman suorituksen simulointi voi auttaa ymmärtämään sitä.

Voit simuloida ohjelman suoritusta piirtämällä taulukon, jossa on sarakkeet jokaiselle muuttujalle ja ehdolle, ja erillinen tila ohjelman tulostukselle. Käyt sitten läpi lähdekoodin rivi riviltä, ja kirjoitat muutokset ohjelman tilaan (jokaisen muuttujan tai ehtolauseen arvon), ja ohjelman tulostuksen.

Arvot muuttujille **result** ja **i** edellisestä esimerkistä on kirjoitettu taulukkoon alla jokaisella kerralla kun ehto **i < 4** arvioidaan.

| result |  i  | i < 4 |
| :----: | :-: | :---: |
|   0    |  0  | true  |
|   3    |  1  | true  |
|   6    |  2  | true  |
|   9    |  3  | true  |
|   12   |  4  | false |

## Ohjelman rakenteesta silmukoiden avulla

Edellisissä esimerkeissä, olemme keskittyneet tapauksiin joissa silmukka suoritetaan ennalta määrätyn määrän kertoja. Toistojen määrä voi perustua käyttäjän syötteeseen -- näissä tapauksissa for-silmukka on kätevä.

Ohjelmissa joissa silmukka suoritetaan kunnes käyttäjä antaa tietyn syötteen, for-silmukka ei ole paras vaihtoehto. Tällaisissa tapauksissa, while-true silmukka jota harjoittelimme aiemmin toimii hyvin. 

Katsotaan vähän monimutkaisempaa ohjelmaa, joka lukee kokonaislukuja käyttäjältä. Ohjelma käsittelee negatiiviset luvut virheellisinä, ja nolla lopettaa silmukan. Kun käyttäjä antaa nollan, ohjelma tulostaa kelvollisten lukujen summan, kelvollisten lukujen määrän ja virheellisten lukujen määrän.

Mahdollinen ratkaisu on esitetty alla. Kuitenkin, esimerkin tyyli ei ole ihanteellinen.

```cpp
Console.Write("Write numbers, negative numbers are invalid: ");
int sum = 0;
int validNumbers = 0;
int invalidNumbers = 0;

while (true)
{
  int input = Convert.ToInt32(Console.ReadLine());

  if (input == 0)
  {
    Console.WriteLine("Sum of valid numbers: " + sum);
    Console.WriteLine("Valid numbers: " + validNumbers);
    Console.WriteLine("Invalid numbers: " + invalidNumbers);
    break;
  }

  if (input < 0) {
      invalidNumbers++;
      continue;
  }

  sum += input;
  validNumbers++;
}
```

Yllä olevassa koodissa, laskenta joka tulisi suorittaa silmukan päättymisen jälkeen, suoritetaan silmukan sisällä. Tämä lähestymistapa ei ole suositeltava, koska se voi johtaa hyvin monimutkaiseen ohjelman rakenteeseen. Jos jotain muuta -- esimerkiksi lisää syötteen lukemista -- pitäisi tehdä silmukan päättymisen jälkeen, se voisi helposti päätyä silmukan sisälle. Mitä enemmän toiminnallisuutta tarvitaan, ohjelman rakenteesta tulee yhä hankalampi lukea.

Pysytellään seuraavassa silmukkarakenteessa:

```cpp
// Luo tarvittavat muuttujat

while (true)
{
  // lue syöte

  // lopeta silmukka --break

  // tarkista syötteen virheellisyys -- continue

  // käsittele kelvollinen syöte
}

// toiminnallisuus silmukan päättymisen jälkeen
```

Toisin sanoen, ohjelman rakenne on puhtaampi jos asiat jotka pitää tehdä silmukan päättymisen jälkeen, sijoitetaan sen ulkopuolelle.


```cpp
Console.Write("Write numbers, negative numbers are invalid: ");
int sum = 0;
int validNumbers = 0;
int invalidNumbers = 0;

while (true)
{
  int input = Convert.ToInt32(Console.ReadLine());

  if (input == 0) {
      break;
  }

  if (input < 0) {
      invalidNumbers++;
      continue;
  }

  sum += input;
  validNumbers++;
}

Console.WriteLine("Sum of valid numbers: " + sum);
Console.WriteLine("Valid numbers: " + validNumbers);
Console.WriteLine("Invalid numbers: " + invalidNumbers);
```

# Tehtävät

<Exercise title={'005 Iterating to input'}>

Kirjoita ohjelma joka lukee käyttäjältä kokonaisluvun. Ohjelma tulostaa luvusta 0 alkaen kaikki luvut käyttäjän antamaan lukuun asti. Voit olettaa, että käyttäjä antaa positiivisen luvun. Alla on muutamia esimerkkejä ohjelman toiminnasta.

<Note>Voit käyttää while-silmukkaa ehdolla, tai for-silmukkaa</Note>

```console
> 4
0
1
2
3
4
```

```console
> 1
0
1
```

</Exercise>

<Exercise title={'006 Iterating to hundred'}>

Kirjoita ohjelma, joka lukee käyttäjältä kokonaisluvun. Ohjelma tulostaa numerot siitä luvusta numeroon 100. Voit olettaa, että käyttäjä antaa aina numeron joka on pienempi kuin 100. Alla on muutamia esimerkkejä halutusta toiminnasta.


```console
> 99
99
100
```

```console
> -4
-4
-3
-2
-1
0
1
... (lots of numbers in between) ...
98
99
100
```

</Exercise>

<Note>

Tästä lähtien tehtävät saattavat olla useassa osassa ohjeissa, jotta niiden ymmärtäminen olisi helpompaa. Lopuksi sinulla pitäisi olla vain yksi ohjelma per tehtävä.

Jokainen osio on laskettu erikseen, kun lasketaan tehtävän kokonaispistemäärää. Esimerkiksi seuraava tehtävä, jossa on 2 osaa, lasketaan 2 pisteeksi kokonaispistemäärästä.

</Note>

<Note>
Kun kaikki testit menevät läpi, olet tehnyt kaikki osat. Tehtävästä on mahdollista saada myös vain osa pisteistä, jos vain osa testeistä menee läpi.
</Note>

<Exercise title={'007 Where to and from'}>

- Osa 1

Kirjoita ohjelma, joka tulostaa kokonaisluvut 1:stä annettuun numeroon.

```console
Where to? 
>3 
1 
2 
3
```

```console
Where to? 
>5 
1 
2 
3 
4 
5
```
<Note>Käyttäjältä annettu numero on nyt ehdon yläraja. Muista, että a &lt;= b tarkoittaa a on pienempi tai yhtä suuri kuin b.</Note>

- Osa 2 2

Kysy käyttäjältä myös lähtönumero. Tulosta kaikki numerot lähtönumerosta ylärajaan.

```console
Where to? 
>8 
Where from? 
>5
5 
6 
7 
8
```

Jos yläraja on pienempi kuin lähtönumero, ei mitään tulosteta:

```
Where to? 
> 12 
Where from? 
> 16
```
<Note>Muista, että yläraja ja alaraja voivat olla negatiivisia, ja yläraja kysytään ensin!</Note>

</Exercise>

<Exercise title={'008 Numbers and calculations'}>

- Osa 1

Luo ohjelma, joka kysyy käyttäjältä numeroita (alussa tulostetaan "Give numbers:") kunnes käyttäjä antaa luvun -1. Kun käyttäjä antaa -1, ohjelma tulostaa "Thx! Bye!" ja ohjelma lopettaa.

```console
Give numbers: 
> 5 
> 2 
> 4 
> -1 
Thx! Bye!
```

- Osa 2

Laajenna ohjelmaa siten, että se laskee ja tulostaa käyttäjän antamien lukujen summan (ei sisällä -1).


```console
Give numbers: 
> 5 
> 2 
> 4 
> -1 
Thx! Bye! 
Sum: 11
```

- Osa 3 

Laajenna ohjelmaa siten, että se laskee ja tulostaa käyttäjän antamien lukujen lukumäärän (ei sisällä -1).

```console
Give numbers: 
> 5 
> 2 
> 4 
> -1 
Thx! Bye! 
Sum: 11
Numbers: 3
```

- Osa 4

Laajenna ohjelma siten, että se tulostaa laskee ja tulostaa käyttäjän antamien lukujen keskiarvon (ei sisällä -1).

```console
Give numbers: 
> 5 
> 2 
> 4 
> -1 
Thx! Bye! 
Sum: 11
Numbers: 3
Average: 3.666666666666
```

- Osa 5

Laajenna ohjelma siten, että se tulostaa käyttäjän antamien lukujen parillisten ja parittomien lukujen lukumäärän (ei sisällä -1).

```console
Give numbers: 
> 5 
> 2 
> 4 
> -1 
Thx! Bye! 
Sum: 11
Numbers: 3
Average: 3.666666666666
Even: 2
Odd: 1
```

</Exercise>

<Note>
Kun kirjoitat ohjelmaa, oli se sitten harjoitustehtävä tai oma projekti, mieti millaisia osia ohjelma tarvitsee toimiakseen. Jaa ohjelma osiin ja toteuta ne yksi kerrallaan. Muista testata ohjelmaa jokaisen osan jälkeen.

Älä koskaan yritä ratkaista koko ongelmaa kerralla, koska se tekee ohjelman testaamisesta ja suorittamisesta kesken ongelmanratkaisun vaikeaa. Aloita jostain helposta, josta tiedät että osaat tehdä sen. Kun yksi osa toimii, voit siirtyä seuraavaan.

Osa tehtävistä on jo jaettuna osiin. Kuitenkin, on tyypillistä ohjelmoinnissa että nämä osat pitää jakaa vielä pienempiin osiin. Sinun pitäisi melkeinpä aina ajaa koodia jokaisen uuden rivin jälkeen. Tämä varmistaa että ratkaisu on menossa oikeaan suuntaan.
</Note>