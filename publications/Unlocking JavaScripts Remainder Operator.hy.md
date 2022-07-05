# Մնացորդով բաժանման օպերատորը JavaScript-ում (%): Ինչպե՞ս օգտվելով մնացորդով բաժանումից արտածել տրված թիվը հակառակ հերթականությամբ(«Շրջել» այն):

Հիմնական թվաբանական գործողություններին՝ գումարում, հանում, բաժանում և բազմապատկում՝ բոլորն են ծանոթ։ Բայց կա ևս մի հասարակ թվաբանական գործողություն՝ ՄՆԱՑՈՐԴՈՎ ԲԱԺԱՆՈՒՄԸ, որը սկսնակները երբեմն չեն պատկերացնում թե հատկապես որտեղ կարելի է կիրառել։ Այն ծրագրավորման մեջ հաճախ է օգտագործվում, և այս գրառման մեջ մենք կծանոթանանք նրա օգտագործման մի քանի տարբերակների, իսկ վերջում շատ տարածված մի խնդիր կլուծենք, որի իմաստը կայանում է նրանում, որ առանց բարձր կարգի ֆունկցիաներ օգտագործելու, տրված թիվը արտածել հակառակ հերթականությամբ։

Տարբեր ծրագրավորման լեզուներում մնացորդով բաժանման օպերատորը տարբեր տեսք ունի։ Օրինակ **Delphi**, **Haskell**, **MATLAB**, **Pascal** և մի շարք այլ լեզուներում օգտագործվում է _mod_ բանալի բառը, **C/C++**, **JavaScript** և մի շարք այլ՝ **C** լեզվին սինթաքսով նման լեզուներում որպես օպերատոր օգտագործվում է **%** սիմվոլը (Նկատենք, որ այն տոկոս հաշվելու հետ կապ չունի)։

Այսպիսով **a % b** -ն կվերադարձնի _a_-ն _b_-ի վրա բաժանելու արդյունքում ստացված մնացորդը։ **JavaScript**-ում մնացորդով բաժանման արդյունքում վերադարձվող արժեքը միշտ ստանում է **ԲԱԺԱՆԵԼԻԻ նշանը** (_Դրական կամ Բացասական_):

```js
console.log(7 % 3); // 1
console.log(8 % 2); // 0
console.log(-1 % 2); // -1
console.log(1 % 2); // 1
console.log(-4 % 2); // -0
console.log(5.5 % 2); // 1.5
```

Երբ և՛ բաժանելին և՛ բաժանարարը դրական թվեր են և բաժանարարը մեծ է բաժանելիից, այդտեղ ամեն ինչ ավելի քան հասկանալի է։ Սակայն ինչու՞ է 1 % 2-ը ստացվում 1։ Որովհետև 1 -ի մեջ 2-ը տեղավորվում է 0 անգամ, 0 \* 2 = 0, հետևաբար մնում է 1 մնացորդը: (Հետաքրքիր տրամաբանություն է, ինչ խոսք):

Նաև -4 % 2 = -0, ինչը ևս տարօրինակ է, սակայն հիշեցնեմ, որ **JavaScript**-ում, և ոչ միայն **JavaScript**-ում, նաև մի շարք այլ ծրագրավորման լեզուներում գոյություն ունի -0 թվային արժեք (մաթեմատիկոսների մոտ հանկարծ այդպիսի բան չասեք), որը կապված է թվերի՝ հիշողության մեջ ներկայացման **IEEE-754** ձևաչափի օգտագործման հետ (_երբեմն անվանում են նաև double precision ձևաչափ կամ ուղղակի double_)։

Մնացորդով բաժանումը կարող ենք օգտագործել պարզելու համար թիվը զույգ է թե կենտ։ Երբ ամբողջ թիվը մնացորդով բաժանում ենք 2-ի, ապա եթե ստացվում է 0 մնացորդ, նշանակում է թիվը զույգ է, քանի-որ միայն զույգ թիվը կարող է առանց մնացորդ բաժանվել 2-ի վրա։ Հակառակ դեպքում բնականաբար թիվը կենտ է։

Նկատենք նաև, որ բազմանիշ ամբողջ թիվը մնացորդով 10-ի վրա բաժանելու արդյունքում ստանում ենք վերջին թվանշանը։ Օրինակ՝

- 458 % 10 կստանանք 8, որովհետև 458-ի մեջ 10-ը տեղավորվում է 45 անգամ, և մնում է 8 մնացորդը։ 458 === 45 \* 10 + 8
- 35 % 10-ի դեպքում կստանանք 5, որովհետև 35-ի մեջ 10-ը տեղավորվում է 3 անգամ և մնում է 5 մնացորդը։ 35 === 3 \* 10 +5

Միանիշ թվի դեպքում նույնպես ամեն ինչ արդեն պարզ է, 10-ի վրա մնացորդով բաժանելուց ստացվում է հենց այդ թիվը։ Օրինակ՝

- 8 % 10 ստացվում է 8, քանի որ 8-ի մեջ 10-ը տեղավորվում է 0 անգամ, և մնում է 8 մնացորդը։

