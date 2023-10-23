---
title: "Toisto"
nav_order: 5
hidden: false
---


Nyt osaamme tehdä yksinkertaisia komentoja, yksi kerrallaan. Mutta mitä jos haluamme tehdä jotain monta kertaa?

Esimerkiksi, tehdään ohjelma, joka kysyy käyttäjältä numeron 7 kertaa ja laskee ne yhteen.


```cpp
int sum = 0;
Console.Write("Give integer value: ");
int userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + intValue);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);

Console.Write("Give integer value: ");
userInput = Convert.ToInt32(Console.ReadLine());
sum = sum + userInput;
Console.WriteLine("Sum is " + sum);
``` 

Tämä saa tehtävän hoidettua, mutta kuten huomaat, siinä on paljon toistoa ja monta riviä koodia näin yksinkertaiseen tehtävään. Entä jos haluaisimme pyytää käyttäjältä 10 numeroa? Tai 1000? Voisimme toistaa samat rivit, mutta se olisi melko hullua.

Helpompi ja siistimpi tapa ratkaista tämä ongelma on käyttää **silmukoita**, erityisesti **while-silmukkaa**, johon tutustuimme hieman aiemmissa osissa.


```cpp
int sum = 0;
int readNumbers = 0;

while (true) 
{
    if (readNumbers == 7) {
        break;
    }

    Console.WriteLine("Give a number");
    sum = sum + Convert.ToInt32(Console.ReadLine());
    readNumbers = readNumbers + 1;
}
Console.WriteLine("Sum is " + sum);
```

Tutkitaan while-silmukkaa hieman tarkemmin.

## While-silmukka

```cpp
while (expression)
{
    // Your code is here
    // Here can be any amount of code
}
```

Toistaiseksi käytämme **true** -arvoa totuusarvona. Tämä voi johtaa loputtomaan silmukkaan. Kun koodilohko on suoritettu, tarkistetaan lausekkeen arvo. Koska se on aina tosi, koodi suoritetaan aina uudelleen.

## While-silmukan lopettaminen

Onnistuimme luomaan ohjelman edellisessä esimerkissä, joka ei toimi ikuisesti. Teimme sen avainsanalla **break**. Kuten nimi viittaa, se keskeyttää silmukan. Teknisesti ottaen se estää nykyisen koodilohkon suorituksen ja hyppää eteenpäin seuraavaan koodilohkoon.

Yleensä break-komentoa käytetään, kun käyttäjä antaa tietyn tyyppisen syötteen tai kun silmukkalaskenta on saavuttanut tietyn kohdan, juuri kuten esimerkissämme yllä.


```cpp
int number = 1;

while (true) 
{
    Console.WriteLine(number);
    if (number >= 5) {
        break;
    }
    number = number + 1;
}
Console.WriteLine("All done!");
```

```console
1
2
3
4
5
All done!
```

<Note>Loimme alkuperäisen numeromme silmukan ulkopuolella. Jos loisimme sen silmukan alussa, se luotaisiin uudelleen joka kerta, kun silmukka alkaa uudelleen.</Note>

```cpp
while (true) 
{
    int number = 1;
    Console.WriteLine(number);
    if (number >= 5) {
        break;
    }
    number = number + 1;
}
Console.WriteLine("All done!");
```

```console
1
1
1
1
1
... 
(This keeps going forever)
```

Voit myös pyytää käyttäjän syötettä while-silmukassa. Seuraavassa esimerkissä kysymme käyttäjältä, haluavatko he jatkaa ohjelman suorittamista.


```cpp
while (true) 
{
    Console.WriteLine("Do you want to continue?");
    string input = Console.ReadLine();
    if (input == "no") 
    {
        break;
    }
    Console.WriteLine("Let's keep going!");
}
Console.WriteLine("All done!");
```

```console
Do you want to continue?
> yes
Let's keep going!
Do you want to continue?
> totally
Let's keep going!
Do you want to continue?
> no
All done!
```

Edellisessä esimerkissä pyysimme käyttäjältä merkkijonosyötettä. Tietenkin muut muuttujatyypit toimivat yhtä hyvin.


```cpp
while (true) 
{
    Console.WriteLine("Input an integer, 0 quits");
    int command = Convert.ToInt32(Console.ReadLine());
    if (command == 0) 
    {
        break;
    }

    Console.WriteLine("You gave " + command);
}

Console.WriteLine("All done!");
```

