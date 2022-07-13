# Predviđanje starosti i cenzura maloletnih lica

Ideja projekta jeste predviđanje starosti osobe na osnovu fotografije i cenzura fotografija maloletnih osoba (blur). Ovakav projekat se može nadograditi i koristiti u mnoge svrhe.

Za predviđanje starosti osobe korišćena je konvolutivna neuronska mreža resnet50 koja se pokazala veoma uspešnom kada su pitanju biometrijske tehnologije, odnosno prepoznavanja lica. Realizacija je sprovedena uz pomoć wrapper-a ktrain koji se zasniva TensorFlow (Keras) i služi kao pomoć u izgradnji, obuci i primeni neuronskih mreža i drugih modela mašinskog učenja. Inspirisan proširenjima ML okvira kao što su FastAI i Ludvig, ktrain je dizajniran da učini duboko učenje i veštačku inteligenciju pristupačnijom i lakšom za primenu. Detaljnije informacije i uputstva za instalaciju: https://github.com/amaiya/ktrain.

Podaci koji su korišćeni preuzeti su sa Kaggle-a i dostupni su na sledećem linku: https://www.kaggle.com/datasets/jangedoo/utkface-new. UTKFace je veliki skup fotografija sa rasponom starosti od 0 do 116 godina, dok je za potrebe ovog projekta taj raspon smanjen od 0 do 43 godine. Originalan skup podataka se sastoji od preko 20.000 slika lica sa napomenama o starosti, polu i etničkoj pripadnosti, dok je za izradu ovog projekta korišćeno 103 nasumično odabrane fotografije. Fotografije pokrivaju velike varijacije u pozi, izrazu lica, osvetljenju, okluziji i rezoluciji.

## Analiza rada

![Screenshot from 2022-07-13 14-09-07](https://user-images.githubusercontent.com/46380340/178732482-28c58fd5-3d36-4251-8eaa-2973d731b6eb.png)

text 

![Screenshot from 2022-07-13 14-11-13](https://user-images.githubusercontent.com/46380340/178732490-675c601a-eae4-4cd4-8760-eefe15890ee7.png)
![Screenshot from 2022-07-13 14-11-37](https://user-images.githubusercontent.com/46380340/178732505-212e3f49-7261-4389-bb08-621bdf05e5a5.png)

## Rezultati

![Screenshot from 2022-07-13 14-10-49](https://user-images.githubusercontent.com/46380340/178732460-659f2b86-6bc7-4214-aa99-d6452239a906.png)

## Potencijalna unapređenja
