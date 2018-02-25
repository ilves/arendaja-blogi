---
title: Stack ehk pinu
date: 2018-02-25 10:49:26
tags: 
- andmestruktuurid
authorIds: 
- taavi-ilves
---

<img src="https://cdn-images-1.medium.com/max/800/1*_tGKhIx1bDwHpBDDM0HsDw.jpeg" style="margin-left:2em; float:right; width:50%; max-width: 300px;" />

Pinu (stack) on sarnaselt [järjekorraga](/2018/02/25/Queue-ehk-jarjekord/) üks lihtsamaid ja laialt kasutatud andmestruktuure. Erinevalt järjekorrast tagastatakse esimesena viimasena lisatud element. Inglise keeles kasutatakse väljendit LIFO (Last-In-Last-Out).

Hea näide elust on taldrikute virn, mis ootab pesemist. Iga lisandunud must taldrik lisatakse virna otsa ning järgmist taldrikut pesema hakkates, võetakse taldrik virna tipust.

### Kasutusalad
* Võta tagasi / taasta (undo / redo ) - Peaaegu igas tekstiredaktoris on võimalik võtta tagasi viimaseid muudatusi või tagasi võetud tegevusi taastada
* Sõne tagurpidi keeramine - Lisa sõna pinusse ühe tähe kaupa (näiteks: k o e r) ja loe sealt andmed tagasi (näiteks: r e o k)

<!-- more -->

## Teostus
Järgnevalt loome pinu andmestruktuuri kasutades javascripti. Reaalses elus on võimalik pinuna kasutada ka ainult massiivi, aga õppimise eesmärgil teeme seda natuke keerukamalt. See võimaldab sarnast koodi kasutada teiste, keerukamate andmestruktuuride tüüpide õppimise puhul (vaata näiteks [järjekorra teostust](/2018/02/25/Queue-ehk-jarjekord/#Teostus)).

### Tegevused
Pinu andmestruktuur peaks sisaldama vähemalt järgmisi tegevusi:

* `insert(item)` - lisab elemendi virna tippu
* `take()` - võtab elemendi virna tipus

``` javascript
function Stack() {
  this.queue = [];
  this.length = 0;
}

Stack.prototype = {
  insert: function (item) {
    this.queue.push(item);
    this.length++;
  },
  take: function () {
    if (this.length === 0) {
      return undefined;
    }
    this.length--;
    return this.queue.pop();
  }
}
```

* Rida 1: Loome pinu objekti
* Rida 2: Loome tühja massiivi (`array`) elementide hoidmiseks
* Rida 3: Loome muutja elementide arvu hoidmiseks
* Rida 6: Lisame `Stack` objektile `insert` ja `take` operatsioonid ([loe rohkem](https://www.w3schools.com/js/js_object_prototypes.asp))
* Rida 8: Lisame elemendi masiivi lõppu
* Rida 9: Suurendame elementide arvu
* Rida 12: Kontrollime kas elementide arv on `0`
* Rida 13: Kui elemente rohkem ei ole, tagastame tühja väärtuse (`undefined`)
* Rida 15: Vähendame elementide arvu
* Rida 16: Võtame massiivi lõpust elemendi


#### Näide kasutamisest

``` javascript
var stack = new Stack();
stack.insert(1);
stack.insert(2);
stack.insert(3);

console.log(stack.take())
console.log(stack.take())
console.log(stack.take())
console.log(stack.take())
```

* Rida 1: Loob uue pinu objekti
* Rida 2-4: Lisab pinusse kolm elementi
* Rida 6-8: Võtab pinust lisatud elemendid järjekorras 3,2,1
* Rida 9: Proovib võtta elementi tühjast pinust, elemendi asemel saame vastuseks `undefined`