```console
Input an integer, 0 quits
> 5
You gave 5
Input an integer, 0 quits
> -2
You gave -2
Input an integer, 0 quits
> 0
All done!
```

## Paluu while-silmukan alkuun

Palaamme while-silmukan alkuun, kun kaikki koodilohkon sisällä oleva koodi on suoritettu. On myös mahdollista palata alkuun muista kohdista koodia. Teemme sen **continue**-avainsanalla.

Alla olevassa esimerkissä pyydämme käyttäjältä positiivisia kokonaislukuja. Jos käyttäjä antaa negatiivisen kokonaisluvun, tulostamme viestin "Ei ole positiivinen kokonaisluku" ja palaamme silmukan alkuun. Jos käyttäjä antaa nollan, ohjelma päättyy.


```cpp
while (true) 
{
    Console.WriteLine("Input a positive integer, 0 quits");
    int number = Convert.ToInt32(Console.ReadLine());
    if (number == 0) 
    {
        break;
    }
    if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
        continue;
    }

    Console.WriteLine("You gave " + number);
}

Console.WriteLine("All done!");
```

```console
Input a positive integer, 0 quits
> 12
You gave 12
Input a positive integer, 0 quits
> -2
Not a positive integer!
Input a positive integer, 0 quits
> 0
All done!
```

Saatoit huomata, että käytimme kaksi if-ehtolauseketta sen sijaan, että käyttäisimme if-else-if -rakennetta. Katsotaan koodiamme if-else-rakenteella.


```cpp
while (true) 
{
    Console.WriteLine("Input a positive integer, 0 quits");
    int number = Convert.ToInt32(Console.ReadLine());
    if (number == 0) 
    {
        break;
    }
    else if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
        continue;
    }

    Console.WriteLine("You gave " + number);
}

Console.WriteLine("All done!");
```

Ainoa ero koodissa on **else if** sen sijaan, että olisi pelkkä **if**. Entä jos muuttaisimme järjestystä koodilohkossa?


```cpp
while (true) 
{
    Console.WriteLine("Input a positive integer, 0 quits");
    int number = Convert.ToInt32(Console.ReadLine());
    if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
        continue;
    }
    if (number == 0) 
    {
        break;
    }
    Console.WriteLine("You gave " + number);
}

Console.WriteLine("All done!");
```

Käyttäjän näkökulmasta toiminnallisuus on identtinen. Yhdistetään tämä koodi if-else-rakenteeksi.


```cpp
while (true) 
{
    Console.WriteLine("Input a positive integer, 0 quits");
    int number = Convert.ToInt32(Console.ReadLine());
    if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
    }
    else if (number == 0) 
    {
        break;
    }
    else 
    {
    Console.WriteLine("You gave " + number);
    }
}

Console.WriteLine("All done!");
```

Nyt kommentoimme ohjelman uusimmat versiot nähdäksemme, mitä tapahtuu koodissa.


```cpp
// Toista kunnes break
while (true) 
{
    // Kysy käyttäjältä syöte
    Console.WriteLine("Input a positive integer, 0 quits");
    // Lue syöte
    int number = Convert.ToInt32(Console.ReadLine());
    
    // Tarkista onko luku pienmpi kuin 0, jos ei, anna virhe
    if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
        continue;
    }
    // Haluaako käyttäjä lopettaa?
    if (number == 0) 
    {
        break;
    }
    // Tulosta lopputulos
    Console.WriteLine("You gave " + number);
}

// Lopeta
Console.WriteLine("All done!");
```

Kaikki rivit ja sisäiset koodilohkot suorittavat yksinkertaisen, merkityksellisen tehtävän. Entä yhdistetty versio?


```cpp
// Toista kunnes break
while (true) 
{
    // Kysy käyttäjältä syöte
    Console.WriteLine("Input a positive integer, 0 quits");
    // Lue syöte
    int number = Convert.ToInt32(Console.ReadLine());

    // if-else-if-else
    // Yksi koodilohko, monta toimintaoa

    // Tarkista onko numero liian pieni
    if  (number < 0)
    {
        Console.WriteLine("Not a positive integer!");
    }
    // Jos numero ei ole liian pieni, haluaako käyttäjä lopettaa?
    else if (number == 0) 
    {
        break;
    }
    // Jos numero ei ole liian pieni eikä käyttäjä halua lopettaa, tulosta numero
    else 
    {
    Console.WriteLine("You gave " + number);
    }
}
// Lopetus
Console.WriteLine("All done!");
```

