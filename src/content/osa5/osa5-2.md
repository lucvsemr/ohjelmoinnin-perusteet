---
title: "Metodien ja konstruktorien ylikuormitus"
nav_order: 2
hidden: false
---

Palataan Person-luokkaan vielä kerran. Katsotaan hieman erilaista versiota luokasta:


```cpp
public class Person
{
  private string name;
  private int age;
  private double weight;
  private double height;


  public Person(string name)
  {
    this.name = name;
    this.age = 0;
    this.weight = 0;
    this.height = 0;
  }

  public double BodyMassIndex()
  {
    double heigthPerHundred = this.height / 100.0;
    return this.weight / (heigthPerHundred * heigthPerHundred);
  }

  public bool IsAdult()
  {
    if (this.age < 18)
    {
      return false;
    }
    return true;
  }

  public void GrowOlder()
  {
    this.age++;
  }

  public override string ToString()
  {
    return this.name + ", age: " + this.age;
  }
}
```

Alussa kaikki henkilöt ovat 0-vuotiaita, koska konstruktori asettaa instanssimuuttujan age arvoksi 0:


```cpp
public Person(string name)
{
  this.name = name;
  this.age = 0;
  this.weight = 0;
  this.height = 0;
}
```

## Konstruktorin ylikuormitus

Haluaisimme pystyä luomaan henkilöitä niin, että konstruktorille annetaan parametrina myös ikä. Tämä on mahdollista, koska luokalla voi olla useita konstruktoreita. Tehdään vaihtoehtoinen konstruktori. Vanhaa konstruktoria ei tarvitse poistaa.


```cpp
public Person(string name)
{
  this.name = name;
  this.age = 0;
  this.weight = 0;
  this.height = 0;
}

    public Person(string name, int age)
{
  this.name = name;
  this.age = age;
  this.weight = 0;
  this.height = 0;
}
```

Nyt meillä on kaksi vaihtoehtoista tapaa luoda henkilöitä:

```cpp
static void Main(string[] args)
{
  Person paul = new Person("Paul", 24);
  Person ada = new Person("Ada");
  
  Console.WriteLine(paul);
  Console.WriteLine(ada);
}
```

```console
Paul, age: 24
Ada, age: 0
```

Tämä tekniikka, jossa luokalla on kaksi (tai useampi) konstruktori, on nimeltään **konstruktorin ylikuormitus**. Luokalla voi olla useita konstruktoreita, jotka eroavat parametrien määrän tai tyypin perusteella. On kuitenkin mahdotonta olla kaksi konstruktoria, joilla on täsmälleen samat parametrit. Emme esimerkiksi voi lisätä konstruktoria **public Person(string name, int weight)**, koska kääntäjä ei pysty erottamaan tätä konstruktoria kahden parametrin konstruktorista, jossa int-parametri tarkoittaa ikää.e.

## Konstruktorin kutsuminen

Kuten ehkä huomasit, koodissamme on paljon "copy-pastea" ylikuormitetuissa konstruktoreissa, mikä tarkoittaa että samat rivit toistuvat uudelleen ja uudelleen. Kun katsot ylikuormitettuja konstruktoreita yllä, niissä on paljon samaa koodia. Tämä ei ole hyvä. Jos meillä olisi vielä enemmän konstruktoreita, meidän pitäisi olla riveillä **this.name...** jokaisessa konstruktorissa.

Ensimmäinen konstruktori, se jossa annamme vain nimen, on oikeastaan erikoistapaus jälkimmäisestä konstruktorista, jossa annetaan sekä nimi että ikä. Entä jos ensimmäinen konstruktori voisi kutsua toista konstruktoria?

Tämä ei ole ongelma, koska voit kutsua konstruktoria toisesta konstruktorista käyttämällä **this**-avainsanaa, joka on sidottu tähän tarkkaan objektiin!

Muokataan ensimmäistä konstruktoria niin, että se ei tee mitään itse, vaan kutsuu toista konstruktoria ja pyytää sitä asettamaan iän 0:ksi.



```cpp
// Tässä kutsutaan toista konstruktoria, ja ikäksi asetetaan 0
public Person(string name) : this(name, 0)
{
}

public Person(string name, int age)
{
  this.name = name;
  this.age = age;
  this.weight = 0;
  this.height = 0;
}
```

Konstruktorukutsu **this(name, 0)** voi vaikuttaa hieman oudolta. Käytämme avainsanaa **this** saadaksemme yhden konstruktorin kutsumaan toista konstruktoria, mikä vähentää "copy-pastea". Esimerkissä yllä voit kuvitella, että ylempi konstruktori kutsuu alempaa, arvoilla **name** ja **0**. Koska alempi konstruktori jo määrittelee, miten näitä arvoja käsitellään, ei ole tarvetta erikseen määritellä muuttujia ylemmässä konstruktorissa. Tämäntyyppinen konstruktorikutsu ei muuta koodin käyttäytymistä, ja uusia objekteja voidaan luoda kuten ennenkin:


