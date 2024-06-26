# Ստորակետ (comma) օպերատորը JavaScript-ում: Ստորակետը որպես տարանջատիչ և որպես օպերատոր:

Մենք հաճախ ենք հանդիպում ստորակետի (,) կիրառությանը որպես տարանջատիչ։ Զանգվածի մեջ այն իրարից առանձնացնում է զանգվածի էլեմենտները, օբյեկտներում՝ հատկությունները, մեթոդների մեջ կարող է իրարից առանձնացնել արգումենտները։ Օրինակ՝

```js
const arr = [1, 2, 3, 4];
const car = { color: "red", speed: 250 };
Math.max(4, 2, 5, 7, 3);
```

Սակայն գոյություն ունի նաև ստորակետ (_comma_) օպերատոր, որն այնքան էլ հաճախ չի կիրառվում և հանդիսանում է երևի թե ամենաանսովոր օպերատորը: Այն, թեև շատ սահմանափակ կիրառություն ունի, այնուամենայնիվ իմանալ և աշխատանքի սկզբունքը հասկանալ պետք է, որովհետև երբեմն օգտագործվում է ավելի կարճ կոդ գրելու համար:

Ստորակետ օպերատորը մեզ թույլ է տալիս հաշվարկել մի քանի արտահայտություններ, դրանք իրարից տարանջատելով ստորակետի միջոցով։ Բոլոր արտահայտությունները կատարվում են, սակայն օպերատորը վերադարձնում է միայն վերջին արտահայտության արդյունքը։ Օրինակ՝

```js
let a = (2 ** 3, 4 / 2, 1 + 2);
console.log(a); // 3
```

Առաջին արտահայտությունը՝ _2 \*\* 3_ կատարվում է, սակայն արդյունքը՝ _8_-ը դեն է նետվում։ Ապա կատարվում է երկրորդ արտահայտությունը՝ _4 / 2_, և ստացված արդյունքը՝ _2_-ը, նույնպես անտեսվում է։ Եվ վերջապես կատարվում է երրորդ արտահայտությունը՝ _1 + 2_, և քանի-որ այն վերջինն է, ստացված արդյունքը՝ _3_-ը, օպերատորը վերադարձնում է, և այն վերագրվում է _a_ փոփոխականին։

Ստորակետ օպերատորն ունի շատ **ցածր առաջնահերթություն** (_Operator precedence_), [այս հղումով](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence?fbclid=IwAR0lky3GjG4TlvRKn3tK_gD2DMi0q9PQ85MpF64-9pWPZFM8wezbcC9hqkY) եթե նայենք **JavaScript**-ի բոլոր օպերատորների առաջնահերթության սանդղակը, ապա կտեսնեք, որ ստորակետը վերջին տեղում է _1_ առաջնահերթության ինդեքսով (_ինչքան ինդեքսը բարձր է, այնքան բարձր է օպերատորի առաջնահերթությունը, օրինակ խմբավորման օպերատոր հանդիսացող փակագծերի առաջնահերթության ինդեքսը 21 է, որն ամենաբարձրն է սանդղակի մեջ_):

Քանի-որ առաջնահերթության սանդղակում ստորակետն ամենացածր ինդեքսն ունի, ապա վերևում բերված օրինակի մեջ փակագծերի կիրառությունը պարտադիր է՝ օպերատորի օգտագործման կանխատեսելի արդյունքը ստանալու համար։

Ստորակետ օպերատորի օգտագործմամբ՝ մի տողի վրա մի քանի արտահայտությունների կատարման հնարքն այնքան էլ ողջունելի չէ, քանի-որ զգալիորեն վատթարացնում է կոդի ընթեռնելիությունը։ Սակայն որոշ դեպքերում այն կարող է օգտագործվել հակիրճ և էլեգանտ կոդ գրելու համար, որը նաև բավականին հասկանալի կլինի։ **JavaScript**-ի մի շարք գրադարաններ լայնորեն կիրառում են այդ հնարքները:

Կիրառության մեկ օրինակ՝ **Stack Overflow**-ից։

```js
for (let a = 1, b = 10; a < b; a++, b--) {
  console.log(new Array(b - a).join("*"));
}
```

Կոնսոլում կնկարվի հետևյալ պատկերը՝

```
*********
*****************
***********************
***************************
*****************************
***************************
***********************
*****************
*********
```
