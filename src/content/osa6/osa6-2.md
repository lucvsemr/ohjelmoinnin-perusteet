---
title: "Staattisuus ja ei-staattisuus"
nav_order: 2
hidden: false
---

# Luokkien ja olioiden metodit: staattisuus

Alussa useimmat metodimme sisälsivät avainsanan **static**, mutta olioiden myötä luovuimme siitä kokonaan. Miksi?

C#:ssa metodit voidaan jakaa kahteen ryhmään, jotka määritellään avainsanalla **static**. Avainsanan **static** puuttuessa metodit ovat **olion metodeja**, jotka kuuluvat tiettyyn olioon luokan sijaan.

Luokissa voit lisätä avainsanan **static** kenttiin, metodeihin, ominaisuuksiin, operaattoreihin, tapahtumiin ja konstruktoreihin (englanniksi **fields, methods, properties, operators, events, constructors**).

Oliometodit ovat metodeja, jotka kuuluvat olioihin, ja joiden koodissa voidaan käsitellä olion omia muuttujia ja muita oliometodeja. Oliometodeissa voidaan käyttää **this**-avainsanaa, joka viittaa kyseiseen olioon.

Alla on esimerkki luokasta **Item**, jolla on kolme oliometodia. Jokainen metodi voi käsitellä oliomuuttujia.


```cpp
public class Item
{
   private string name;

   public Item(string name) 
   {
     this.name = name;
   }

  // C#:ssa tämä voisi olla myös { get; set; } muuttujalle
  // Tällöin muuttuja olisi julkinen
  // Tässä esimerkissä haluamme suojata muuttujan ja pitää sen yksityisenä 
    public string GetName()
  {
    return this.name;
  }

  public string SetName(string name) 
  {
    this.name = name;
  }

  public override string ToString()
  {
    return this.name;
  }
}
```

Toisin kuin oliometodit, luokkametodit voivat käsitellä vain muuttujia jotka annetaan parametreina tai jotka luodaan metodin sisällä. Alla on esimerkki luokasta **Printer**, jolla on kaksi luokkametodia. Ensimmäinen tulostaa annetun merkkijonon alaviivoilla, ja toinen tulostaa viivoja annetun määrän.


```cpp
public class Printer
{
  // class methods
  public static void PrintUnderscored(string input)
  {
    Console.WriteLine(input);
    PrintLine(input.Length);
  }

  public static void PrintLine(int length)
  {
    for (int i = 0; i < length; i++)
    {
      Console.Write("-");
    }
    Console.WriteLine();
  }
}
```

Oliometodin kutsumiseen tarvitaan olio, jonka metodia kutsumme (muotoa **olioNimi.MetodinNimi**). Luokkametodeita voidaan kutsua ilman oliota (kutsu muodossa **MetodinNimi**). Jos haluamme kutsua luokkametodia luokan ulkopuolelta, kutsu on muodossa **LuokanNimi.MetodinNimi**.

Tarkastellaan esimerkkejä yllä olevista luokista **Program**-luokassa. Käytämme esimerkissä luokan **Printer** luokkametodeja, ja luokan **Item** oliota ja sen metodeja.


```cpp
public class Program 
{
  public static void Main(string[] args)
  {
    Printer.PrintUnderscored("Hello World!");

    Item chair = new Item("Kartell Louis Ghost");
    Printer.PrintLine(chair.GetName().Length);
    Printer.PrintUnderscored(chair.ToString());
  }
}
```

```console
Hello World!
------------
-------------------
Kartell Louis Ghost
-------------------
```

## Oliot luokkametodin parametrina

Tarkastellaan ohjelmaa, joka käsittelee listoja. **Main**-metodissa on toiminnallisuus, joka käsittelee listan kokonaislukuja. Lisäksi luokalla on luokkametodi **ZeroList**, joka toimii nimensä mukaisesti, asettaen nollan jokaiseen listaan saamaansa arvoon.


