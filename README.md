<a name="top"></a>

# Angular RxJS Interview Questions

| No. | Questions                                                                                                                          |
| --- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [Explain RxJS Observable?](#explain-rxjs-observable)                                                                               |
| 2   | [What are RxJS operators?](#what-are-rxjs-operators)                                                                               |
| 3   | [What is Observable.pipe() and how to use it?](#what-is-observablepipe-and-how-to-use-it)                                          |
| 4   | [What is the difference between RxJS of and from?](#what-is-the-difference-between-rxjs-of-and-from)                               |
| 5   | [Explain RxJS map operator?](#explain-rxjs-map-operator)                                                                           |
| 6   | [Explain RxJS switchMap operator?](#explain-rxjs-switchmap-operator)                                                               |
| 7   | [Explain RxJS mergeMap operator?](#explain-rxjs-mergemap-operator)                                                                 |
| 8   | [Explain RxJS concatMap operator?](#explain-rxjs-concatmap-operator)                                                               |
| 9   | [Explain RxJS exhaustMap operator?](#explain-rxjs-exhaustmap-operator)                                                             |
| 10  | [How will you handle errors on observable using RxJS throwError?](#how-will-you-handle-errors-on-observable-using-rxjs-throwerror) |
| 11  | [How will you handle errors on observable using RxJS catchError?](#how-will-you-handle-errors-on-observable-using-rxjs-catcherror) |
| 12  | [Explain RxJS retry operator?](#explain-rxjs-retry-operator)                                                                       |
| 13  | [Explain RxJS filter operator?](#explain-rxjs-filter-operator)                                                                     |
| 14  | [Explain RxJS tap operator?](#explain-rxjs-tap-operator)                                                                           |
| 15  | [Explain RxJS takeUntil operator?](#explain-rxjs-takeuntil-operator)                                                               |
| 16  | [Explain RxJS takeWhile operator?](#explain-rxjs-takewhile-operator)                                                               |
| 17  | [Explain RxJS takeLast operator?](#explain-rxjs-takelast-operator)                                                                 |
| 18  | [Explain RxJS take operator?](#explain-rxjs-take-operator)                                                                         |
| 19  | [Explain RxJS debounce operator?](#explain-rxjs-debounce-operator)                                                                 |
| 20  | [Explain RxJS debounceTime operator?](#explain-rxjs-debouncetime-operator)                                                         |
| 21  | [Explain RxJS combineLatestWith operator?](#explain-rxjs-combinelatestwith-operator)                                               |
| 22  | [Explain RxJS fromEvent operator?](#explain-rxjs-fromevent-operator)                                                               |

## Explain RxJS Observable

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الإجابة المبسطة: الـ Observable في RxJS هو طريقة لتبادل البيانات بين اللي بينتجها (الـ producer) واللي بيستخدمها (الـ consumer). تخيل إن فيه حد بيبعث لك بيانات، بس مش هتبعت لك غير لما تطلبها (ده نظام الـ pull)، أو ممكن البيانات تتبعت لك من غير ما تطلبها (ده نظام الـ push).

في الـ JavaScript العادي، أنت اللي بتطلب البيانات (ده زي الـ pull). لكن في الـ RxJS Observable، البيانات بتتبعت لك تلقائيًا أول ما تعمل subscribe للـ Observable (ده نظام الـ push).

في Angular، الـ Observable بتبدأ تشتغل لما تعملها subscribe، وبتقدر تعمل كده إما باستخدام subscribe مباشرةً أو باستخدام async pipe.

</div>

## What are RxJS operators?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
RxJS operators ببساطة هما  (functions) بتساعدك في التعامل مع **Observables** بطريقة مرنة وسهلة، وبتنقسم لنوعين:

### **Pipeable Operators**

دي العمليات اللي بتشتغل مع `Observable.pipe()`. زي مثلاً:

**map**: بتاخد **observable** وتعدل على الداتا اللي فيه.
**switchMap**: بتبدل بين **observables** بطريقة ذكية لما فيه طلبات جديدة.**mergeMap** و**concatMap**: لدمج أو تسلسل **observables**.
**takeUntil**: بتوقف **observable** لما يحصل حاجة معينة.
**retry** و**catchError** و**throwError**: للتعامل مع الأخطاء وإعادة المحاولة لو في مشكلة.

دي كل العمليات اللي ممكن تستخدمها في `pipe()`، يعني بتاخد **observable** وتعمل عليه شغل وتطلعلك **observable** جديد.

pipeable operators\*\*:

```typescript
import { map, switchMap, debounceTime, catchError } from "rxjs/operators";
```

### 2. **Creation Operators**:

دي العمليات اللي بتقدر تستخدمها كدوال مستقلة لإنشاء **observables**. زي مثلاً:

**of**: لإنشاء **observable** من قيمة أو مجموعة قيم.
**from**: بيعمل **observable** من **array** أو **promise**.
**interval**: بينشئ **observable** بيرجع أرقام على فترات زمنية محددة.
**fromEvent**: لإنشاء **observable** من الأحداث اللي بتحصل على DOM زي الـ `click`.

\*creation operators\*\*:

```typescript
import { of, from, interval, fromEvent } from "rxjs";
```

</div>

## What is Observable.pipe() and how to use it?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ pipe في RxJS هو اللي بنستخدمه عشان نمرر مجموعة من الـ pipeable operators، اللي بنقدر نستخدمها مع observables. يعني ببساطة، تقدر تحط أي عدد من العمليات (operators) جوه الـ pipe، وهيشتغلوا بالتسلسل. الفكرة إن الـ observable الأساسي بيتبعت لأول operator، والنتيجة بتاعت أول واحد بتتبعت للتاني، وهكذا.

```typescript
of(101, 102)
  .pipe(
    delay(1000),
    map((num) => num * 2)
  )
  .subscribe((v) => console.log(v)); // 202, 204
```

في المثال ده، أول حاجة بنستخدم delay(1000) علشان نأخر التنفيذ ثانية (1000 ميلي ثانية).
بعد كده، بنستخدم map اللي بيضرب كل رقم في 2.
النتيجة هتكون: 202، 204 (يعني الأرقام اتضربت في 2 بعد التأخير).

الخلاصة:
الـ pipe بيسهل عليك تنفيذ عمليات متتابعة على البيانات اللي جاية من observable، وده بيديك تحكم أكبر في تعديل الداتا أو توقيتها أو التعامل مع الأخطاء.

</div>

## What is the difference between RxJS of and from?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الفرق بين RxJS of و RxJS from ببساطة هو في نوع المدخلات اللي كل واحد فيهم بيتعامل معاها وطريقة تحويلهم لـ Observable

### of - 1

بتاخد مجموعة من القيم (زي "a" و "b" و "c") وتحولهم لـ observable sequence، يعني كل قيمة بتطلع لوحدها.

```typescript
of("a", "b", "c").subscribe((e) => console.log(e));
```

في الحالة دي، كل حرف هيظهر في السطر على حدة.

### from - 2

بتاخد array أو حاجة شبهه (زي promise) وتحوّله لـ observable، يعني كل عنصر جوه الـ array بيتعامل معاه كجزء من الـ observable.

```typescript
from(["a", "b", "c"]).subscribe((e) => console.log(e));
```

هنا، نفس القيم اللي كانت في الـ array (يعني "a", "b", "c") هتتعامل معاها كأن كل عنصر بيتطلع لوحده في الـ observable.

</div>

## Explain RxJS map operator?

[⬆️ Back to Top](#top)

![ map ](https://rxjs.dev/assets/images/marble-diagrams/map.png)

<div dir="auto" align="right">
الـ map operator في RxJS ببساطة بيطبق function معينة على كل عنصر بيتم إصداره من الـ Observable. يعني كل عنصر بيعدي من المصدر، بيتم تطبيق الـ function عليه والنتيجة هي اللي بتطلع.

```typescript
of(1, 2, 3, 4)
  .pipe(map((e) => e * e))
  .subscribe((output) => console.log(output));
```

في المثال ده:

عندنا observable بيرسل القيم (1, 2, 3, 4).
كل قيمة من القيم دي بتدخل في map، اللي بتضرب القيمة في نفسها (يعني بتربع القيمة).
بعد كده الـ observable الجديد اللي طالع بيرجع القيم: 1, 4, 9, 16.
يعني لما بنعمل subscribe على الـ observable الناتج، بنشوف القيم الجديدة اللي هي 1، 4، 9، و 16 في الـ console.

بكده تقدر تستخدم map علشان تعدل أو تعمل عمليات على البيانات اللي بتيجي من الـ observable الأصلي بطريقة بسيطة.

</div>
