# h1 Sniff

# x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)

Karvinen 2025: Wireshark - Getting Started

Karvinen 2025: Network Interface Names on Linux

# a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. (Tätä alakohtaa ei poikkeuksellisesti tarvitse raportoida, jos sinulla ei ole mitään ongelmia. Jos on mitään haasteita, tee täsmällinen raportti)

Virtuaalikone on asennettu käyttäen Teron ohjeita: https://terokarvinen.com/2021/install-debian-on-virtualbox/

# b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.

Aloitin pingaamalla googleen 8.8.8.8

    ping 8.8.8.8
![image](https://github.com/user-attachments/assets/af180e63-a9a0-4013-bc65-0949093d4de0)

Kuva näyttää yhteyden verkkoon.

![image](https://github.com/user-attachments/assets/b5831ae9-3cc1-462a-a49b-70309c56ffc4)

Yksinkertaisesti painamalla "Wired" saadaan virtuaalibox pois verkosta.

![image](https://github.com/user-attachments/assets/046f73dc-a9d2-430c-b2cb-4904589ae3b9)


Pingaus kun verkkoa ei ole : 

![image](https://github.com/user-attachments/assets/c7be18c4-eeb0-4466-b131-f35c387ce04e)

Verkko saadaan takaisin painamalla uudestaan "Wired"


# c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).

Alotiin asentamalla wiresharkin käyttämällä komentoa : 

    sudo apt-get install wireshark

# d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Voit selityksen tueksi laatikoida ne ruutukaappauksesta.

# e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.

# f) Vapaaehtoinen, vaikea: Mitä selainta käyttäjä käyttää? surfing-secure.pcap (Päivitys 2025-03-31 w14 ma - muutin tehtävän vapaaehtoiseksi Giang:n suosituksesta)

# g) Minkä merkkinen verkkokortti käyttäjällä on? surfing-secure.pcap

# h) Millä weppipalvelimella käyttäjä on surffaillut? surfing-secure.pcap
Huonoja uutisia: yhteys on suojattu TLS-salauksella.

# i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)

## References