```cpp
public class Program 
{
  public static void Main(string[] args)
  {
    List<int> numbers = new List<int>();
    numbers.Add(1);
    numbers.Add(2);
    numbers.Add(3);
    numbers.Add(4);
    numbers.Add(5);

    foreach (int number in numbers)
    {
      Console.Write(number + " "); // Tulostaa 1 2 3 4 5
    }
    Console.WriteLine();

    ZeroList(numbers);

    foreach (int number in numbers)
    {
      Console.Write(number + " "); // Tulostaa 0 0 0 0 0
    }
  }

  public static void ZeroList(List<int> list)
  {
    for (int i = 0; i < list.Count; i++)
    {
      list[i] = 0;
    }
  }
}
```

Yllä olevassa esimerkissä **ZeroList**-metodilla on avainsana **static**, ja sitä kutsutaan ilman oliota ennen sitä.

Voimme antaa luokkametodille (tai **staattiselle metodille**) olion parametrina (jota olemme itseasiassa tehneet jo jonkin aikaa todelisuudessa). Luokkametodit eivät kuitenkaan voi käsitellä muita numeroita, merkkijonoja tai olioita kuin niitä, jotka annetaan parametreina tai jotka luodaan metodin sisällä.

Toisinsanoen, luokkametodia käyttävän koodin täytyy tukea metodia antamalla sille arvot ja oliot, joita se käyttää.

Koska luokkametodi ei ole sidoksissa yhteenkään olioon, sitä ei kutsuta samalla tavalla kuin oliometodia (**olioNimi.MetodinNimi()**), vaan kutsumme sitä (samassa luokassa) vain metodin nimellä. Jos luokkametodia kutsutaan luokan ulkopuolelta, se voidaan kutsua muodossa **LuokanNimi.StaattinenMetodi()**.

Alla on sama esimerkki, muutettuna siten, että **Main**-metodi ja metodi ovat omissa luokissaan:


```cpp
public class Program 
{
  public static void Main(string[] args)
  {
    List<int> numbers = new List<int>();
    numbers.Add(1);
    numbers.Add(2);
    numbers.Add(3);
    numbers.Add(4);
    numbers.Add(5);

    foreach (int number in numbers)
    {
      Console.Write(number + " "); // Prints 1 2 3 4 5
    }
    Console.WriteLine();

    Lists.ZeroList(numbers);

    foreach (int number in numbers)
    {
      Console.Write(number + " "); // Prints 0 0 0 0 0
    }
  }
}
```

```cpp
public class Lists 
{
  public static void ZeroList(List<int> list)
  {
    for (int i = 0; i < list.Count; i++)
    {
      list[i] = 0;
    }
  }
}
```

Staattinen metodi joka määritellään toisessa luokassa, tällä kertaa luokassa **Lists**, kutsutaan yllä olevassa esimerkissä muodossa **Lists.ZeroList(** parametrit **);**.

## Milloin tulisi käyttää luokkametodeja

Kaikki metodit jotka käsittelevät olioiden tilaa, täytyy määritellä oliometodeina, eli ilman avainsanaa **static**. Aiemmissa osissa olemme määritelleet luokkia kuten **Person, SimpleDate, Item, ...**, joiden kaikki metodit tulisi määritellä ilman **static**.

Palataan luokkaan **Person**. Alla on osa luokasta. Kaikki oliomuuttujat viitataan avainsanalla **this** korostaaksemme, että metodit käyttävät oliomuuttujia "sisällä" oliossa.


```cpp
public class Person
{
  private string name;
  private int age;

  public Person(string givenName) 
  {
    this.name = givenName;
    this.age = 0;
  }

  public bool IsOfAge()
  {
    return (this.age >= 18);
  }

  public void GrowOlder()
  {
    this.age++;
  }

  public override string ToString()
  {
    return this.name;
  }
}
```

Kun metodit käsittelevät oliota, niitä ei voida määrittää staattisiksi, eli "riippumattomiksi oliosta". Jos yritämme tehdä näin, metodi ei toimi. Alla oleva metodi ei toimi:

```cpp
public static void GrowOlder()
{
  this.age++;
}
```

Tuloksena saamme virheen:

```console
Member 'Exercise001.Person.GrowOlder()' cannot be accessed with an instance reference; qualify it with a type name instead
(38:5) Keyword 'this' is not valid in a static property, static method, or static field initializer
```

Tämä tarkoittaa sitä, että staattinen metodi ei voi käsitellä oliomuuttujia.