Իսկ հիմա փորձենք մնացորդով բաժանման օգնությամբ լուծել մի շատ տարածված խնդիր։ Ստեղծենք ծրագիր, որը թույլ կտա ներմուծել թիվ, և այդ թվերը արտածենք հակառակ հերթականությամբ։ Մենք իհարկե կարող ենք օգտագործել ներդրված ֆունկցիաների մի քանի շղթայական կանչ, և խնդիրը լուծել շատ հեշտ ու շատ արագ։

```js
alert(prompt("Input a number").split("").reverse().join(""));
```

Այստեղ ուղղակի _promp_-ով կատարում ենք հարցում, ստանում թիվը, և քանի որ _prompt_-ը մուտքագրված արժեքները վերադարձնում է տողի տեսքով, այն միանգամից վերածում ենք զանգվածի _split_ մեթոդի օգնությամբ, _reverse_-ով շուռ տալիս, հետո _join_-ով կրկին վերածում տողի։ Ապա _alert_ ենք անում արժեքը։

Բայց բերեք _String_-ի և _Array_-ի մեթոդներ չօգտագործենք ու փորձենք խնդիրը լուծել մնացորդով բաժանման օպերատորի և _while_ ցիկլի օգնությամբ։

```js
function reverseNum(num) {
  let result = 0;
  while (num) {
    result = result * 10 + (num % 10);
    num = Math.floor(num / 10);
  }
  return result;
}
```

ֆունկցիան որպես արգումենտ ստանում է թիվ, այնուհետև ֆունկցիայի մարմնում հայտարարվում է _result_ փոփոխականը, և որպես սկզբնական արժեք տրվում է 0-ն։ Հաջորդ քայլին _while_ ցիկլը որպես պայման ստանում է _num_ արգումենտը և ինչպես գիտենք ցիկլի պայմանում ցանկացած տիպի արգումենտ ավտոմատ փոխակերպվում է բուլյան արժեքի։ 0-ից և _NaN_-ից բացի, բոլոր մյուս թվային արժեքները փոխակերպվում են _true_-ի։ Ցիկլը կաշխատի այնքան ժամանակ, քանի դեռ num-ի արժեքը չի դարձել 0, որը _falsy_- ի արժեք է, և կստիպի ցիկլին դադարեցնել աշխատանքը։

Որպեսզի թիվը հակառակ հերթականությամբ «հետ հավաքենք» մենք պետք է _result_ փոփոխականի արժեքը ցիկլի յուրաքանչյուր իտերացիայի ժամանակ բազմապատկենք 10-ով և գումարենք դրան մուտքագրված թվի վերջին թվանշանը, որն էլ կստանանք թիվը 10-ի վրա մնացորդով բաժանելու շնորհիվ։ Նաև անհրաժեշտ կլինի մուտքագրված թիվն ամեն իտերացիայի ժամանակ փոքրացնել, դեն նետելով վերջին թվանշանը, այլապես կունենանք անվերջ ցիկլ։ Դրա համար մենք թիվը կբաժանենք 10-ի, և _parsInt_ կամ _Math.floor_ ֆունկցիաների օգնությամբ դեն կնետենք մնացորդը։

Եթե կհետաքրքրի, [նախորդ գրառումներիցս մեկում](./JavaScripts%20Numeric%20Nitty-Gritty.hy.md), որը նվիրված էր ոչ ամբողջ թվերից ամբողջ մասի ստացմանը, ես նշել եմ մի քանի տարբերակներ, թե ինչպես կարելի է դա անել, այդ թվում նաև էկզոտիկ տարբերակներով՝ օրինակ `~` (tilde կամ հայերեն ալիքանշան) օպերատորի օգտագործմամբ: Եվ այսպես՝ ամեն իտերացիայի ընթացքում մուտքագրված թիվը զրկվում է իր վերջին թվանշանից, մինչև դառնում է միանիշ, որն էլ 10-ի վրա բաժանվելով և դեպի ներքև կլորացվելով դառնում է 0։ Ցիկլը դադարեցնում է իր աշխատանքը, ֆունկցիան վերադարձնում է _result_ փոփոխականը, որում արդեն հակառակ հերթականությամբ հավաքված թիվն է։

Մենք կարող ենք փոքրիկ լրացում կատարել, որպեսզի _prompt_ - ի շնորհիվ հնարավոր լինի մուտքագրել թիվը, և _alert_ արվի թիվը՝ բայց հակառակ հերթականությամբ։

```js
alert(reverseNum(prompt("Enter a value"), ""));
```

Ֆունկցիան կարող է ունենալ նաև հետևյալ տեսքը՝

```js
function reverseNum(n) {
  let x = 0;
  while (n > 0) {
    x = x * 10 + (n % 10);
    n = ~~(n / 10);
  }
  return x;
}
```

Ամեն ինչ այնպես է ինչպես վերևի օրինակում, ուղղակի մնացորդից ազատվելու համար օգտագործում ենք ~ օպերատորը, ինչպես արդեն ասեցի, դրա մասին առանձին գրառում կա [հետևյալ հղումով](./JavaScripts%20Numeric%20Nitty-Gritty.hy.md)

Իսկ վերջում որպես բոնուս ներկայացնեմ շատ խառն ու անհասկանալի տարբերակ, որը թեև շատ հրաշալի աշխատում է, սակայն օգտագործել խորհուրդ չի տրվում &#128522;

```js
const reverseNum = (n, res = "", _) => (
  (_ = (n) => (n < 1 ? null : ((res += ~~(n % 10)), _(n / 10))))(n), +res
);
```