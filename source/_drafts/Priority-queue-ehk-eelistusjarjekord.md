---
title: Priority queue ehk eelistusjärjekord
date: 2018-02-25 10:10:20
tags:
authorIds: 
- taavi-ilves
---

## Mis see on?
Eelistusjärjekorra puhul on tegemist abstraktse andmestruktuuriga, mis on sarnane tavalisele järjekorra või pinu andmestruktuurile. Erinevus seisneb selles, et iga andmeelemendiga on seotud ka tema prioriteeti näitav väärtus. See tagab selle, et järjekorrast tagastatakse esimesena kõige kõrgema prioriteediga element ehk järjekord ei ole otseselt seotud elementide järjekorda lisamise järjekorraga.

## Tegevused
* isEmpty(): kontrolli, kas järjekord on tühi
* insert(): kontrolli, kas järjekord on tühi

``` javascript
function PriorityQueue() {
    this.data = [];
    this.length = 0;
}

PriorityQueue.prototype = {
	push: function (item) {
        this.data.push(item);
        this.length++;
        this._up(this.length - 1);
	},
}
```