No milloin sitten tulisi käyttää staattisia metodeja? Katsotaan seuraavaa esimerkkiä, jossa meillä on henkilö-olioita. Ohjelmassa luomme henkilöitä, kasvatamme heitä vanhemmiksi ja lopulta tulostamme tietoa siitä, ovatko he täysi-ikäisiä.


```cpp
public class Program
{
  public static void Main(string[] args)
  {
    Person ada = new Person("Ada");
    Person jack = new Person("Jack");
    Person mike = new Person ("Mike");

    for (int i = 0; i < 30; i++)
    {
      ada.GrowOlder();
      mike.GrowOlder();
    }

    jack.GrowOlder();

    if (ada.IsOfAge())
    {
      Console.WriteLine(ada + " is of age");
    }
    else
    {
      Console.WriteLine(ada + " is under age");
    }

        if (mike.IsOfAge())
    {
      Console.WriteLine(mike + " is of age");
    }
    else
    {
      Console.WriteLine(mike + " is under age");
    }

        if (jack.IsOfAge())
    {
      Console.WriteLine(jack + " is of age");
    }
    else
    {
      Console.WriteLine(jack + " is under age");
    }
  }
}
```

Kuten näemme, koodi joka kertoo henkilön täysi-ikäisyydestä on kopioitu kolmeen kertaan. Tämä on rumaa!

Tässä on hyvä tilaisuus käyttää staattista metodia. Kirjoitetaan ohjelma uudelleen, käyttäen metodia:


```cpp
public class Program
{
  public static void Main(string[] args)
  {
    Person ada = new Person("Ada");
    Person jack = new Person("Jack");
    Person mike = new Person ("Mike");

    for (int i = 0; i < 30; i++)
    {
      ada.GrowOlder();
      mike.GrowOlder();
    }

    jack.GrowOlder();

    TellIfOfAge(ada);
    TellIfOfAge(mike);
    TellIfOfAge(jack);
  }

  public static void TellIfOfAge(Person person) 
  {
    if (person.IsOfAge())
    {
      Console.WriteLine(person + " is of age");
    }
    else
    {
      Console.WriteLine(person + " is under age");
    }
  }
}
```

Metodi **TellIfOfAge** on määritelty staattiseksi, joten se ei ole kiinnitetty mihinkään olioon, **MUTTA** metodi saa olion parametrina. Metodia ei ole määritelty **Person**-luokassa, vaikka se käsittelee **Person**-olioita. Se on apumetodi pääohjelmalle, joka tekee pääohjelmasta luettavamman.

# Tehtävät

<Exercise title={'003 How many names'}>

Tehtäväpohjassa on luokka `Person` ja sen käyttöä Mainissa. Tee Main-luokkaan metodi `public static void HowManyNames(Person person)`, joka tulostaa nimen ja sen nimien määrän seuraavasti:


```cpp
public static void Main(string[] args)
{
  Person ada = new Person("Ada Lovelace");
  Person jack = new Person("Jack The Ripper");
  Person mike = new Person("Mike The Incredible Magic Mouse");

  HowManyNames(ada);
  HowManyNames(jack);
  HowManyNames(mike);
}
```

```console
Ada Lovelace has 2 names.
Jack The Ripper has 3 names.
Mike The Incredible Magic Mouse has 5 names.
```

<Note> 
Console.WriteLine kutsutaan metodin sisältä tällä kertaa!
</Note>

</Exercise>

<Exercise title={'004 How many names in person'}>

Tehtäväpohjassa on luokka `Person` ja sen käyttöä Mainissa. Tee luokkaan `Person` metodi `public int HowManyNames()`, joka palauttaa nimen ja sen nimien määrän seuraavasti:

```cpp
public static void Main(string[] args)
{
  Person ada = new Person("Ada Lovelace");
  Person jack = new Person("Jack The Ripper");
  Person mike = new Person("Mike The Incredible Magic Mouse");

  Console.WriteLine(ada + " has " ada.HowManyNames() + " names.");
  Console.WriteLine(jack + " has " jack.HowManyNames() + " names.");
  Console.WriteLine(mike + " has " mike.HowManyNames() + " names.");
}
```

```console
Ada Lovelace has 2 names.
Jack The Ripper has 3 names.
Mike The Incredible Magic Mouse has 5 names.
```

<Note> 
Console.WriteLine kutsutaan metodin sisältä tällä kertaa!
</Note>

</Exercise>
