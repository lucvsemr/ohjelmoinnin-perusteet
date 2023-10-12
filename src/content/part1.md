---
title: 'Osa 1 - Aloitus'
nav_order: 2
hidden: false
---

Tällä kurssilla opit ohjelmoinnin perusteita. Kurssi alkaa alkeista ja syventyy pikkuhiljaa. Ennen kuin aloitamme koodaamisen, meidän täytyy tietää, mitä koodaaminen on.

Ohjelmointi on ohjelmistojen suunnittelua ja toteutusta. Ohjelmia (**software** tai **program**) toteutetaan (eli kirjoitetaan tai "koodataan") tyypillisesti ihmisten kirjoitettavaksi ja luettavaksi tarkoitetulla **ohjelmointikielellä**.

Ohjelmointikieliä on satoja ja tällä kurssilla keskitytään näistä kielistä yhteen. Kurssin kielenä on **C#**. Voit löytää lisää tietoa kielestä englanniksi [**täältä**](https://docs.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/). Kyseisellä kielellä on hyvä dokumentaatio ja sieltä löytyy myös kurssille tarpeellista tietoa.

Ohjelmointikielet tarjoavat monia **metodeja** ja **komentoja** valmiiksi **sisäänrakennettuna** Täten meidän ei tarvitse toteuttaa aivan kaikkea itse. Iso osa ohjelmoinnista onkin ohjelmointikielen valmiiksi tarjoamien komentojen soveltamista ongelmien ratkaisuissa. Kirjoitettua "koodia" kutsutaan lähdekoodiksi (**source code**). Lähdekoodi koostuu lauseista (**statement**) ja lausekkeista (**expression**), joita yleensä voidaan lukea rivi riviltä ylhäältä alaspäin ja vasemmalta oikealle.

Meidän C# -ohjelmamme vaativat tietynlaisen rungon toimiakseen:

```cpp
public class Program {
    public static void Main(string[] args)
    {
        // Add your statements here
    }
}
```

Rungossa on monia osia, joista moni on valmiiksi luotu. Me keskitymme niihin myöhemmin tämän kurssin aikana.

Tällä hetkellä riittää että tiedät, että jokaisessa ohjelmassa on koodia joka on valmiiiksi kirjoitettu. Kaikkea ei tarvitse kirjoittaa itse. Jokaisessa ohjelmointikielessä on ominaisuuksia, joita tarvitaan koodin pyörittämiseen.

## Ohjelman ajaminen

Kun haluat kokeilla, toimiiko lähdekoodisi, sinä **ajat ohjelman**. Tämä tarkoittaa käytännössä kahta vaihetta: Ensin koodi pitää **kääntää**. Toinen vaihe on ohjelman ajaminen. Onneksi kääntäminen ja ajaminen voidaan yleensä tehdä melko automaattisesti, omalla **kääntäjällä**. Nykyaikaisilla kehitystyökaluilla kääntäminen ja ajaminen tapahtuu yhdellä komennolla, tai jopa napin painalluksella.

Kun käännät koodin, C# kääntäjä kääntää lähdekoodin moduuliksi, joka muutetaan **asemaksi**. Asema sisältää **Intermediate Language** (IL) koodin yhdessä **metadatan** kanssa. **Common Language Runtime** (CLR) toimii aseman kanssa. Se lataa aseman ja muuntaa sen **konekieleksi**. Tämän jälkeen käyttöjärjestelmä suorittaa konekielen ja tulostaa ohjelman tuloksen.

Kuten huomataan, kääntämisprosessi on melko monimutkainen toimenpide, jossa ihmisluettava koodi kääntyy konekielisemmäksi. Me keskitymme kuitenkin ihmislukuisempaan puoleen.