```cpp
static void Main(string[] args)
{
  Person paul = new Person("Paul", 24);
  Person ada = new Person("Ada");
  
  Console.WriteLine(paul);
  Console.WriteLine(ada);
}
```

```console
Paul, age: 24
Ada, age: 0
```

## Metodin ylikuormitus

Kuten konstruktoreita, myös muita metodeita voidaan ylikuormittaa, joten sinulla voi olla monta versiota samasta metodista. Jälleen, eri versioiden parametrien on oltava erilaisia. Tehdään toinen versio **GrowOlder**-metodista, joka vanhentaa henkilöä sille annetun määrän vuosia.


```cpp
public void GrowOlder()
{
  this.age++;
}

public void GrowOlder(int years)
{
  this.age += years;
}
```

Alla "Paul" syntyy 24-vuotiaana, vanhenee vuoden, ja sen jälkeen 10 vuotta:


```cpp
static void Main(string[] args)
{
  Person paul = new Person("Paul", 24);
  Console.WriteLine(paul);
  paul.GrowOlder();
  Console.WriteLine(paul);
  paul.GrowOlder(10);
  Console.WriteLine(paul);

}
```

```console
Paul, age: 24
Paul, age: 25
Paul, age: 35
```

Luokalla Person on nyt kaksi **GrowOlder** -metodia. Kumpi niistä suoritetaan riippuu parametrien määrästä.

Voimme muokata ohjelmaa niin, että metodi ilman parametreja toteutetaan käyttämällä metodia **GrowOlder(int years)**:

```cpp
public void GrowOlder()
{
  this.GrowOlder(1);
}

public void GrowOlder(int years)
{
  this.age += years;
}
```

Ylikuormitetun metodin kutsuminen on hieman erilainen kuin ylikuormitetun konstruktorin kutsuminen. Ideana on edelleen täsmälleen sama. Sen sijaan, että koodi toistuisi kahdesti, käytämme **this**-avainsanaa ja kerromme, mitä kutsumme.

<Note>
Et voi käyttä samaa notaatiota kuin konstruktorin kanssa, eikä tämä toimi konstruktorin kanssa. Voit kokeilla, mitä tapahtuu (tai millaisia virheilmoituksia saat).
</Note>


# Tehtävät

<Exercise title={'004 Constructor overload'}>

Tehtäväpohjassa on luokka Product, joka kuvaa tuotetta kaupassa. Tuotteella on nimi, sijainti ja paino.

Lisää seuraavat kolme konstruktoria Product-luokkaan:

- `public Product(string name)` luo tuotteen, jonka nimi on annettu parametrina. Tuotteen sijainti on "shelf" ja paino on 1.
- `public Product(string name, string location)` luo tuotteen, jonka nimi ja sijainti on annettu parametrina. Tuotteen paino on 1.
- `public Product(string name, int weight)` luo tuotteen, jonka nimi ja paino on annettu parametrina. Tuotteen sijainti on "warehouse".

Voit kokeilla ohjelmaa seuraavalla koodilla:


```cpp
Product tapeMeasure = new Product("Tape measure");
Product plaster = new Product("Plaster", "home improvement section");
Product tyre = new Product("Tyre", 5);

Console.WriteLine(tapeMeasure);
Console.WriteLine(plaster);
Console.WriteLine(tyre);
```

```console
Tape measure (1 kg) can be found from the shelf. 
Plaster (1 kg) can be found from the home improvement section. 
Tyre (5 kg) can be found from the warehouse.
```

</Exercise>

<Exercise title={'005 Overloaded counter'}>

Luo luokka `Counter`. Luokka sisältää numeron, jonka arvoa voidaan kasvattaa ja pienentää. Luokalla on seuraavat konstruktorit:

- `public Counter(int startValue)` asettaa arvon laskurille konstruktorin parametrina annetun arvon mukaan.

- `public Counter()` asettaa arvon laskurille arvoksi 0.

Seuraavat metodit ja ominaisuudet:

- `public int value { get; set; }`
- `public void Increase()` kasvata arvoa yhdellä
- `public void Decrease()` vähennä arvoa yhdellä
- `public void Increase(int increaseBy)` kasvattaa arvoa parametrina annetulla arvolla. Jos parametrin arvo on negatiivinen, arvo ei muutu.
- `public void Decrease(int decreaseBy)` vähentää arvoa parametrina annetulla arvolla. Jos parametrin arvo on negatiivinen, arvo ei muutu.

</Exercise>