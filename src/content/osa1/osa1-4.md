---
title: 'Ehdot ja vertailut'
nav_order: 4
hidden: false
---

Tähän asti ohjelmamme ovat olleet melko lineaarisia, edeten vaiheittain järjestyksessä ilman vaihtoehtoja tai vaihtoehtoja. Usein haluamme vaihtoehtoja ohjelmistoomme, mikä tarkoittaa, että toiminnallisuus riippuu ohjelman muuttujien tilasta.

Jotta ohjelma voisi haarautua esimerkiksi käyttäjän syötteen perusteella, tarvitsemme **ehtolauseen** ohjelmaan. Yksinkertaisin ehtolause on


```cpp
Console.WriteLine("Hello world!");
if (true) 
{
    Console.WriteLine("This is always printed!");
}
```

```console
Hello world!
This is always printed!
```

Toisaalta voimme saada aikaan koodin jota ei koskaan suoriteta:

```cpp
Console.WriteLine("Hello world!");
if (false) 
{
    Console.WriteLine("This will never printed!");
}
```

```console
Hello world!
```

Tämä on tietysti aivan tarpeeton, vaikka mahdollinen.

Ehtolause alkaa avainsanalla **if**, jota seuraa **hakasulkeet ( )**. Hakasulkujen sisällä on lauseke, joka arvioidaan. Arvioinnin tulos on totuusarvo. Yllä olevissa esimerkeissä ei ollut tarvetta arvioinnille, koska ne olivat jo totuusarvoja.

Hakasulkeiden jälkeen tulee koodilohko, joka on ympäröity **{ }**. Lohkon sisällä oleva koodi suoritetaan, jos hakasulkujen sisällä oleva lauseke arvioidaan todeksi.

Tutkitaan esimerkki, jossa vertailemme kokonaislukuja.


```cpp
int number = 11;
if (number > 10) 
{
    Console.WriteLine("The number was larger than 10");
}
```

Jos ehtolauseen lauseke arvioidaan todeksi, kuten yllä rivillä "jos muuttujan number arvo on suurempi kuin 10", koodin suoritus siirtyy ehdollisen lauseen sisällä määritellyn lohkon sisään.

Jos lause olisi epätosi, koodin suoritus siirtyisi seuraavalle riville koodilohkon sulkevan **}** jälkeen.

<Note>if-lauseen jälkeen ei ole puolipistettä, koska lause ei pääty ehdollisen osan jälkeen.</Note>

### Muistutus koodin sisennyksestä

Koodin sisällä oleva lohko tulee sisentää. Esimerkiksi, if-lauseen sisällä oleva koodi tulee olla sisennetty enemmän kuin avainsana **if** koodissa. Lopetus **}** tulee olla samalla tasolla kuin if.


```cpp
int number = 11;
if (number > 10) 
{
Console.WriteLine("Indentation is wrong!");
}
```

```cpp
int number = 11;
if (number > 10) 
{
    Console.WriteLine("Indentation is right!");
}
```

## Relational operators

Seuraavassa taulukossa on lueteltu vertailuoperaattorit:

|Merkki| Merkitys |
|:--:|:---|
| >  | suurempi kuin |
| >= | suurempi tai yhtäsuuri kuin |
| <  | pienempi kuin|
| <= | pienempi tai yhtäsuuri kuin |
| == | yhtäsuuri |
| != | ei yhtäsuuri|


```cpp
int number = 55;

if (number != 0) 
{
    Console.WriteLine("Number is not equal to 0.");
}

if (number >= 1000) 
{
    Console.WriteLine("Number is at least 1000.");
}
```

```console
Number is at least 1000.
```

## Vaihtoehdot, ELSE

Jos if-lauseen sisällä oleva lauseke arvioidaan epätodeksi, koodin suoritus jatkuu seuraavaan lausuntoon. Tämä ei aina ole toivottavaa, mutta haluamme vaihtoehdon niille tilanteille, joissa if-lause arvioidaan epätodeksi.

Tämä voidaan saavuttaa else-lauseella, joka yhdistetään if-lauseeseen.


```cpp
int number = 4;

if (number > 5) 
{
    Console.WriteLine("Number is greater than 5!");
} 
else 
{
    Console.WriteLine("Number is 5 or smaller!");
}
```

```console
Number is 5 or smaller!
```

Jos ehtolauseella on else-haara, ehdollisen lauseen määrittelemä koodilohko suoritetaan, jos if-lause arvioidaan epätodeksi. Huomaa sisennys ja rivit!


## Vaihtoehdot, ELSE IF

Jos haluat useita vaihtoehtoja, käytä **else-if-rakennetta**. Se on samanlainen kuin else, mutta sillä on if-ehto. Niitä voi olla useita, ja ne tulevat if:n jälkeen, ennen elseä.


```cpp
int number = 3;

if (number == 1) 
{
    Console.WriteLine("Number is 1");
} 
else if (number == 2) 
{
    Console.WriteLine("Number is 2");
} 
else if (number == 3) 
{
    Console.WriteLine("Number is 3");
} 
else 
{
    Console.WriteLine("Number is something else");
}
```

```console
Number is 3
```

Yllä olevassa esimerkissä tarkistamme ensin, onko numero yhtä suuri kuin 1. Koska näin ei ole, siirrymme ensimmäiseen else-if:iin ja vertailemme numeroa arvoon 2. Koska tämä ei ole totta, siirrymme eteenpäin ja vertaamme muuttujamme arvoa 3:een. Koska tämä on totta, suoritamme koodin koodilohkossa ja tulostamme yllä näytetyn viestin. Emme mene else-lauseeseen, koska aiempi lause arvioitiin todeksi.

## Vertailujärjestys

Kuten kaikki koodit, vertailut tehdään järjestyksessä ylhäältä alas, vasemmalta oikealle. Kun saavutamme ehtolauseen, joka arvioidaan **todeksi**, suoritamme sen lohkon ja lopetamme vertailun.


```cpp
int number = 42;

if (number == 0) 
{
    Console.WriteLine("Number is 0.");
} 
else if (number > 0) 
{
    Console.WriteLine("Number is greater than 0.");
} 
else if (number > 2) 
{
    Console.WriteLine("Number is greater than 2.");
} 
else 
{
    Console.WriteLine("Number is smaller than 0.");
}
```

```console
Number is greater than 0.
```

Esimerkissä ehto **number > 0** arvioidaan **todeksi**, joten suoritamme siihen liittyvän koodilohkon ja lopetamme vertailun. Vaikka seuraava lause arvioitaisi myös todeksi, emme saavuta sitä osaa koodista (ja emme koskaan voi).

## Ehtolause ja bool-luokka

If-lauseen hakasulkujen sisällä olevan lauseen arvioidun arvon on oltava **bool**-tyyppiä. Bool on totuusarvon edustus ja se voi olla joko **true** tai **false**.


```cpp
bool truthValue = true;
Console.WriteLine("The value of truthValue is " + truthValue);
```

```console
The value of truthValue is True
```

Tai ehdollisesti,

```cpp
bool truthValue = true;
if (truthValue)
{
    Console.WriteLine("This is awesome!");
}
```
```console
This is awesome!
````

Vertailua voidaan käyttää myös ilman lauseita. Silloin bool-arvo tallennetaan bool-muuttujaan odottamaan myöhempää käyttöä.



```cpp
int first = 1;
int second = 3;
bool isFirstLargerThanSecond = first > second;
```

Nyt **isFirstLargerThanSecond** muuttujan arvo on **false**. Muutetaan esimerkkiä hieman ja jatketaan:


```cpp
int first = 1;
int second = 3;
bool isFirstSmallerThanSecond = first < second;

if (isFirstSmallerThanSecond)
{
    Console.WriteLine("1 is less than 3!");
}
```

```console
1 is less than 3!
```

## Jakojäännös

Jakojäännöstä ei tarvita kovin usein, mutta se on hyvä työkalu jos halutaan selvittää onko jokin jaollinen jollain toisella numerolla. 

```cpp
int remainder = 7 % 2;
Console.WriteLine(remainder); // 1
Console.WriteLine(5 % 3); //  2
Console.WriteLine(7 % 4); //  3
Console.WriteLine(8 % 4); //  0
Console.WriteLine(1 % 2); // 1
```

Koska jakojäännös on toimenpide, joka on samankaltainen kuin muut laskutoimitukset, voimme käyttää sitä esimerkiksi if-lauseessa.


```cpp
string userInput = Console.ReadLine();

int number = Convert.ToInt32(userInput);


if ((number % 400) == 0) 
{
    Console.WriteLine("The number " + number + " is divisible by four hundred");
} 
else 
{
    Console.WriteLine("The number " + number + " is not divisible by four hundred");
}
```

## Ehtolauseet ja muuttujien yhdenvertaisuus

Useimmissa ohjelmointikielissä, mukaan lukien C#, merkkijono on viittausmuotoinen (reference type), kun taas esimerkiksi kokonaisluku, totuusarvo ja liukuluku ovat arvotyyppejä (value types).

Joissakin ohjelmointikielissä tämä tarkoittaa, että merkkijonojen vertailu on tehtävä eri tavalla kuin muiden muuttujien. **C# on anteeksiantavampi.** Voimme vertailla kahta merkkijonoa **==** -operaattorilla, ainakin tässä kurssin vaiheessa.

Esimerkiksi seuraava toimii C#-kielellä, kun taas useimmissa muissa kielissä se ei toimisi:


```cpp
string a = "word";
string b = "word";
Console.WriteLine(a == b);
```

```console
True
```

Toinen tapa verrata merkkijonoja on käyttää **Equals-metodia**. Tämä metodi vertailee objektin arvoa. Palaamme tähän aiheeseen tarkemmin myöhemmin; nyt riittää, että tiedät tällaisen metodin olemassaolosta.


```cpp
string a = "word";
string b = "word"; 

