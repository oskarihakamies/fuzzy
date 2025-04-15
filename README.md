# fuzzy
Learning the basics of fuzzing


x)

Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with Fuff

- Tekstissä selitettiin hyvin, miten erilaisia piilotettuja netin hakemistoja voi löytää.
- Esimerkki fuffin avulla, miten salaisen hakemiston löytäminen onnistui oli ihan mielenkiintoinen.
- Näytettiin hyvin, miten fuffin avulla fuzzaaminen on paljon nopeampaa, kuin manuaalisesti.




Hoikkala 2023: ffuf README.md

- Kyseessä on Joona 'joohoi' Hoikkalan selitys fuffista sen asennuksesta erilaisiin komentoihin asti.
- Näytetyt komennukset ovat selkeitä sivulla ja muutama video auttaa myös selkeyttämään ymmärrystä.





a) Fuzzzz.

Aloitin tehtävän lataamalla dirfurzt-1 kaliin. 


<img width="314" alt="image" src="https://github.com/user-attachments/assets/3394a92c-f662-48dd-9ce4-d6b329642bc4" />




Tämä myös käynnisti HTTP-palvelimen tähän osoitteeseen: 

<img width="128" alt="image" src="https://github.com/user-attachments/assets/3ccb4365-988c-4a74-ac1c-f8001c9a2a06" />


Lähdin siis testaamaan selainyhteyttä katsoakseen avaisiko se nothing, nil, null, nada sivuston. 


<img width="366" alt="image" src="https://github.com/user-attachments/assets/42e5ed64-19fb-4836-875f-06f0bbee2006" />



Ja kalin firefoxissahan se avasi odotetusti. Tämän jälkeen siirryin fuffin lataukseen. 



(Olin jo hieman aikaisemmin tehtävänantoa ladannut jo fuffin. )

<img width="304" alt="image" src="https://github.com/user-attachments/assets/d616a168-d666-4347-ac9e-6303fae02d5f" />


Mutta tarkistin vielä varmuuden vuoksi asennuksen komennolla ffuf -h , joka listasi myös hyvin erilaisia komentoja, joita voi käyttää. 

<img width="320" alt="image" src="https://github.com/user-attachments/assets/00a56eef-f8e5-4b58-982f-91c54ec90f1d" />

Siirryin kuitenkin seuraavaan vaiheeseen, jossa latasin sanalistan. 


<img width="325" alt="image" src="https://github.com/user-attachments/assets/1e4caafc-01c9-4c75-84d7-8236cede599e" />


Tarkistin vielä sen sisällön ja se sisälsi päälle 4700 riviä. 

<img width="156" alt="image" src="https://github.com/user-attachments/assets/af605aaa-8ca1-4a7e-a694-3682a968529b" />

<img width="281" alt="image" src="https://github.com/user-attachments/assets/7961897d-5555-4463-9ea7-f14c3e21c66e" />


Tässä vaiheessa jäin hieman jumiin, joten yritin pähkäillä mm. erilaisia annettuja komentoja kuten ./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -fs 132 ja ffuf -u http://127.0.0.2:8000/FUZZ -w common.txt 

Tämä löysi erilaisia polkuja, kuten git/config ja index

<img width="325" alt="image" src="https://github.com/user-attachments/assets/364dbf4d-2daa-43ec-b5d5-40106d45fff7" />


Työkalulla curl, joka oli asennettuna kaliin sain selvitettyä vastauksen! Kokeilin molempia jäljellä olevia git/index ja git/configgia. 

<img width="319" alt="image" src="https://github.com/user-attachments/assets/3ad0226d-0d17-4e7d-b958-bf3699bd9301" />





b)

Siirryttiin siis b-kohtaan. Lisäsin annettuja komentoja, kuten dockerin asennus. 

<img width="299" alt="image" src="https://github.com/user-attachments/assets/65f7582f-ed9b-4558-a77e-f7f67424b7e8" />

Tämän jälkeen kloonasin sen, sillä lähdin ratkaisemaan target practice dockeria. 


<img width="327" alt="image" src="https://github.com/user-attachments/assets/281e258b-23fe-45d9-9410-6e87a3c45b7a" />


<img width="335" alt="image" src="https://github.com/user-attachments/assets/c0cc774a-8be2-4138-b2f9-2e69867341a6" />


Sitten pyöritin targetin, joka näytti näin. 

<img width="304" alt="image" src="https://github.com/user-attachments/assets/26071678-b1f9-45ac-88cd-cb351d343556" />

Ja pyöritin curlin komentoa käyttäen. Curl is a command line tool for transferring data with URL syntax, supporting DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET and TFTP. 


<img width="314" alt="image" src="https://github.com/user-attachments/assets/2c04d22b-c189-47b1-bde4-2ce2050436eb" />


Ja sain targetin ylös testatessa localhostia. 


<img width="497" alt="image" src="https://github.com/user-attachments/assets/eb7d9237-e0cd-466a-876d-fd2fe57dab9a" />


Asensin sen jälkeen kaikki wordlistit ja käynnistin fuffin.  

<img width="336" alt="image" src="https://github.com/user-attachments/assets/0634af7a-2ec8-4e75-b932-ab64b04f3d96" />


Suljin apachen hetkelliseksi, sillä se toi liikennettä port 80/tcp. 


<img width="323" alt="image" src="https://github.com/user-attachments/assets/6cff5a9d-ee57-48fa-a0d7-8ce7b373ace6" />


Tässä kohtaa docker näytti jostain syystä erroria.  


<img width="329" alt="image" src="https://github.com/user-attachments/assets/4b39f7f4-fae3-44ab-892e-5861c4512694" />


Ja löysin portit, jotka huomasivat liikennettä- 


<img width="331" alt="image" src="https://github.com/user-attachments/assets/029fe641-6478-46c4-88d6-301f35274f69" />





f) No 404 Status


Ja sitten suodatin kaikki, jossa ei ollut 669 tavua 


<img width="322" alt="image" src="https://github.com/user-attachments/assets/0773346b-c70f-4277-b473-9934bec6134c" />

Näin yksi line muodostui ja siitä muodostui secret



<img width="311" alt="image" src="https://github.com/user-attachments/assets/813e0051-f637-4055-8bd7-12321b7a2599" />



g) Param Mining




h) Rate Limited




i) Subdomains - Virtual Host Enumeration



# References

Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/


Hoikkala 2023: ffuf README.md https://github.com/ffuf/ffuf/blob/master/README.md


Kali 2025: tools - curl, https://www.kali.org/tools/curl/#curl



