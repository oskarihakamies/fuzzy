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


Testaamalla curl komennolla ja ensin git/configgia kalissa sain vastauksen selville!

<img width="319" alt="image" src="https://github.com/user-attachments/assets/3ad0226d-0d17-4e7d-b958-bf3699bd9301" />





b)












# References

Karvinen 2023: Find Hidden Web Directories - Fuzz URLs with ffuf. https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/


Hoikkala 2023: ffuf README.md https://github.com/ffuf/ffuf/blob/master/README.md
