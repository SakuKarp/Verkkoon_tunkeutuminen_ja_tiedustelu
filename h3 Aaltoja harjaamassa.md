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

# e) Ultimate. Asenna URH, the Ultimate Radio Hacker.


# f) Yleiskuva

# g) Bittistä

## References:

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s&ab_channel=hubmartin

https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html
