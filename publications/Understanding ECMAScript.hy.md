# Ի՞նչ է իրենից ներկայացնում ECMAScript-ը և ինչո՞վ է այն տարբերվում JavaScript-ից

[**ECMAScript**](https://www.ecma-international.org/ecma-262)
-ը դա սքրիփթային ծրագրավորման լեզվի ստանդարտ է, և հիմք է հանդիսանում լեզվի տարբեր ռեալիզացիաների համար, որոնցից ամենահայտնի 3 են՝ **JavaScript**, **JScript** և **ActionScript**-ը: Ի դեպ սկզբում ստեղծվել է **JavaScript**-ը, իսկ լեզվի ստանդարտը՝ **ECMAScript**-ը առաջացել է միայն 1997 թվականին, այսինքն լեզվի ստեղծումից երկու տարի հետո միայն։

Հիմա փորձենք հասկանալ թե ինչպես ստացվեց, որ մի լեզվական ստանդարտի վրա առաջացան մի քանի տարբեր անվանումով լեզուներ, որոնք իրականում իրարից շատ չեն տարբերվում թե՛ սինթաքսով և թե՛ սեմանտիկայով։ Բանը նրանում է, որ **Java** և **JavaScript** ապրանքային նշանները գրանցված են _Sun Microsystems_ ընկերության կողմից, որը ներկայումս մտնում է _Oracle_-ի կազմի մեջ։ Սակայն բուն լեզուն որևէ ընկերության կամ կազմակերպության սեփականություն չի հանդիսանում, և օրինակ հենց դրա համար _Microsoft_ կորպորացիան մշակեց լեզվի իր սեփական տարբերակը՝ **JScript**-ը, որը նույն **JavaScript**-ն է, թեև որոշ ոչ այդքան էական տարբերություններ իհարկե կան։

**ECMA international**-ը (_European Computer Manufacturers Association_) հիմնադրվել է 1961 թվականին, և հանդիսանում է կազմակերպություն, որը զբաղվում է կապի և ինֆորմացիոն տեխնոլոգիաների ստանդարտիզացմամբ։
Կազմակերպությունը բաղկացած է գլխավոր ասամբլեայից, քարտուղարությունից, կառավարման ու կոորդինացիայի կոմիտեից և մի շարք տեխնիկական կոմիտեներից, որոնցից ամեն մեկը զբաղվում է որոշակի բնագավառով կամ թեմայով։ **ECMA**-ի կազմում կան 14 կոմիտեներ, և մեզ այս պահին հետաքրքիր է դրանցից միայն մեկը՝ **TC39**-ը։ **TC39**-ը զբաղվում է **ECMAScript**-ի մշակմամբ և **JavaScript**-ի հերթական թարմացված տարբերակի թողարկմամբ։

**TC39**-ի կազմում են դիտարկիչների մշակմամբ և թողարկումով զբաղվող բոլոր խոշոր ընկերությունները (_Google_, _Microsoft_, _Mozilla_, _Apple_, _Opera Software_), ինչպես նաև հրավիրյալ փորձագետներ և մասնագետներ այլ խոշոր IT ընկերություններից և հայտնի գիտահետազոտական կենտրոններից։ Ամեն 2 ամիսը մեկ նրանք հավաքվում են քննարկելու ինչպես պետք է զարգանա **ECMA-262** կամ այպես կոչված **ECMAScript** լեզվական ստանդարտը։

Եվ ուրեմն ինչի՞ համար է նախատեսված լեզվական ստանդարտի նկարագրությունը։ Խնդիրը նրանում է, որ տարբեր բրաուզերներ կամ այլ միջավայրեր օգտագործում են **JavaScript**-ի տարբեր engine-ներ, օրինակ _chrome_, _opera_, _yandex_ բրաուզերների և _node.js_ պլատֆորմի համար դա **V8**-ն է, _firefox_-ի համար **SpiderMonkey**-ին, կա նաև **Trident** և **Chakra** engine-ները _internet explorer_-ի տարբեր վերսիաների համար, **Nitro**-ն և **SquirrelFish**-ը _safari_-ի համար և այլն։

Եվ եթե բոլորը խստորեն հետևեն ստանդարտներին, ապա ակնկալվում է, որ **JavaScript**-ով գրված կոդը բոլոր միջավայրերում կիրականացվի բացարձակորեն միանման կերպով, ինչը կերաշխավորի, որ վեբ հավելվածները կամ **JavaScript**-ով գրված այլ ծրագրերը կոռեկտ կաշխատեն բոլոր միջավայրերում։

Ի դեպ ցանկացած ոք կարող է դիմել **TC39** կոմիտեին, լեզվում նոր հնարավորություններ ավելացնելու առաջարկով։ Եվ իրականում բացի խոշոր կորպորացիաների պրոֆեսիոնալ թիմերից, այլ IT կազմակերպությունների ներկայացուցիչները և անհատ ծրագրավորողները նույնպես մեծ դեր են խաղում լեզվի զարգացման գործում՝ առաջարկելով, մշակելով և ներկայացնելով մի շարք կարևոր նորամուծություններ։ Դիմելուց մինչև հավանության արժանանալ և ստանդարտ ներառվել երկար պրոցես է, որն անցնում է մի քանի տարբեր փուլերով:
