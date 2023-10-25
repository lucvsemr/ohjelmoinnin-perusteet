---
title: "Merkkijonot"
nav_order: 4
hidden: false
---

Kerrataan alkuun mitä tiedämme merkkijonoista ja katsotaan sen jälkeen miten niitä voidaan jakaa. Luodaan ensin merkkijonon sisältävä muuttuja magicWord, joka saa arvon "abracadabra".

```cpp
string magicWord = "abracadabra";
```

Merkkijonon antaminen parametrina tulostuskomennolle (tai muillekin merkkijonoparametrin ottaville metodeille) tapahtuu tuttuun tapaan:


```cpp
string magicWord = "abracadabra";
Console.WriteLine(magicWord);
```

```console
abracadabra
```

## Merkkijonon lukeminen ja tulostaminen

Voit lukea merkkijonon ReadLine-metodilla, jota Console tarjoaa. Alla oleva ohjelma lukee käyttäjän nimen ja tulostaa sen:


```cpp
Console.WriteLine("What's your name?");
// luetaan käyttäjän syöte ja sijoitetaan se name-muuttujaan
string name = Console.ReadLine();

Console.WriteLine(name);
```

```console
What's your name?
> Hank
Hank
```

Merkkijonoja voi myös konkatenoida (eli yhdistää). Jos laitat + -operaattorin kahden merkkijonon väliin, saat uuden merkkijonon, joka on näiden kahden merkkijonon yhdistelmä. Kiinnitä huomiota välilyönteihin!

```cpp
string greeting = "Hi ";
string name = "Lily";
string goodbye = " and see you later!";

string phrase = greeting + name + goodbye;

Console.WriteLine(phrase);
```

```console
Hi Lily and see you later!
```

## Merkkijonojen vertailu

Merkkijonoa voidaan verrata toiseen merkkijonoon **==** -operaattorilla kuten muihinkin muuttujiin.

```cpp
string text = "Hello";
string word = "Hullo";

if (text == word)
{
  Console.WriteLine("Hooray!");
}
else
{
  Console.WriteLine("Boo");
}
```

```console
Boo
```

Kuten olemme jo tottuneet, boolean-arvo voidaan kääntää negaatiolla **!**.

```cpp
string text = "Hello";
string word = "Hullo";

if (!(text == word))
{
  Console.WriteLine("Boo!");
}
else
{
  Console.WriteLine("Hooray!");
}
```

Tai vertailun negaatiolla **!=**.

```cpp
string text = "Hello";
string word = "Hullo";

if (text != word)
{
  Console.WriteLine("Boo!");
}
else
{
  Console.WriteLine("Hooray!");
}
```

## Merkkijonon jakaminen

Voit jakaa merkkijonon useampaan osaan merkkijonon **Split-metodilla**. Metodi ottaa parametrina merkkijonon, jonka kohdalta merkkijono jaetaan. Split-metodi palauttaa taulukon, jossa on jaetun merkkijonon osat (englanniksi **substring**). Alla olevassa esimerkissä merkkijono on jaettu välilyönnin kohdalta.

```cpp
string text = "first second third fourth";
string[] pieces = text.Split(" ");
Console.WriteLine(pieces[0]);
Console.WriteLine(pieces[1]);
Console.WriteLine(pieces[2]);
Console.WriteLine(pieces[3]);

// Tulostetaan tyhjä rivi väliin
Console.WriteLine();

for (int i = 0; i < pieces.Length; i++)
{
  Console.WriteLine(pieces[i]);
}
```

```console
first
second
third
fourth

first
second
third
fourth
```

## Kiinteän muotoisen datan käsittely

Merkkijonon jakaminen on kätevää erityisesti silloin, kun data on kiinteässä muodossa. Tällä tarkoitetaan dataa, joka noudattaa jotain ennalta määriteltyä formaattia. Esimerkki tällaisesta on pilkuilla erotettu data (englanniksi **comma-separated values**, csv), jossa pilkut erottavat arvot toisistaan. Alla on esimerkki csv-muotoisesta datasta, jossa on nimiä ja ikä. Ensimmäisessä sarakkeessa on nimiä ja toisessa ikä. Saraakkeet on erotettu pilkulla.

```console
sebastian,2 
lucas,2 
lily,1
```

Oletetaan että käyttäjä syöttää yllä olevan datan rivi riviltä, lopettaen tyhjällä rivillä.


