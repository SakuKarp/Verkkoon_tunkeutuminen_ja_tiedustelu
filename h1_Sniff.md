# h1 Sniff

# x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

Karvinen 2025: Wireshark - Getting Started

- Wiresharkin asennus
- Wiresharkin käyttö
- Verkon sieppaaminen
- Display filtterit

Karvinen 2025: Network Interface Names on Linux

- Verkon käyttöliittymän käyttöä
- Verkon eri käyttöliittymien tarkoitukset
- Oman käyttöliittymän tarkastelu

# a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. (Tätä alakohtaa ei poikkeuksellisesti tarvitse raportoida, jos sinulla ei ole mitään ongelmia. Jos on mitään haasteita, tee täsmällinen raportti)

Virtuaalikone on asennettu käyttäen Teron ohjeita: https://terokarvinen.com/2021/install-debian-on-virtualbox/

# b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.

Aloitin pingaamalla googleen 8.8.8.8

    ping 8.8.8.8
![image](https://github.com/user-attachments/assets/af180e63-a9a0-4013-bc65-0949093d4de0)

Kuva näyttää yhteyden verkkoon.

![image](https://github.com/user-attachments/assets/b5831ae9-3cc1-462a-a49b-70309c56ffc4)

Yksinkertaisesti painamalla "Wired" saadaan virtuaalikone pois verkosta.

![image](https://github.com/user-attachments/assets/046f73dc-a9d2-430c-b2cb-4904589ae3b9)


Pingaus kun verkkoa ei ole : 

![image](https://github.com/user-attachments/assets/c7be18c4-eeb0-4466-b131-f35c387ce04e)

Verkko saadaan takaisin painamalla uudestaan "Wired"

Koneen saa myös verkosta pois tai päälle käyttäen virtualboxin omaa Devices -> Network -> Connect Network Adapter. 

![image](https://github.com/user-attachments/assets/a629b838-e44c-41ec-b5a4-73bc0e680b3a)



# c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).

Alotiin asentamalla wiresharkin käyttämällä komentoa : 

    sudo apt-get install wireshark

Wiresharkin Gui:

![image](https://github.com/user-attachments/assets/9a14c09e-80a2-464a-b0a8-e2147fa21098)


Aloitin sieppaamaan liikennettä painamalla sinistä "hain" kuvaa.

![image](https://github.com/user-attachments/assets/fcd6c03f-64e5-48b6-80a7-de8bb160a64e)

Kuvaa liikenteen seuraamisesta. 

![image](https://github.com/user-attachments/assets/20082a6f-49e6-4e0a-a581-d9933b15a1e1)




# d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Voit selityksen tueksi laatikoida ne ruutukaappauksesta.

Kuva siepatusta paketista:

![image](https://github.com/user-attachments/assets/facbb97c-babd-40e0-b112-151131d2ec9b)

Network access / link layer

1. Lähde ja kohde mac osoitteet: 

![image](https://github.com/user-attachments/assets/859b1780-b0b2-404d-b306-6196f8f69c78)


Kuvassa näkyy MAC-osoitteet ja ethernet tyyppi ipv4

2. Internet layer:

![image](https://github.com/user-attachments/assets/42b0ffde-82e9-4aa0-a526-d9fe4ec5dd84)

Kuvassa näkyy lähde ja kohde ip


3. Transport layer:

![image](https://github.com/user-attachments/assets/2c119af5-c7a3-4b4d-88f5-a1882c2fb577)

Kuvassa on lähdeportti, kohdeportti, sekvenssinumerot ja ACK-tiedot.

4. Application layer

![image](https://github.com/user-attachments/assets/fdbedf71-1709-4946-9cbf-71337bf0f1f4)

Kuvassa näkyy Protokolla ja tila (HTTP/1.1 200 OK), palvelin, pvm 



# e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.

# f) Vapaaehtoinen, vaikea: Mitä selainta käyttäjä käyttää? surfing-secure.pcap (Päivitys 2025-03-31 w14 ma - muutin tehtävän vapaaehtoiseksi Giang:n suosituksesta)

# g) Minkä merkkinen verkkokortti käyttäjällä on? surfing-secure.pcap

# h) Millä weppipalvelimella käyttäjä on surffaillut? surfing-secure.pcap
Huonoja uutisia: yhteys on suojattu TLS-salauksella.

# i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)

## References

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff

https://terokarvinen.com/2021/install-debian-on-virtualbox/

https://terokarvinen.com/network-interface-linux/

https://terokarvinen.com/wireshark-getting-started/

https://en.wikipedia.org/wiki/Internet_protocol_suite

https://tracker.debian.org/pkg/wireshark
