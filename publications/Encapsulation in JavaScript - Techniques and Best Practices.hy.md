# Ի՞նչ է ինկապսուլյացիան։ Մասնավոր (private) հատկություններն ու մեթոդները JavaScript ծրագրավորման լեզվում։

Ինկապսուլյացիա (_անգլ․ encapsulation բառից_) եզրը կարելի է հասկանալ որպես ինչ֊որ բանի մեկուսացում, դրա վրա դրսից արտաքին միջամտությունները բացառելու կամ հնարավորինս փոքրացնելու համար։ Այն կարելի է ընկալել նաև որպես մեխանիզմ, որը մեզ հնարավորություն է տալիս տեսնել գլխավորն ու կարևորը՝ երկրորդական կամ խանգարող բաները ինչ֊որ պայմանական կապսուլի մեջ սահմանափակելով։

Ինկապսուլյացիայի օրինակները մեր շուրջը բազմաթիվ են։ Դիտարկենք հեռուստացույցի օրինակը։ Հեռակառավարման վահանակի օգնությամբ կարելի է փոխել հեռուստաալիքները, բարձրացնել կամ ցածրացնել հեռուստացույցի ձայնը, փոխել էկրանի պայծառության չափը և այլն։

Այդ առաջին հայացքից պարզ թվացող գործողությունները կատարելու ժամանակ հեռուստացույցի ներսում կարող են մի շարք փոխազդեցություններ տեղի ունենալ տարբեր բլոկների, դետալների միջև, սակայն այդ ամենը մեզանից խնամքով թաքցված է։ Այսինքն գոյություն ունի հեռուստացույցի արտաքին և ներքին ինտերֆեյս։

Ներքին ինտերֆեյսն օգտագործվում է օբյեկտի աշխատանքի ընթացքում։ Օբյեկտի դետալները փոխազդեցության մեջ են իրար հետ։ Բայց արտաքինից այդ ամենը խնամքով թաքցրած է հեռուստացույցի պատյանի տակ, և դետալները տեսանելի չեն։ Մենք նրանց կարող ենք օգտագործել միայն արտաքին ինտերֆեյսի օգնությամբ։

Ինֆորմատիկայում ինկապսուլյացիան կատարում է նույն դերը՝ այն փաստացի ծրագրավորման մեխանիզմ է, որը թույլ է տալիս սահմանափակել դասերի հատկություններին և մեթոդներին դրսից հասանելիությունը՝ վերահսկելի դարձնելով նրանց հետ կատարվող գործողությունները։

Թեև ծրագրավորման մեջ ինկապսուլյացիան շատ հաճախ դիտարկվում է որպես բացառապես Օբյեկտ Կողմնորոշված Ծրագրավորման հետ սերտորեն կապված մեխանիզմ, իրականում այն ավելի ընդգրկուն է։

Օրինակ մի շարք ֆունկցիոնալ լեզուներում տարածված է ինկապսուլյացիայի մեխանիզմի իրագործումը հատուկ տեսակի ֆունկցիաների օգնությամբ։ Նրանք հայտարարվում են այլ ֆունկցիաների մեջ, և հասանելիություն են ունենում արտաքին ֆունկցիայի լոկալ փոփոխականներին։ **JavaScript**-ը, որպես բազմահարացուցային լեզու, հիմնականում տիպիկ ֆունկցիոնալ լեզուներին բնորոշ այդ մեխանիզմը նույնպես օգտագործում է, ընդ որում շատ հաճախակի (_closure֊ները_):

