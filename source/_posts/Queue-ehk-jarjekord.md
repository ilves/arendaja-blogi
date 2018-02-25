---
title: Queue ehk järjekord
date: 2018-02-25 10:49:26
tags: 
- andmestruktuurid
authorIds: 
- taavi-ilves
---

![alt text](https://cdn-images-1.medium.com/max/2000/1*cXqsegIn_iAAboiryWFSyw.jpeg "")

Järjekord on üks lihtsamaid ja laialt kasutatud andmestruktuur. Järjekorda lisatud elemendid tagastatakse lisamise järjekorras ehk esimesena lisatud element tagastatakse esimesena. Inglise keeles kasutatakse väljendit FIFO (First-In-First-Out).

Hea näide elust on poejärjekord. Esimesena teenindatakse järjekorras esimest inimest. Iga lisandunud inimene läheb järjekorra lõppu.

### Kasutusalad
* Ajaplaanimine (scheduling) - Näiteks veebiserveril on limiit, kui mitu päringut ta suudab samaaegselt täita. Mõned serverid lisavad päringu järjekorda ning kui mõne varasema päringu täitmine lõppeb, võetakse järjekorrast järgmine.

<!-- more -->

## Teostus
Järgnevalt loome järjekorra andmestruktuuri kasutades javascripti. Reaalses elus on võimalik järjekorrana kasutada ka ainult massiivi, aga õppimise eesmärgil teeme seda natuke keerukamalt. See võimaldab sarnast koodi kasutada teiste, keerukamate järjekorra tüüpide õppimise puhul.

### Tegevused
Järjekorra andmestruktuur peaks sisaldama vähemalt järgmisi tegevusi:

* `insert(item)` - lisab elemendi järjekorra lõppu
* `take()` - võtab elemendi järjekorra algusest

``` javascript
function Queue() {
  this.queue = [];
  this.length = 0;
}

Queue.prototype = {
  insert: function (item) {
    this.queue.push(item);
    this.length++;
  },
  take: function () {
    if (this.length === 0) {
      return undefined;
    }
    this.length--;
    return this.queue.shift();
  }
}
```

* Rida 1: Loome järjekorra objekti
* Rida 2: Loome tühja massiivi (`array`) elementide hoidmiseks
* Rida 3: Loome muutja elementide arvu hoidmiseks
* Rida 6: Lisame `Queue` objektile `insert` ja `take` operatsioonid ([loe rohkem](https://www.w3schools.com/js/js_object_prototypes.asp))
* Rida 8: Lisame elemendi masiivi lõppu
* Rida 9: Suurendame elementide arvu
* Rida 12: Kontrollime kas elementide arv on `0`
* Rida 13: Kui elemente rohkem ei ole, tagastame tühja väärtuse (`undefined`)
* Rida 15: Vähendame elementide arvu
* Rida 16: Võtame massiivi algusest elemendi

#### Näide kasutamisest

``` javascript
var queue = new Queue();
queue.insert(1);
queue.insert(2);
queue.insert(3);

console.log(queue.take())
console.log(queue.take())
console.log(queue.take())
console.log(queue.take())
```

* Rida 1: Loob uue järjekorra objekti
* Rida 2-4: Lisab järjekorda kolm elementi
* Rida 6-8: Võtab järjekorrast lisatud elemendid järjekorras 1,2,3
* Rida 9: Proovib võtta elementi tühjast järjekorrast, elemendi asemel saame vastuseks `undefined`