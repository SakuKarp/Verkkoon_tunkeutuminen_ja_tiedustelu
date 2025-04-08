# x) Lue ja vastaa lyhyesti kysymyksiin.

1. Selitä tuskan pyramidi

Tuskanpyramidin idea on korostaa sitä kuinka paljon haittaa aiheutetaan hyökkääjälle estämällä heitä. Mitä korkeammalla indikaattorityyppi on pyramiidissa sitä enemmän aikaa ja vaivaa hyökkääjän on käytettävä.

2. Selitä timanttimallin (Diamond Model)

Timanttimalli on malli jota käytetään kyberturvallisuuden ja eri hyökkäysten analysoinnissa. Hyäkkäys jaetaan neljään: Adversary, infrastructure, capability ja victim.


# a) Apache log. Asenna Apache-weppipalvelin paikalliselle virtuaalikoneellesi. Surffaa palvelimellesi salaamattomalla HTTP-yhteydellä, http://localhost . 
Etsi omaa sivulataustasi vastaava lokirivi. Analysoi yksi tällainen lokirivi, eli selitä sen kaikki kohdat. (Jos Apache ei ole kovin tuttu, voit tätä tehtävää varten vain asentaa sen ja testata oletusweppisivulla. Eli ei tarvitse tehdä omia kotisvuja tms.)

Aloitin asentamalla Apachen:

    sudo apt-get update # päivittää paketit
    sudo apt-get install apache2 # asentaa apachen
    sudo systemctl start apache2 # käynnistää

Avasin tämän jälkeen apachen localhostina http://localhost. Jonka jälkeen catti komennolla katsoin lokit.

    
    sudo cat /var/log/apache2/access.log

Rivi:

![image](https://github.com/user-attachments/assets/db2c9eea-eb43-4737-8dfc-23b315f643d2)

- Ip osoite
- aikaleima
- HTTP-pyyntö
- HTTP-vastauskoodi:200 OK
- 3380 vastauksen koko
- Selain: Firefox 128
- käyttis: Linux x86_64


# b) Nmapped. Porttiskannaa oma weppipalvelimesi käyttäen localhost-osoitetta ja 'nmap -A' päällä. Selitä tulokset. (Pelkkä http-portti 80/tcp riittää)

Alotin asentamalla nmapin, jonka jälkeen suoritin porttiskannauksen:

        sudo apt-get install nmap # asentaa
        sudo nmap -A -p 80 localhost # -A Agressiivinen/isompi skannaus, -p 80 Skannaa vain portin 80 ja localhost eli kohteena oma kone.


![image](https://github.com/user-attachments/assets/9919de1f-7aca-4392-a20e-f2c0289dc5ee)


- Hosti on päällä ja vastasi nopeasti
- 80/tcp open eli portti 80 on auki
- HTTP-palvelimena toimii Apache, versio 2.4.62, Debian-versio
- Palvelin versio Apache/2.4.62
- Varoitus siitä että vain yksi portti on skannattu mikä saattaa johtaa epätarkkaan tunnistukseen.

# c) Skriptit. Mitkä skriptit olivat automaattisesti päällä, kun käytit "-A" parametria? (Näkyy avoimien porttinumeroiden alta, http-blah, http-blöh...).

![image](https://github.com/user-attachments/assets/22711b76-42e2-4fe4-9df7-55f157e7e798)

http-server-header hakee palvelimen version

http-title hakee HTML-sivuston <title> elementin


# d) Jäljet lokissa. Etsi weppipalvelimen lokeista jäljet porttiskannauksesta (NSE eli Nmap Scripting Engine -skripteistä skannauksessa). Löydätkö sanan "nmap" isolla tai pienellä? Selitä osumat. Millaisilla hauilla tai säännöillä voisit tunnistaa porttiskannauksen jostain muusta lokista, jos se on niin laaja, että et pysty lukemaan itse kaikkia rivejä?

Aloitin tehtävän greppaamalla sanan "nmap" /var/log/apache2/access.log loki tiedostosta.

        sudo grep -i nmap /var/log/apache2/acess.log # -i ei erottele isoja ja pieniä kirjaimia

![image](https://github.com/user-attachments/assets/cc411fe9-8003-4573-ba24-ceed2e3baea5)

Sieltä löytyi rivejä joissa esintyy "Nmap Scripting Engine" user agent. Nmap on siis käyttänyt skriptejä tehdä HTTP-pyyntöjä palvelimelle osana skannausta.

        sudo gerp - i "Nmap Scripting Engine" /var/log/apache2/access.log # voi etsiä user agentit

Erisäännöillä joilla voisi luke lokia olisi esim. ip osoitteen kohdistaminen tai epätavallisten porttien etsiminen.

# e) Wire sharking. Sieppaa verkkoliikenne porttiskannatessa Wiresharkilla. Huomaa, että localhost käyttää "Loopback adapter" eli "lo". Tallenna pcap. 
Etsi kohdat, joilla on sana "nmap" ja kommentoi niitä. Jokaisen paketin jokaista kohtaa ei tarvitse analysoida, yleisempi tarkastelu riittää.

Aloitin avaamalla wiresharkin jonka jälkeen nmappasin portti 80 local hostin.

        sudo nmap -A -p 80 localhost

Kuva kun suodatetaan "nmap" eli käytetään filtterinä: frame contains "Nmap"

![image](https://github.com/user-attachments/assets/49f6ac93-6c75-426d-9a89-8b795284eeeb)

Nmap on käytetty palvelimen skannaamiseen HTTP:n kautta. Lähde- ja kohde osoite on sama eli skannaus tehty paikallisesti.

# f) Net grep. Sieppaa verkkoliikenne 'ngrep' komennolla ja näytä kohdat, joissa on sana "nmap".

Aloitin asentamalla ngrepin jonka jälkeen ngreppasin hakusanalla nmap. Spammasin muutaman kerran nmappia local hostiin jotta saadaan tietoa ulos.

        sudo apt-get install ngrep
        sudo ngrep -d lo -i nmap # -d lo määrittää että sieppaus tapahtuu verkkokortilla local host ja -i ei erottele isoja ja pieniä kirjaimia

![image](https://github.com/user-attachments/assets/51e09c87-a400-4a88-b6a6-71af4f58148d)

Kuvasta näkyy 338 saatu ja 25 oli "nmap".



# g) Agentti. Vaihda nmap:n user-agent niin, että se näyttää tavalliselta weppiselaimelta.

Alotin tutkimalla miten saisin vaihdettua useragentin että ses näyttäisi normaalilta webbiselaimelta ja löysin tämmöisen : 

https://www.oreilly.com/library/view/nmap-network-exploration/9781786467454/62ae3cc1-af7b-4046-89c1-a6eaa6c0b759.xhtml

        nmap -p80 --script http-sqli-finder --script-args http.useragent="Mozilla 42" <localhost> 

En saanut tätä toimimaan joten testasin teron antamaa :

        sudo nmap -A --script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)"

Tämän jälkeen katsoin catilla lokit ja siellä näkyi että user-agent on vaihtunut.

![image](https://github.com/user-attachments/assets/61e30428-73dd-44bf-8524-4b35315a46bf)


# h) Pienemmät jäljet. Porttiskannaa weppipalvelimesi uudelleen localhost-osoitteella.

Huomasin että lokit olivat hiaman muuttuneet mutta siellä silti näkyi vielä nämä kaksi:

![image](https://github.com/user-attachments/assets/53d15b94-340c-46bf-a9e3-f783edbd38e2)


# i) Hieman vaikeampi: LoWeR ChEcK. Poista skritiskannauksesta viimeinenkin "nmap" -teksti. Etsi löytämääsi tekstiä /usr/share/nmap -hakemistosta ja korvaa se toisella. Tee porttiskannaus ja tarkista, että "nmap" ei näy isolla eikä pienellä kirjoitettuna Apachen lokissa eikä siepatussa verkkoliikenteessä. 
(Tässä tehtävässä voit muokata suoraan lua-skriptejä /usr/share/nmap alta, 'sudoedit'. Muokatun version paketoiminen siis rajataan ulos tehtävästä.)

Jatkan tehtävää..









## References

https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/

https://www.oreilly.com/library/view/nmap-network-exploration/9781786467454/62ae3cc1-af7b-4046-89c1-a6eaa6c0b759.xhtml

https://www.threatintel.academy/wp-content/uploads/2020/07/diamond-model.pdf

https://duckduckgo.com/?t=ftsa&q=diamond+model+attacker+capability+infrastructure&ia=web

https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html