Ohjelma tulostaa nimet ja iät seuraavasti:


```cpp
while (true)
{
  string input = Console.ReadLine();
  if (input == "")
  {
    break;
  }
  string[] pieces = input.Split(",");
  Console.WriteLine("Name: " + pieces[0] + ", age: " + pieces[1]);
}
```

```console
> sebastian,2 
Name: sebastian, age: 2 
> lucas,2 
Name: lucas, age: 2 
> lily,1 
Name: lily, age: 1
```

## Monimuotoisen tekstin käyttäminen


Olemme tulostaneet merkkijonoja aiemmissa esimerkeissä. Kiinteässä muodossa olevassa merkkijonossa voi olla myös numeerista dataa. Yllä olevassa esimerkissä, jossa oli nimiä ja ikä, ikä oli kokonaisluku.

```console
sebastian,2 
lucas,2 
lily,1
```

Merkkijonon jakaminen tuottaa aina taulukon merkkijonoja. Jos teksti on kiinteässä muodossa, voimme olettaa tietyn indeksin olevan aina tietyn tyyppinen. Esimerkiksi yllä olevassa esimerkissä ikä indeksissä 1 on kokonaisluku.

Alla oleva ohjelma laskee summan tästä datasta. Jotta voisimme laskea summan, meidän pitää ensin muuttaa ikä kokonaisluvuksi (tuttu komento Convert.ToInt32).

```cpp
int sum = 0;

while (true)
{
  string input = Console.ReadLine();
  if (input == "")
  {
    break;
  }
  string[] parts = input.Split(",");
  sum = sum + Convert.ToInt32(parts[1]);
}
Console.WriteLine("Sum of the ages is " + sum);
```

```console
> sebastian,2 
> lucas,2 
> lily,1

Sum of the ages is 5
```

Voimme kirjoittaa ohjelman myös niin, että se laskee keskiarvon. 

```cpp
int sum = 0;
int count = 0;

while (true)
{
  string input = Console.ReadLine();
  if (input == "")
  {
    break;
  }
  string[] parts = input.Split(",");
  sum = sum + Convert.ToInt32(parts[1]);
  count++;
}
if (count > 0)
{
  Console.WriteLine("Age average: " + ((double)sum / count));
}
else
{
  Console.WriteLine("No input");
}
```

```console
> sebastian,2
> lucas,2
> lily,1

Age average: 1.6666666666666667
```

# Tehtävät

<Exercise title={'022 String three times'}>

Kirjoita ohjelma, joka lukee käyttäjältä merkkijonon ja tulostaa sen kolme kertaa peräkkäin.


```console
Give a word: cake

cakecakecake
```

<Note>Ohjelman tulisi kysyä merkkijonoa vain kerran. Älä käytä silmukkaa tässä.</Note>

</Exercise>

<Exercise title={'023 True string'}>

Kirjoita ohjelma, joka kysyy käyttäjältä merkkijonon. Jos käyttäjä kirjoittaa merkkijonon "true", ohjelma tulostaa "You got it right!", muussa tapauksessa ohjelma tulostaa "Try again!".

```console
Give a string: true 
You got it right!
```


```console
Give a string: trueish 
Try again!
```

</Exercise>

<Exercise title={'024 Login'}>

Kirjoita ohjelma joka tunnistaa seuraavat käyttäjät:


|käyttäjänimi	|salasana|
|--|--|
|alex|	sunshine|
|emma|	haskell|

Ohjelman pitäisi näyttää joko kirjautumisviesti tai ilmoitus virheellisestä käyttäjänimestä tai salasanasta.


```console
Enter username: 
>alex 
Enter password: 
> sunshine 
You have successfully logged in!
```


```console
Enter username: 
> emma 
Enter password: 
> haskell 
You have successfully logged in!
```

```console
Enter username: 
> alex 
Enter password: 
> haskell 
Incorrect username or password!
```

<Note>
Todellisuudessa kirjautuminen ei toimi näin! Tämä on vain harjoitus.
</Note>


</Exercise>

<Exercise title={'025 String split'}>

Kirjoita ohjelma joka lukee käyttäjältä merkkijonoja. Jos käyttäjä syöttää tyhjän merkkijonon, ohjelma lopettaa lukemisen ja ohjelman suoritus päättyy. Jos käyttäjä syöttää muun merkkijonon, ohjelma jakaa merkkijonon välilyöntien kohdalta ja tulostaa osat yksi kerrallaan.


