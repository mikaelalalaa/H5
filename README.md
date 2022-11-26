# H5

Tunkeutumistestaus kurssin kotiläksy H5 Kautta kiven ja kannon. Alkuperäisen tehtävä anto löytyy [opttajan sivuilta.](https://terokarvinen.com/2022/tunkeutumistestaus-ict4tn027-3010-syksylla-2022/#h5-kautta-kiven-ja-kannon)



## x) Lue ja tiivistä valitsemasi Bellingcatin OSINT-opas.


## y) SuomiOsint



## a) Zap / b) ZAP certificate

Asensin zap sovelluksen tunnilla mutta kertaan miten tein sen.

Ensin haettiin paketteja ja sen jälkeen päivitettiin

```
sudo apt-get update

&

sudo apt upgrade

```
Sitten asennettiin itse sovellus komennolla `sudo apt install zaproxy`.

![image](https://user-images.githubusercontent.com/93308960/204091951-c0190b44-3d2a-4fea-9a90-e57774d04fb7.png)


Asennuksen jälkeen testattiin että zap toimii. Valitsin automatic scan ja siihen laitoin metaspoitable 2 olevan dvwa sivun osoitteen.

![image](https://user-images.githubusercontent.com/93308960/204102803-d9e26a93-cd6e-4446-8a9e-c63ddd74fb2b.png)


Skannaus onnistui ja saatiin paljon tietoa sivusta, kuten sen haavoittuvuudet ja kuinka vakavat ne ovat. Sieltä myös löydettiin istunto keksit.

![image](https://user-images.githubusercontent.com/93308960/204093507-ac7e091f-001a-471a-abf8-5220eb233ea4.png)



## c) Mitmproxy / d) Totally Legit Sertificate


Sain asennettua mitmproxyn jo tunnilla, komennolla `sudo apt install mitmproxy` se onnistui.


![image](https://user-images.githubusercontent.com/93308960/204095537-f75bb684-f12f-4331-996a-a773fe972e71.png)



![image](https://user-images.githubusercontent.com/93308960/204098610-97d6c039-3d99-4765-92c0-00bfb3911911.png)


![image](https://user-images.githubusercontent.com/93308960/204097871-0c50eaa4-de80-4867-8429-11497c500f70.png)

Verkon sieppaaminen ei onnistunut, ensin tuli error viesti siitä että osoite on jo käytössä. Löysin [Githubista](https://github.com/mitmproxy/mitmproxy/issues/219) samalla ongelmalla, joten ajattelin että ongelma on portissa. Löysin parilta sivustola portti vaihtoehtoja joita voisi testata [spiceworks](https://community.spiceworks.com/topic/2031610-webcache-tcp-port-8080) portti 8008 ja [opetajamme sivuta](https://terokarvinen.com/2019/mitmproxy-on-kali-and-xubuntu-attack-and-testing/?fromSearch=mitmproxy) portti 8888.

Testasin porttia 8888 `mitmproxy -p 8888`, jonka jälkeen avasin uuden terminaali sviun johon kirjoitin `curl --proxy http://localhost:8888 http://192.168.56.107/mutillidae`. Sain tietoa mitmproxyyn.

Apuna oli youtube video [QAInsights](https://www.youtube.com/watch?v=igcsLKDfssw) käyttäjältä.

![image](https://user-images.githubusercontent.com/93308960/204105607-22d05c72-b8f9-46b4-acaa-1b15068ca194.png)





## e) Ratkaise valitsemasi WebGoat-tehtävä

Valitsin tehtävän HTTP basic -> HTTP proxy.

 Zap proxyn kautta avasin uuden firefox selaimen jolla pääsin webgoat sivulle. 

![image](https://user-images.githubusercontent.com/93308960/204103225-7f452ce3-2c75-4b0a-a956-f6bac3cc7e6c.png)

Tämän jälkeen painoin vihreää painiketta jotta saadaan kaapattua uudet pyynnöt. Sitten mentiin takaisin webogat sivulle jossa painettiin submit.  

![image](https://user-images.githubusercontent.com/93308960/204101258-46a93ccd-4855-4a95-af81-412d61ad120b.png)

Muokattiin pyyntöä tehtävän mukaan:

Method vaihdettiin POST -> GET

lisättiin x-request-intercepted:true

lopuksi viahdettiin ChangeMe parametri doesn't+matter+really -> Request are tempered easly

Muutoksien jälkeen tämä lähetettiin uudelleen.

![image](https://user-images.githubusercontent.com/93308960/204101160-4f571f4d-c3fc-49e8-bbdb-1eaf63d4e027.png)

Mentiin takaisin webgoat sivulle jossa näkyi että tehtävä onnistui.

![image](https://user-images.githubusercontent.com/93308960/204101188-15319dde-af5e-4e20-9691-8411636666f1.png)

