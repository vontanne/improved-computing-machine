# Ի՞նչ է NaN-ը և ինչպե՞ս ստուգել արժեքն արդյոք հավասար է NaN-ի: Ինչպե՞ս հնարավորինս խուսափել իրավիճակներից, որոնց արդյունքում կստանանք NaN: Նաև մի փոքր անվերջության և մինուս անվերջության մասին:

**JavaScript**-ում թվերը ներկայացվում են **IEEE 754** ստանդարտով սահմանված **`double-precision`** (_երբեմն ուղղակի անվանում են Double_) ձևաչափով։ Վերջին լրացումներն այս ստանդարտի մեջ արվել են 2008 թվականին։ **JavaScript**-ում բացի մեզ քաջածանոթ դրական և բացասական ամբողջ և կոտորակային թվերից, 0-ից և մինուս 0-ից, կան նաև 3 հատուկ թվային արժեքներ՝ անվերջություն (**`Infinity`**), մինուս անվերջություն (**`-Infinity`**) և **`NaN`**:

**`Infinity`**-ին դա հատուկ թվային արժեք է, իրենից ներկայացնում է դրական անվերջություն, և մեծ է ցանկացած թվից։ Նույն կերպ **`-Infinity`**-ին հանդիսանում է բացասական անվերջություն, և փոքր է ցանկացած թվից։ **`NaN`**-ը թեև թարգմանվում է որ թիվ չէ (_Not a Number_), իրականում հանդիսանում է **ՀԱՏՈՒԿ ԹՎԱՅԻՆ ԱՐԺԵՔ**։ Այն սխալ կամ անորոշ մաթեմատիկական գործողության արդյունք է, և կարծես հանդիսանում է «ինդիկատոր», որ կոդի մեջ ինչ որ տեղ սխալ կա։

```js
typeof window.NaN; // "number"
typeof globalThis.NaN; // "number"
```

Ինչպես տեսնում ենք այն գլոբալ օբյեկտի հատկություն է հանդիսանում։ Նշենք այն գործողությունները, որոնց արդյունքում վերադարձվում է **`NaN`**՝

- Բոլոր այն մաթեմատիկական գործողությունները, որտեղ թեկուզև մի օպերանդը հանդիսանում է _NaN_: _NaN_-ի հետ ցանկացած մաթեմատիկական գործողություն կվերադարձնի _NaN_:

- Երբ 0-ն բաժանենք 0-ի վրա։ Հիշեցնեմ որ եթե 0-ից տարբեր թիվ բաժանենք 0-ի վրա, ապա կախված նրանից թե թիվը դրական է կամ բացասական, կստանանք համապատասխանաբար _Infinity_ և _-Infinity_:

- Երբ անվերջությունը բաժանենք անվերջության վրա։ (ինչպես _Infinity_-ի, այնպես էլ _-Infinity_-ի դեպքում):

- Երբ 0-ն բազմապատկենք անվերջության կամ մինուս անվերջության հետ։

- Երբ իրար գումարենք դրական և բացասական անվերջությունները։

- Երբ փորձենք բացասական թվից քառակուսի արմատ հանել։

- Երբ փորձենք ստանալ բացասական թվի լոգարիթմը։

- Երբ մաթեմատիկական գործողության մեջ օպերանդներից մեկը _undefined_ է։ Ի դեպ գործնականում սա համարվում է հիմնական պատճառներից ամենատարածվածը, և նույնիսկ ասացվածք-հուշում կա, որ _ԵԹԵ ՍՏԱՑԵԼ ԵՍ NaN, ՓՆՏՐԻՐ undefined-ը_

- Հնարավոր է նաև Number կամ parseInt, parseFloat ֆունկցիաների աշխատանքի հետևանքով, երբ նրանք չեն կարողանում իրենց հաղորդած արգումենտը «զտել» և վերափոխել թվային արժեքի։

Սրանք ամենատարածված տարբերակներն են,բայց ցուցակը ամբողջական չէ, և հնարավոր են նաև այլ դեպքեր։ Եթե արժեքը թվային է, սակայն մենք վստահ չենք այն «սովորական» թվային արժեք է, թե հատուկ, ապա գոյություն ունեն տարբեր եղանակներ և ներդրված ֆունկցիաներ, որոնց օգնությամբ մենք կարող ենք դա ստուգել։

Օրինակ դա հեշտությամբ կարելի է անել հիմնվելով **`NaN`**-ի մի հետաքրքիր առանձնահատկության վրա, որ այն հավասար չէ ոչ մի բանի, անգամ ինքն իրեն։ (Եթե ստուգենք **`NaN === NaN`** արտահայտությունը, ապա այն կվերադարձնի `false`) :

