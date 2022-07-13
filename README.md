# Predviđanje starosti i cenzura maloletnih lica

Ideja projekta jeste predviđanje starosti osobe na osnovu fotografije i cenzura fotografija maloletnih osoba (blur). Ovakav projekat se može nadograditi i koristiti u mnoge svrhe.

Za predviđanje starosti osobe korišćena je konvolutivna neuronska mreža resnet50 koja se pokazala veoma uspešnom kada su pitanju biometrijske tehnologije, odnosno prepoznavanja lica. Realizacija je sprovedena uz pomoć wrapper-a ktrain koji se zasniva TensorFlow (Keras) i služi kao pomoć u izgradnji, obuci i primeni neuronskih mreža i drugih modela mašinskog učenja. Inspirisan proširenjima ML okvira kao što su fastai i ludvig, ktrain je dizajniran da učini duboko učenje i veštačku inteligenciju pristupačnijom i lakšom za primenu. Detaljnije informacije i uputstva za instalaciju: https://github.com/amaiya/ktrain.

Podaci koji su korišćeni preuzeti su sa Kaggle-a i dostupni su na sledećem linku: https://www.kaggle.com/datasets/jangedoo/utkface-new. UTKFace je veliki skup fotografija sa rasponom starosti od 0 do 116 godina, dok je za potrebe ovog projekta taj raspon smanjen od 0 do 43 godine. Originalan skup podataka se sastoji od oko 23000 slika lica sa napomenama o starosti, polu i etničkoj pripadnosti, dok je za izradu ovog projekta korišćeno 103 nasumično odabrane fotografije. Fotografije pokrivaju velike varijacije u pozi, izrazu lica, osvetljenju, okluziji i rezoluciji.

## Analiza rada

### Prikupljanje podataka:
  S obzirom na to da prikupljene fotografije u svom nazivu sadrže informaciju o uzrastu osobe i većina naziva prati isti šablon, kako bi informacije o godinama bile verodostojne i izvučene sa što manje grešaka, uzete su samo one fotografije koje odgovaraju šablonu većine (prvi broj u nazivu fotografije predstavlja broj godina).

### Predvidjanje:
Za određivanje train i test skupa, podešavanja random state-a, kreiranje modela i predikciju rezultata korišćena je vision biblioteka. Zadatak se svodi na problem regresije kako bi se odredile tačne predviđene godine. Korišćene su samo dve epohe, sa learning rate-om 1e-4. Nakon toga isti je postupak ponovljen radi postizanja boljih rezultata. Prediktor nad većim podacima može biti sačuvan uz pomoć komande:

**predictor.save("naziv_foldera_prediktora")**

i učitan ponovo uz pomoć komande: 

**(predictor = ktrain.load_predictor('naziv_foldera_prediktora')**

Ovaj projekat je previše malih razmera da bi bilo potrebno čuvati prediktor i sve epohe se izvršavaju svega nekoliko minuta dok je za originalan dataset potrebno oko 14 sati.

### Prikaz rezultata: 
Funkcija show_pred za unet naziv fotografije prikazuje fotografiju sa zaokruženim rezultatima predviđanja i realnim podacima.


![Screenshot from 2022-07-13 14-09-07](https://user-images.githubusercontent.com/46380340/178732482-28c58fd5-3d36-4251-8eaa-2973d731b6eb.png)

Svi predviđeni i realni podaci, zajedno sa nazivima fotografija čuvaju se u dataframe-u uz pomoć funkcije calculate_predictions i python-ove ugrađene funkcije map. (map omogućava brzo izvršavanje te je pogodan za rad i sa originalnim datasetom)

### Cenzura: 

Ukoliko je lice po predviđenim godinama maloletno, njegovo lice će biti zamagljeno Gausovom metodom.

![Screenshot from 2022-07-13 14-11-13](https://user-images.githubusercontent.com/46380340/178732490-675c601a-eae4-4cd4-8760-eefe15890ee7.png)
![Screenshot from 2022-07-13 14-11-37](https://user-images.githubusercontent.com/46380340/178732505-212e3f49-7261-4389-bb08-621bdf05e5a5.png)

## Rezultati

S obzirom na to da je u fokusu da li je osoba maloletna ili ne, najvećom greškom se smatra situacija u kojoj je lice maloletno a proglasi se punoletnim jer u tom slučaju njegovo lice neće biti dalje zamagljeno.
Nakon što su godine starosti i realnih i predviđenih podataka podeljene u dve grupe "Maloletan" i "Punoletan", izračunata je matrica konfuzije: 

![Screenshot from 2022-07-13 14-10-49](https://user-images.githubusercontent.com/46380340/178732460-659f2b86-6bc7-4214-aa99-d6452239a906.png)

koja prikazuje relativno mali stepen greške pri predviđanju.

- Srednja apsolutna greška (MAE): 4.3887987
- Preciznost: ~65%
- Tačnost: ~65%

## Potencijalna unapređenja

Kako bi model pravio manje grešaka potrebno je uključiti znatno veći broj podataka (fotografija) nad kojima bi učila mreža, svih godina. Ovaj projekat predstavlja samo kostur uspešnog projekta. Takođe, bilo bi neophodno povećati broj epoha. 
Potencijalna dodatna unapređenja bi se ogledala u optimizaciji krajnjeg modela (u zavisnosti od toga za koju je meru evaluacije važnije dobiti bolji rezultat) i potencijalnom optimizacijom learning rate-a.

Ceo projekat je moguće posmatrati umesto iz ugla regresije iz ugla klasifikacije, gde bi jedna klasa predstavljala maloletna lica a druga punoletna lica, te ovaj način u nekim slučajevima može potencijalno dati bolje rezultate.



_Andrijana Živić
Jul, 2022._
