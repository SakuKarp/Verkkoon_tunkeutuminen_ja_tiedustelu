# x) Lue ja tiivistä.

Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs (Video, alkaen 3:19 ja päättyen 7:40. Yhteensä noin 4 min.)

Cornelius 2022: Decode 433.92 MHz weather station data


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

![Näyttökuva 2025-04-16 035130](https://github.com/user-attachments/assets/183f434c-947b-4503-a899-9722d15a2b5f)


## References:

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s&ab_channel=hubmartin

https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html