```js
const someNumber = NaN;
if (someNumber !== someNumber) {
  console.log("is NaN");
} else {
  console.log("is'nt NaN");
}
```

Այստեղ ուղղակի համեմատում ենք փոփոխականն ինքն իր հետ։ Միայն մի դեպքում փոփոխականի արժեքը կարող է ինքն իրեն հավասար չլինել՝ երբ այն **`NaN`** է։ Մենք կարող ենք վերևում նշվածն օգտագործելով հեշտությամբ ստեղծել ֆունկցիա, որին կտանք արգումենտ, իսկ ֆունկցիան մեզ կվերադարձնի արդյոք այն **`NaN`** է թե ոչ։ Բայց այդ ամենը մեր փոխարեն արդեն արել են, և JavaScript-ում դրա համար կա հատուկ ներդրված ֆունկցիա՝ `isNaN`: **ES6**-ում որպես այլընտրանք կարող ենք օգտագործել նաև `Number.isNaN` մեթոդը։ Նրանց միջև կա մի փոքրիկ տարբերություն, որին կանդրադառնամ․

```js
isNaN(42); // false
Number.isNaN(42); // false
isNaN(Math.sqrt(-12)); // true
Number.isNaN(Math.sqrt(-12)); // true
```

Վերևի 2 օրինակում նրանք միանման են աշխատում։ Իսկ նրանց տարբերությունը կայանում է նրանում, որ `isNaN` ֆունկցիան արգումենտը վերածում է _Number տիպի_, նոր ստուգում է արդյոք այն **`NaN`** է թե ոչ։ **Number.isNaN** մեթոդը միայն ստուգում է արժեքը տվյալ պահին **`NaN`** է, թե ոչ։ Որպեսզի ամեն ինչ ավելի հասկանալի լինի, բերեմ օրինակ․

```js
isNaN("hello world"); // true
Number.isNaN("hello world"); // false
```

Շատ հաճախ մեզ անհրաժեշտ է լինում ստուգել, որ արժեքը ոչ միայն **`NaN`**, այլև մյուս հատուկ թվային արժեքներին նույնպես չպատկանի (**`Infinity և -Infinity`**): Դրա համար գոյություն ունի մի հրաշալի և ունիվերսալ Ֆունկցիա՝ `isFinite`։ Այն ոչ մի օբյեկտի հետ կապված չէ, և եթե որպես արգումենտ հաղորդում ենք որևէ արժեք, ապա վերադարձնում է արդյոք այն սովորական թվային արժեք է, թե ոչ։ Բերեմ օրինակներ՝

```js
isFinite(0); // true
isFinite(2e64); // true
isFinite(Infinity); // false
isFinite(NaN); // false
isFinite(-Infinity); // false
```

Գոյություն ունի նաև `Number.isFinite` մեթոդը, որը տարբերվում է `isFinite` գլոբալ ֆունկցիայից նրանով, որ տրված արգումենտը հարկադրաբար չի վերածում _Number_ տիպի և նոր ստուգում։ (_Ինչպես isNaN() vs Number.isNaN() ի դեպքում_): Օրինակ՝

```js
Number.isFinite(Infinity); // false
Number.isFinite(NaN); // false
Number.isFinite(-Infinity); // false
Number.isFinite(0); // true
Number.isFinite(2e64); // true
Number.isFinite("0"); // false
```

Ուշադրություն դարձնենք վերջին օրինակին։ Եթե մենք `isFinite` գլոբալ ֆունկցիային որպես արգումենտ հաղորդեյինք "0", ապա այն կվերադարձներ true: Բացի այս մեթոդներից **ES6**-ում ներդրվել է ևս մի շատ հետաքրքիր մեթոդ, որը որոշում է թե արդյոք տրված երկու արժեքները նույնն են հանդիսանում։ Այդ մեթոդը `Object.is` -ն է, այն արժեքների համեմատությունը կատարում է ինչպես խիստ հավասարության (===) դեպքում, այն տարբերությամբ միայն, որ ավելի հուսալի է աշխատում, և օրինակ **`NaN`**-ը **`NaN`**-ի հետ համեմատելու արդյունքում վերադարձնում է `true`: (այսինքն որ դրանք նույնն են, ինչպես հիշում ենք === ով ստուգելու դեպքում վերադառնում էր `false`):

```js
Object.is(NaN, Math.sqrt(-12)); // true
```

Ինչպես տեսնում ենք՝ երկրորդ պարամետրի արտահայտությունը հաշվարկվում է որպես **`NaN`**, և համեմատելով առաջին պարամետրին տրված **`NaN`** արժեքի հետ, վերադարձնում է որ այո՛, նրանք հավասար են։