Kuten näet, if-else-if-else -lohkolla on melko suuri tehtävä, ja sen määrittäminen vaatii useita vaiheita. Kun suunnittelet ohjelmiasi, sinun tulisi pyrkiä yksinkertaisiin tehtäviin kaikille koodilohkoille.

## Laskutoimitukset while-silmukoiden avulla

While-silmukoita käytetään usein laskutoimituksiin. Esimerkiksi ohjelmat, jotka käsittelevät määrittelemättömiä määriä käyttäjän syötteitä, perustuvat while-rakenteeseen. Tällaisissa ohjelmissa voimme kerätä esimerkiksi tilastoja annetuista numeroista tai muista syötteistä.

Jotta ohjelma voi tulostaa tietoa sen jälkeen, kun while-silmukka on suoritettu, meidän on tallennettava ja muokattava tietoja silmukan aikana.

Jos muuttuja tietojen tallentamiseen esitellään silmukalle omistetussa koodilohkossa, muuttuja on saatavilla vain koodilohkossa eikä muualla. Näytetään tämä kommentoidulla koodilla.


```cpp
// Toista kunnes lopetetaan

while (true) 
{
    // Luo muuttuja pitämään kirjaa ykkösistä
    int countOnes = 0;
    // Kysy luku
    Console.WriteLine("Input an integer, 0 quits");
    // Lue luku ja tallenna se muuttujaan
    int number = Convert.ToInt32(Console.ReadLine());
    // Jos 0, lopeta
    if (number == 0) 
    {
        break;
    }
    // Jos annettu numero on 1
        if  (number == 1)
    {
        // Kasvata muuttujan arvoa 1:llä
        countOnes = countOnes + 1;
    }
}

// Alla oleva käsky ei pysty käyttämään muuttujaa "countOnes",
// koska se on määritelty while-loopin sisäll
// Koodi ei toimi
Console.WriteLine("Amount of ones: " + countOnes);
```

Kaikki muuttujat ovat **näkyvissä** sille koodilohkolle, jossa ne sijaitsevat. Muokataan esimerkkiämme niin, että tulostusrivi on sisäisen koodilohkon sisällä, ja katsotaan, mitä tapahtuu.


```cpp
// Toista kunnes lopetetaan

while (true) 
{
    // Luo muuttuja pitämään kirjaa ykkösistä
    int countOnes = 0;
    // Kysy luku
    Console.WriteLine("Input an integer, 0 quits");
    // Lue luku ja tallenna se muuttujaan
    int number = Convert.ToInt32(Console.ReadLine());
    // Jos 0, lopeta
    if (number == 0) 
    {
        break;
    }
    // Jos annettu numero on 1
    if  (number == 1)
    {
        // Kasvata muuttujan arvoa 1:llä
        countOnes = countOnes + 1;
    }
    // Tulosta montako ykköstä kerättiin
    Console.WriteLine("Amount of ones: " + countOnes);
}
```

```console
Input an integer, 0 quits
> 5
Amount of ones: 0
Input an integer, 0 quits
> 1
Amount of ones: 1
Input an integer, 0 quits
> 1
Amount of ones: 1
Input an integer, 0 quits
> 2
Amount of ones: 0
Input an integer, 0 quits
> 0
```

Nyt ohjelma toimii, mutta ei niin kuin tarkoitimme. Koska muuttuja luodaan silmukan sisällä ja alustetaan nollaksi, aina kun silmukka toistuu, muuttuja palaa aina alkutilanteeseen.

Jos haluamme ohjelman toimivan, meidän on luotava muuttuja ennen silmukkaa. Seuraava esimerkki toimii tarkoitetusti.


