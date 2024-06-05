# Արժեքների ո՞ր տիպին են պատկանում ֆունկցիաները: Բարձր կարգի ֆունկցիաներն (higher-order functions) ու ծրագրավորման ֆունկցիոնալ հայեցակարգը:

Ինչպես գիտենք ֆունկցիաները **JavaScript**-ում հանդիսանում են արժեքներ, և ամեն արժեք ունի իր տիպը։ Իսկ ո՞ր տիպին են պատկանում ֆունկցիաները։ JavaScript-ում ֆունկցիաները հանդիսանում են օբյեկտներ։ Ֆունկցիաներին կարելի է ոչ միայն կանչել, այլ նաև օգտագործել որպես սովորական օբյեկտներ, օրինակ նրանց մեջ ավելացնել/ջնջել հատկություններ։ Ստեղծենք պարզագույն ֆունկցիա, որի գործառույթը կլինի իրար գումարել և վերադարձնել տրված երկու արգումենտները։

```js
function sum(a, b) {
  return a + b;
}
```

Եթե հիմա մենք _typeof_ օպերատորի օգնությամբ ստուգենք sum-ի տիպը՝ typeof sum, ապա կստանանք "function"։ Ֆորմալ առումով սա ճիշտ չէ, քանի-որ JavaScript-ում չկա այդպիսի առանձին տվյալների տիպ, սակայն դա արվել է գործնական նպատակահարմարությունից ելնելով։ Որպեսզի իրոք համոզվենք, որ ֆունկցիաներն օբյեկտներ են, մենք կարող ենք նրանց մեջ ստեղծել հատկություններ, ինչպես որ սովորաբար օբյեկտների հետ ենք անում։

```js
sum.prop = "test";
```

Այժմ sum ֆունկցիայի մեջ կա prop հատկությունը՝ ինչ-որ "test" տեքստային արժեքով։ Եվ մենք կարող ենք օրինակ alert անել sum.prop-ը, դրանում համոզվելու համար։

Այս հնարքները գործնականում կարող են օգտագործվել տարբեր խնդիրների լուծման համար։ Օրինակ մեզ կարող է անհրաժեշտ լինել հաշվել թե քանի անգամ է ֆունկցիան կանչվել սքրիփթի մեջ։ Դրա համար ընդամենը պետք է ստեղծել ինչ-որ count հատկություն, որը կպահի հաշիվը, և ամեն անգամ ֆունկցիայի կանչի ժամանակ նրա արժեքը մեկով ավելացնել։

```js
function sum(a, b) {
  sum.count++;
  return a + b;
}

sum.count = 0;
```

Ունենք sum ֆունկցիան, որը վերադարձնում է տրված երկու արգումենտների գումարը, և ամեն կանչի ժամանակ իր count հատկության արժեքը ավելացնում է մեկով։ Անմիջապես ֆունկցիան հայտարարելուց հետո տալիս ենք նաև count հատկության նախնական արժեքը՝ 0։ Եվ այժմ եթե ֆունկցիան կանչվի, յուրաքանչյուր կանչը կավելացնի count-ի արժեքը մեկով։

```js
sum(5, 3); // 8
sum(2, 1); // 3
alert(sum.count); // 2
```

Ֆունկցիան ունի նաև մի շարք ներդրված հատկություններ, որոնք մենք կարող ենք ստանալ։ Օրինակ եթե alert անենք sum ֆունկցիայի name հատկությունը, կստանանք հենց ֆունկցիայի անվանումը։

```js
alert(sum.name); // "sum"
```

Կա նաև length ներդրված հատկությունը, որը պարունակում է ֆունկցիայի հայտարարման ժամանակ նրան տրված պարամետրերի քանակը։

```js
alert(sum.length); // 2
```

JavaScript ծրագրավորման լեզվում ֆունկցիաները բարձր կարգի են (_Higher-Order Function_), սա նշանակում է, որ ֆունկցիան որպես պարամետր կարող է ընդունել ուրիշ ֆունկցիա, կամ որպես արդյունք նույնպես վերադարձնել ինչ-որ ֆունկցիա։ JavaScript-ով կոդ գրելիս, սա շատ սովորական և տրամաբանական է թվում, սակայն պետք է ասել, որ ոչ բոլոր լեզուներում է հնարավոր ֆունկցիաները նման կերպ օգտագործել, և բարձր կարգի ֆունկցիաների առկայությունը համարվում է JavaScript-ի ամենաուժեղ կողմերից մեկը։ Այն ապահովում է աբստրակցիայի բարձր մակարդակ, թույլ է տալիս գրել ավելի համառոտ կոդ, և բարդ ու խճճված գործողությունները կատարել պարզ եղանակներով։

JavaScript-ի մեջ շատ կան ներդրված բարձր կարգի ֆունկցիաներ։ Օրինակ զանգվածների բոլոր մեթոդները որպես արգումենտ ստանում են հետադարձ կանչի (_callback_) ֆունկցիաներ, և զանգվածի էլեմենտների հետ աշխատում են ըստ այդ հետադարձ կանչի ֆունկցիաներում տրված տրամաբանության։ Բարձր կարգի ֆունկցիաների ունակությունը՝ վերադարձնել մեկ այլ ֆունկցիա, նույնպես հաճախ է կիրառվում, մասնավորապես _closure_-ների ստեղծման ժամանակ։

Ֆունկցիաների՝ ինչպես սովորական արժեքների հետ աշխատանքի սկզբունքը և բարձր կարգի ֆունկցիաների առկայությունը թույլ են տալիս JavaScript ծրագրավորման լեզվում որպես մոտեցում, որպես ոճ օգտագործել ֆունկցիոնալ ծրագրավորման հայեցակարգը։ Այն հանդիսանում է արժանի այլընտրանք օբյեկտ կողմնորոշված ծրագրավորման (_OOP_) հայեցակարգին և լայնորեն օգտագործվում է։