Այժմ վերացական տեսական դատողություններից անցնենք կոնկրետ օրինակների քննարկմանը։ **JavaScript**-ում օբյեկտների հատկություններն ու մեթոդները կարող են լինել հասանելի և մասնավոր (_private_): Մի շարք տարածված ծրագրավորման լեզուներում (_օրինակ C++, C#, Java_) ծրագրի մեջ բոլոր տեղերից հասանելի դաշտերի ստեղծման համար օգտագործվում է _public_, իսկ մասնավոր, միայն դասի մեջ տեսանելի դաշտերի համար՝ _private_ բանալի բառը։

**JavaScript**-ում որոշել են այլ կերպ իրականացնել դա, ծրագրի շրջանակում բոլոր տեղերից հասանելի հատկությունների և մեթոդների համար ոչ մի լրացուցիչ բանալի բառ չի օգտագործվում, իսկ եթե հատկությունը կամ մեթոդը պետք է ստեղծել «փակ», տեսանելի միայն դասի ներսում, ապա դրանցից առաջ դրվում է **#** նշանը։

Պետք է նշել, որ վերոհիշյալ ծրագրավորման լեզուներում (_C++, C#, Java և այլն_) կա նաև հնարավորություն ստեղծել այպես կոչված «պաշտպանված» դաշտեր և մեթոդներ, որոնք հասանելի են միայն տվյալ դասի և նրա ժառանգների համար (_Օգտագործվում է protected բանալի բառը_)։ **JavaScript**-ում դա նախատեսված չէ, սակայն որոշակի պայմանավորվածություններով հնարավոր է էմուլացնել։

Այժմ ստեղծենք _Person_ դասը, որի հատկությունները սկզբում կլինեն հասանելի, իսկ հետո կսարքենք փակ, մասնավոր (_private_): Եվ կտեսնենք, թե ինչ առավելություններ ունի երկրորդ տարբերակը՝ համեմատած առաջինի։

```js
class Person {
  name;
  age;
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greeting() {
    console.log(`hello ${this.name}`);
  }
}
```

Դասն ունի երկու դաշտ՝ _name_ և _age_, և մեկ սովորական մեթոդ, որի կանչի ժամանակ ուղղակի կոնսոլում տպվում է ողջույնի խոսք։ Երբ մենք այս դասի հիման վրա ստեղծում ենք օբյեկտներ, ապա նրանց դաշտերին կոնստրուկտորի օգնությամբ վերագրվում են համապատասխան արժեքները։ Փորձենք ստեղծել օբյեկտ, և տեսնել թե ինչ կարող ենք անել նրա դաշտերի հետ։

```js
const person = new Person("Joe", 25);
person.greeting(); // hello Joe
person.age = 150;
console.log(person); // { name: 'Joe', age: 150 }
```

Օբյեկտի ստեղծման ժամանակ մենք կոնստրուկտորի օգնությամբ նրան տվեցինք անուն և տարիք։ Սակայն քանի֊որ օբյեկտի հատկությունները հասանելի են դրսից, շատ հնարավոր է անկառավարելի, անգամ անհեթեթ արժեքներ վերագրվեն տվյալ հատկություններին, կամ այդ վերագրումներն արվեն ոչ այն ժամանակ, երբ պետք է։

Իհարկե նման փոքրիկ օրինակի վրա հնարավոր չէ պատկերացնել թե դա ինչպես կարող է տեղի ունենալ, սակայն պատկերացրեք չափազանց մեծ նախագիծ, բաղկացած հազարավոր կամ տասնյակ հազարավոր տողերից, որի վրա աշխատում է մեծ թիմ։

Այդպիսի դեպքերում չի կարելի բացառել, որ սխալմամբ կամ անուշադրության արդյունքում մեծ քանակությամբ սխալ վերագրումներ լինեն՝ դրանից բխող հետևանքներով։ Ճիշտ իրականացված ինկապսուլյացիան օգնում է խուսափել մեծ քանակությամբ խնդիրներից։ Օրինակ մեր պարագայում կարող ենք դաշտերին հասանելիություն տալ միայն դասի շրջանակներում՝ այդպիսով ապահովագրելով մեզ օբյեկտների հատկությունների սխալ վերագրումներից։

```js
class Person {
  #name;
  #age;

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  greeting() {
    console.log(`hello ${this.#name}`);
  }
}

const person = new Person("Joe", 25);
person.greeting(); // hello Joe
console.log(person.age); // undefined
console.log(person.name); // undefined
```

Ինչպես տեսնում ենք _greeting_ մեթոդը շարունակում է աշխատել, քանի֊որ այն հասանելիություն ունի դասի ներսում գտնվող name դաշտին, սակայն դրսից հիմա եթե ուզենանք տեսնել name և age դաշտերի արժեքները, կամ փոխել դրանք, մենք չենք կարողանա։

Այդ սահմանափակումը շատ խիստ է, և կարելի է օրինակ հնարավորություն տալ տեսնելու, կարդալու հատկությունները, սակայն չտալ հասանելիություն՝ դրանք փոխելու։ Դրա համար կարելի է ստեղծել մեթոդներ, որոնք կլինեն հասանելի դասից դուրս, և դասի մեջ հասանելի դաշտերի արժեքները «տեսանելի» կդարձնեն մեզ համար։

```js
class Person {
  #name;
  #age;

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  getAge() {
    return this.#age;
  }

  getName() {
    return this.#name;
  }

  greeting() {
    console.log(`hello ${this.#name}`);
  }
}

console.log(person.getAge()); // 25
console.log(person.getName()); // Joe
```

_getAge_ և _getName_ մեթոդները մեզ հնարավորություն տվեցին կարդալ _person_ օբյեկտի հատկությունները։ Մենք կարող ենք նաև ստեղծել մեթոդներ, որոնք մեզ հնարավորություն կտան փոխել «փակ» հատկությունների արժեքները, սակայն թույլատրելիի շրջանակներում։ Այսինքն մենք կարող ենք ձևակերպել այն սահմանները, որոնց շրջանակում պետք է լինի հատկության ընդունելիք արժեքը։ Դա մեզ թույլ կտա խուսափել իրավիճակներից, երբ հատկությանը կարող են վերագրվել սխալ, երբեմն անգամ անհեթեթ արժեքներ։

```js
class Person {
  #name;
  #age;

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  getAge() {
    return this.#age;
  }

  getName() {
    return this.#name;
  }

  setAge(age) {
    if (age > 0 && age < 99) {
      this.#age = age;
    }
  }

  greeting() {
    console.log(`hello ${this.#name}`);
  }
}
```

Մեր դասին ավելացել է _setAge_ մեթոդը, որը հնարավորություն է տալիս փոխել օբյեկտին նախապես տրված _age_ հատկության արժեքը։ Սակայն այդ փոփոխությունն այժմ արվում է կառավարելի կերպով, մենք կարողանում ենք նշել այն թույլատրելի սահմանները, որոնց միջակայքում պետք է լինի այդ հատկության արժեքը, օրինակ մեր պարագայում _person_ օբյեկտի տարիքը կարող է լինել 0֊ից 99֊ը միջակայքում, և այլևս հնարավոր չի լինի ինչ֊որ անհեթեթ արժեքներ վերագրել օբյեկտի _age_ հատկությանը։

```js
console.log(person.getAge()); // 25
person.setAge(150);
console.log(person.getAge()); // 25
```

_age_ հատկության արժեքը չի փոփոխվել, քանի֊որ մեր առաջարկած արժեքը՝ 150֊ը, չի բավարարում _setAge_ մեթոդի մարմնում գրված պայմանին։ Սակայն եթե այժմ մենք տանք 0֊ից 99 միջակայքի ցանկացած այլ թիվ, ապա հատկության արժեքը կփոփոխվի։

```js
console.log(person.getAge()); // 25
person.setAge(42);
console.log(person.getAge()); // 42
```

**JavaScript**-ում կա գեթթերների և սեթթերների հատուկ գրելաձևը, որը թույլ է տալիս օբյեկտների հատկությունները համապատասխանաբար կարդալ կամ փոխել, այսինքն ապահովում է նույն այն գործառույթները, որը մենք մեր օրինակում արեցինք _getAge_ և _setAge_ մեթոդների միջոցով։

Գեթթերներն ու սեթթերներն իրենց հիմքում փաստացի նույնպես ֆունկցիաներ են, սակայն փաթեթավորված են այնպես, որ օբյեկտների վրա օգտագործվում են ասես թե լինեն սովորական հատկություններ։ (_մեթոդների նման չեն կանչվում_)։ Ապագայում նրանց անդրադարձ անպայման կլինի, քանի֊որ դասերի, օբյեկտների հետ աշխատելու բավականին հարմար գործիքներ են։

Նշենք նաև, որ բացի հատկություններից, կարող են մասնավոր, «փակ» լինել նաև դասերի մեջ հայտարարված մեթոդները, և դրա համար ընդամենը պետք է մեթոդի անվանումից առաջ դնել **#** նշանը։ Սակայն նմանատիպ մեթոդներն՝ ի տարբերություն հատկությունների, ավելի հազվադեպ են կիրառվում։

Նյութի մասին ավելի մանրամասն կարելի ծանոթանալ այստեղ՝

- [Private Methods and Fields in JavaScript](https://github.com/tc39/proposal-private-methods)
- [Class Fields in JavaScript](https://github.com/tc39/proposal-class-fields)