```cpp
// Luo muuttuja pitämään kirjaa ykkösistä. Huom nyt while-silmukan ulkopuolella!
int countOnes = 0;

// Toista kunnes lopetetaan
while (true) 
{

    // Kysy luku
    Console.WriteLine("Input an integer, 0 quits");
    // Lue luku ja tallenna se muuttujaan
    int number = Convert.ToInt32(Console.ReadLine());
    // Jos 0, lopeta
    if (number == 0) 
    {
        break;
    }
    // Jos annettu numero on 1
    if  (number == 1)
    {
        // Kasvata muuttujan arvoa 1:llä
        countOnes = countOnes + 1;
    }
}
// Tulosta montako ykköstä kerättiin
Console.WriteLine("Amount of ones: " + countOnes);
```

```console
Input an integer, 0 quits
> 5
Input an integer, 0 quits
> 1
Input an integer, 0 quits
> 1
Input an integer, 0 quits
> -1
Input an integer, 0 quits
> 0
Amount of ones: 2
```

# Harjoitukset

<Note>Huom! Tee harjoitukset englanniksi, katso mallia harjoitusten esimerkeistä, miten koodin tulee toimia ja mitä sen tulee tulostaa (englanniksi)</Note>

<Exercise title={'034 Continue'}>

Luo ohjelma, joka kysyy käyttäjältä haluaako hän jatkaa. Jos käyttäjä vastaa "no", ohjelma päättyy, muussa tapauksessa kysytään uudestaan.


<Note>Use a while-loop!</Note>

```console
Do you want to continue?
> Yes
Do you want to continue?
> Hot potato
Do you want to continue?
> no
```

</Exercise>

<Exercise title={'035 Answer to life'}>

Luo ohjelma, joka kysyy käyttäjältä kokonaislukuja, kunnes käyttäjä antaa luvun 42.


```console
Give a number:
> 41
Give a number:
> 68
Give a number:
-42
Give a number:
42
```

</Exercise>

<Exercise title={'036 Power of positivity'}>

Luo ohjelma, joka kysyy kokonaislukuja käyttäjältä. Jos numero on nolla, ohjelma loppuu. Jos numero on negatiivinen tulosta viesti "That is negative". Jos numero on positiivinen, tulosta numero korotettuna toiseen potenssiin (eli numero kerrottuna itsellään).


```console
Give a number:
> 5
25
Give a number:
> -2
That is negative
Give a number:
> 4
16
Give a number:
0
```

</Exercise>

<Exercise title={'037 Counting numbers'}>

Luo ohjelma, joka kysyy käyttäjältä kokonaislukuja. Jos käyttäjä syöttää 0, ohjelma loppuu. Ohjelman lopussa ohjelma ilmoittaa montako numeroa käyttäjä kerkesi syöttää ennen loptusta. Älä laske viimeistä nollaa mukaan.


```console
Give a number:
> 5
Give a number:
> -2
Give a number:
> 22
Give a number:
> 0
Total amount of numbers: 3
```

</Exercise>

<Exercise title={'038 Counting negatives'}>

Luo ohjelma joka kysyy käyttäjältä kokonaislukuja. Jos luku on 0, lopeta. Lopussa ohjelma tulostaa montako negatiivista lukua käyttäjä syötti ennen lopetusta. Tee tulostus käyttämällä fraasia "Total amount of negative numbers: " ja summa. Älä laske viimeistä nollaa mukaan.


```console
Give a number:
> 5
Give a number:
> -2
Give a number:
> 22
Give a number:
> 0
Total amount of negative numbers: 1
```

</Exercise>

<Exercise title={'039 Sum of numbers'}>


Luo ohjelma, joka kysyy käyttäjältä kokonaislukuja. Jos luku on 0, lopeta. Lopussa tulosta syötettyjen lukujen yhteissumma "Total sum of numbers: " ja summa perään. 


```console
Give a number:
> 5
Give a number:
> -2
Give a number:
> 22
Give a number:
> 0
Total sum of numbers: 25
```

</Exercise>

<Exercise title={'040 Amount and sum'}>

Luo ohjelma, joka kysyy käyttäjältä kokonaislukuja. Nolla lopettaa. Lopussa tulosta numeroiden summa ja numeroiden määrä.


```console
Give a number:
> 5
Give a number:
> -2
Give a number:
> 22
Give a number:
> 0
Total sum of numbers: 25
Total amount of numbers: 3
```

<Note>Tarvitset kaksi muuttujaa, yhden summalle ja toisen numeroiden määrälle.</Note>


</Exercise>
