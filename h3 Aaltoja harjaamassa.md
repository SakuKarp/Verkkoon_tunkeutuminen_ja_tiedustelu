# x) Lue ja tiivistä.

Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs (Video, alkaen 3:19 ja päättyen 7:40. Yhteensä noin 4 min.)

- Signaalin kuunteleminen ja tallentaminen
- Signaalin tutkiminen
- Modulaatiot ASK,FSK,PSK
- Automaattinen parametrien tutkiminen
- Bittien pituus



Cornelius 2022: Decode 433.92 MHz weather station data

- Signaalien analysointiin voi käyttää URH:ta tai muita SDR-sovelluksia
- ASK-modulaatio on yleinen ja helppo toteuttaa esimerkiksi Arduinolla
- Signaalin dekoodaaminen



# a) WebSDR

Aloitin menemällä http://websdr.org/ sivustolle ja valitsin sieltä ensimmäisen joka oli :

![image](https://github.com/user-attachments/assets/babfceb4-2bd3-4374-af1e-b2f7e4cd2a3a)

Lähdin kuuntelemaan ja löysin:

![image](https://github.com/user-attachments/assets/8cbd178b-0555-4eab-8446-bd4a0fab0076)

Modulaatio: AM

Aallonpituus: n. 377 metriä

Sieltä kuului musiikkia joten olettaen tämä oli vissiin joku am-radiolähetys


# b) rtl_433

Aloitin asentamalla rtl_433 kalille:

    sudo apt install rtl-433 #asentaa
    rtl_433 #ajaa ohjelmaa
        
![image](https://github.com/user-attachments/assets/d8e5efbd-be43-4857-b4d8-7a2384e557c8)


# c) Automaattinen analyysi. Mitä tässä näytteessä tapahtuu? Mitä tunnisteita (id yms) löydät? Converted_433.92M_2000k.cs8. Analysoi näyte 'rtl_433' ohjelmalla.

Latasin Teron tiedoston ja menin Downloads kansioon jossa ajoin tiedoston 

        rtl_433 Converted_433.92M_2000k.cs8

        
![image](https://github.com/user-attachments/assets/630e1602-16fb-4635-b6af-c92f13663dbe)


Kuvasta näkee tunnisteen: 8785315

Mallit: KlikAanKlikUit-Switch, Proove-Security ja Nexa-Security

Komento : off eli jotain ehkä suljetaan


# d) Too compex 16

Aloitin lataamalla Teron tiedoston jonka jälkeen aloin muokkaamaan tiedosta jotta rtl_433 osaa lukea sitä.

    mv Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s foo_433.92M_2000k.cs8 # muuttaa tiedosto nimen oikein luettavaksi

Kuvasta näkee tunnisteen: 8785315

Mallit: KlikAanKlikUit-Switch, Proove-Security ja Nexa-Security

Komento : off

Eli sain samoja tietoja ulos tästä kuin edellisen tehtävästä.

# e) Ultimate. Asenna URH, the Ultimate Radio Hacker.

Aloitin asentamalla Teron ohjeita käyttäen:

    sudo apt-get update
    sudo apt-get -y install pipx
    pipx install urh
    pipx ensurepath

Tuli ongelma ettei se antanut minun asentaa sitä joten lähdin tutkimaan mistä tämä voisi johtua.

Löysin https://github.com/jopohl/urh/issues/1064 jossa oli ohje:

    sudo apt-get install cython3
    pipx install urh --system-site-packages

Tämän jälkeen urh latautui normaalisti:

![image](https://github.com/user-attachments/assets/d70403b1-3805-48b6-b403-586ebb06e6ad)

![image](https://github.com/user-attachments/assets/40812407-8685-47a7-bf66-6a16fdeacce9)

Aloitin tarkistelemaan Teron näytettä.

# f) Yleiskuva. Kuvaile näytettä yleisesti: kuinka pitkä, millä taajuudella, milloin nauhoitettu? Miltä näyte silmämääräisesti näyttää?

![image](https://github.com/user-attachments/assets/4e38341d-9c2e-492b-a922-b7d5a92e7e59)

Kohina: 0.0000

Keskipiste: 0.1439

Näytteet/symboli: 500

Virhetoleranssi: 2

Modulaatio: ASK

Bitit/symboli: 1

Aika: 5.49 sekunttia



# g) Bittistä. Demoduloi signaali niin, että saat raakabittejä. Mikä on oikea modulaatio? Miten pitkä yksi raakabitti on ajassa? Kuvaile tätä aikaa vertaamalla sitä johonkin. (Monissa singaaleissa on line encoding, eli lopullisia bittejä varten näitä "raakabittejä" on vielä käsiteltävä)

Aloitin tehtävän avaamalla tiedoston URH kautta. lähdin testaamaan eri modulaatioilla tiedostoa katsomalla bittien kautta mikä täsmää tähän tiedostoon.


![1](https://github.com/user-attachments/assets/f617fe82-ad54-4171-a032-cbc17044a576)


Tulokset kun katsoin bittien mukaan 1 ja 0:

![bitit 1](https://github.com/user-attachments/assets/ac13d857-cc29-4e5d-91f5-1924160c3375)

![bitit 0](https://github.com/user-attachments/assets/9cd071ed-bdd3-41c5-8b4a-5703fd16f060)


Bittien mukaan se saa signaalin tai äänen 1 mukaan ja ei mitään kun on 0.

kun valitsin tiedoston sain ajaksi 5.49 ja kun valitsin kaikki bitit se antoi ajaksi 5.42 en tiedä miksi.

kuva demuloidusta missä näkyy bitit 1 ja 0:


![demodul](https://github.com/user-attachments/assets/30666685-ec2b-4cf6-af90-08c7f3390336)


yhden signaalin pituus noin 524 mikro sekunttia

![1signaali](https://github.com/user-attachments/assets/4a6293a8-cb74-482f-b1f4-0a9543c5bf57)



## References:

http://websdr.org/

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s&ab_channel=hubmartin

https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html

https://github.com/jopohl/urh/issues/1064