```console
> once upon a time 
once 
upon 
a 
time 
> a little program 
a 
little 
program 
> halted 
halted
>
```

</Exercise>

<Exercise title={'026 Split contains av'}>

Kirjoita ohjelma, joka lukee käyttäjältä merkkijonoja. Jos käyttäjä syöttää tyhjän merkkijonon, ohjelma lopettaa lukemisen. Jos käyttäjä syöttää muun merkkijonon, ohjelma jakaa merkkijonon välilyöntien kohdalta ja tulostaa osat, jotka sisältävät merkkijonon `av`.

```console
> navy blue shirt
navy
> Do you have a favourite flavour
have
favourite
flavour
> was that a cat
>
```

<Note>
Merkkijonolla on Contains-metodi, joka kertoo, sisältääkö merkkijono toisen merkkijonon. Se toimii näin:


```cpp
string text = "volcanologist";

if (text.Contains("can")) 
{
  Console.WriteLine("can was found");
}

if (!text.Contains("tin")) 
{
  Console.WriteLine("tin wasn't found");
}
```

```console
can was found 
tin wasn't found
```
</Note>


</Exercise>

<Exercise title={'027 First part split'}>

Kirjoita ohjelma joka lukee käyttäjältä merkkijonoja. Jos käyttäjä syöttää tyhjän merkkijonon, ohjelma lopettaa lukemisen. Jos käyttäjä syöttää muun merkkijonon, ohjelma jakaa merkkijonon välilyöntien kohdalta ja tulostaa ensimmäisen osan.

```console
> one two three four 
one 
> this is a very important message 
this
>
```

</Exercise>

<Exercise title={'028 Last part split'}>

Kirjoita ohjelma joka lukee käyttäjältä merkkijonoja. Jos käyttäjä syöttää tyhjän merkkijonon, ohjelma lopettaa lukemisen. Jos käyttäjä syöttää muun merkkijonon, ohjelma jakaa merkkijonon välilyöntien kohdalta ja tulostaa viimeisen osan.

```console
> one two three four 
four 
> this is a very important message 
message
>
```

<Note>
Löydät taulukon pituuden Length-metodilla. Se toimii näin:

```cpp
string[] parts = {"one", "two", "three"};
Console.WriteLine("Number of parts: " + parts.Length);
```

```console
Number of parts: 3
```
</Note>

</Exercise>

<Exercise title={'029 CSV age'}>

Kirjoita ohjelma joka lukee käyttäjältä nimiä ja ikiä kunnes käyttäjä syöttää tyhjän merkkijonon. Nimi ja ikä on erotettu pilkulla.

Lukemisen jälkeen ohjelma tulostaa vanhimman henkilön iän. Voit olettaa, että käyttäjä syöttää ainakin yhden henkilön ja että ainakin yksi henkilö on vanhempi kuin muut.


```console
> sebastian,2 
> lucas,2
> lily,1
> hanna,5
> gabriel,10
>
Age of the oldest: 10
```

</Exercise>

<Exercise title={'030 CSV name'}>

Kirjoita ohjelma joka lukee käyttäjältä nimiä ja ikiä kunnes käyttäjä syöttää tyhjän merkkijonon. Nimi ja ikä on erotettu pilkulla.

Lukemisen jälkeen ohjelma tulostaa vanhimman henkilön nimen. Voit olettaa, että käyttäjä syöttää ainakin yhden henkilön ja että ainakin yksi henkilö on vanhempi kuin muut.

```console
> sebastian,2 
> lucas,2
> lily,1
> hanna,5
> gabriel,10
>
Name of the oldest: gabriel
```

</Exercise>

<Exercise title={'031 Maximum name and age'}>

Kirjoita ohjelma joka lukee käyttäjältä nimiä ja syntymävuosia kunnes käyttäjä syöttää tyhjän merkkijonon. Nimi ja syntymävuosi on erotettu pilkulla.

Lukemisen jälkeen ohjelma tulostaa pisimmän nimen ja korkeimman iän. Jos useilla henkilöillä on yhtä pitkä nimi, voit tulostaa minkä tahansa niistä. Voit olettaa, että käyttäjä syöttää ainakin yhden henkilön, ja meneillään on tämä vuosi.

```console
> sebastian,2017 
> lucas,2017 
> lily,2017 
> hanna,2014 
> gabriel,2009
>
Longest name: sebastian 
Highest age: 11
```

</Exercise>