Console.WriteLine(a.Equals(b));
```

```console
True
```

# Harjoitukset

<Note>Huom! Tee harjoitukset englanniksi, katso mallia harjoitusten esimerkeistä, miten koodin tulee toimia ja mitä sen tulee tulostaa (englanniksi)</Note>

<Exercise title={'024 Speeding'}>

Luodaan ohjelma, joka pyytää käyttäjältä kokonaislukua.

Jos annettu kokonaisluku on suurempi kuin 120, tulostetaan "Speeding!".


```console
Your speed:
> 5
````

```console
Your speed:
> 125
Speeding!
```

</Exercise>

<Exercise title={'025 Orwell'}>

Luo ohjelma, joka kysyy kokonaisluvun käyttäjältä. Jos luku on 1984, tulosta "Orwell".


```console
Give a number:
>1985
```

```console
Give a number:
> 1984
Orwell
```

</Exercise>



<Exercise title={'026 Too old'}>

Luo ohjelma, joka kysyy kokonaisluvun käyttäjältä. Jos luku on pienempi kuin 1900, tulostuu "You're old".


```console
Give your year of birth:
>1985
```

```console
Give your year of birth:
> 1899
You're old
```

</Exercise>

<Exercise title={'027 Stay positive'}>

Tee ohjelma, joka kertoo onko annettu luku positiivinen vai ei.


```console
Give a number:
> 5
It is positive
```

```console
Give a number:
-2
It is not positive
```

</Exercise>

<Exercise title={'028 Over eighteen'}>

Tee ohjelma, joka kertoo onko henkilö laillisesti aikuinen (Suomessa 18 tai yli), vai ei.

```console
How old are you?
> 5
You're under age!
```

```console
How old are you?
> 18
You're an adult!
```

</Exercise>

<Exercise title={'029 Larger number'}>

Tee ohjelma, joka kysyy kaksi kokonaislukua. Ohjelman tulee kertoa kumpi luvuista on suurempi. Jos ne ovat samat, sekin tulee ilmoittaa.


```console
Give the first number!
> 3
Give the second number!
> 2
The larger number is 3!
```

```console
Give the first number!
> 3
Give the second number!
> 4
The larger number is 4!
```

```console
Give the first number!
> 3
Give the second number!
> 3
They are equal!
```

</Exercise>

<Exercise title={'030 Course grading'}>

Alla on kurssin arviointitaulukko.

| Percent | Grade|
|---|---|
| < 0 | Impossible |
| 0 - 49  | Fail |
| 50 - 59 | 1 |
| 60 - 69 | 2 |
| 70 - 79 | 3 |
| 80 - 89 | 4 |
| 90 - 100 | 5 |
| > 100 | Outstanding! |

Laadi ohjelma, joka kysyy käyttäjältä heidän prosentit ja antaa arvosanan. 

(Käytä englanninkielisiä termejä!)

Alla pari esimerkkiä ohjelman toiminnasta:

```console
Give your percent [0 - 100]:
> -2
Impossible
```

```console
Give your percent [0 - 100]:
> 49
Fail
```

```console
Give your percent [0 - 100]:
> 75
Grade: 3
```

```console
Give your percent [0 - 100]:
> 99
Grade: 5
```

```console
Give your percent [0 - 100]:
> 9001
Outstanding!
```

</Exercise>

<Exercise title={'031 Even or odd'}>

Tee ohjelma, joka kysyy käyttäjältä kokonaisluvun ja kertoo onko se parillinen vai ei.


```console
Give a number:
> 2
It is even.
```

````console
Give a number
> 5
It is odd.
````

<Note>Vinkki: Voit tutkia jakojäännöksen avulla parillisuutta, käyttämällä % operaattoria.</Note>

</Exercise>

<Exercise title={'032 Enter friend'}>

Luo ohjelma, joka kysyy merkkijonon (string). Jos merkkijono on "Mellon", tulosta "Welcome, friend", muuten tulosta "They've got a cave troll!"


```console
Speak, friend, and enter!
> Let meeeee in!
They've got a cave troll!
```

```console
Speak, friend, and enter!
> Mellon
Welcome, friend
```

</Exercise>

<Exercise title={'033 Echo'}>

Tee ohjelma, joka kysyy kaksi merkkijonoa (string). Jos merkkijonot ovat samoja, tulosta "Echo!", muuten tulosta "Nope!"


```console
Give the first string:
> Potato
Give the second string:
> Potato
Echo!
```

```console
Give the first string:
> Potato
Give the second string:
> Tomato
Nope!
```

</Exercise>