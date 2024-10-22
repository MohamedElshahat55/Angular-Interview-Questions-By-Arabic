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
  الـ Observable في RxJS هو طريقة لتبادل البيانات بين اللي بينتجها (الـ producer) واللي بيستخدمها (الـ consumer). تخيل إن فيه حد بيبعث لك بيانات، بس مش هتبعت لك غير لما تطلبها (ده نظام الـ pull)، أو ممكن البيانات تتبعت لك من غير ما تطلبها (ده نظام الـ push).

في الـ JavaScript العادي، أنت اللي بتطلب البيانات (ده زي الـ pull). لكن في الـ RxJS Observable، البيانات بتتبعت لك تلقائيًا أول ما تعمل subscribe للـ Observable (ده نظام الـ push).

في Angular، الـ Observable بتبدأ تشتغل لما تعملها subscribe، وبتقدر تعمل كده إما باستخدام subscribe مباشرةً أو باستخدام async pipe.

</div>

## What are RxJS operators?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
ببساطة RxJS operators هما functions بتساعدك في التعامل مع Observables وبتنقسم لنوعين:

### Pipeable Operators - 1

دي اللي بتشتغل مع Observable.pipe() وبتاخد observable كـ input وتطلع observable جديد. أمثلة عليها: map، switchMap، mergeMap، concatMap، takeUntil، retry، catchError، و throwError.

### Creation Operators - 2

دي اللي بنستخدمها كـ functions مستقلة عشان ننشئ observables. أمثلة عليها: of، from، interval، fromEvent، generate، و range.

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

## Explain RxJS switchMap operator?

[⬆️ Back to Top](#top)

![ switchMap ](https://rxjs.dev/assets/images/marble-diagrams/switchMap.png)

<div dir="auto" align="right">
الـ switchMap() بيحول observable لواحد تاني، وفي نفس الوقت بيكنسل الاشتراك اللي كان قبل كده. ده معناه إنه لو طلع observable جديد، الاشتراك القديم بيتلغي تلقائيًا. الميزة هنا إن الـ switchMap() بيحميك من تسريب الذاكرة وبيضمن إن آخر observable بس هو اللي شغال ومشترك فيه.

بس علشان كده، الـ switchMap() مش مناسب في السيناريوهات اللي محتاج فيها إن كل الاشتراكات تخلص للآخر، زي لما بتستخدمه مع طلبات HTTP اللي بتكتب في قاعدة البيانات زي (POST، PUT، PATCH، DELETE). في الحالات دي الأفضل إنك تستخدم mergeMap()، لأنه بيسمح لكل الاشتراكات تكمل بدون ما يوقف أي واحدة منهم.

### Some typical use cases for the switchMap() operator are

##### 1- Fetching Details from an API on a Routed Detail Screen

##### 2- Typeahead Search

## Detail screen with switchMap

```typescript
@Component({
  selector: "my-car-brand-detail",
  standalone: true,
  imports: [CommonModule],
  providers: [CarBrandService],
  template: `
    Details:
    <ng-container *ngIf="carBrand$ | async as brand">
      <p>Brand ID:</p>
      <p>Brand Name:</p>
    </ng-container>
  `,
})
export class CarBrandDetailComponent {
  private readonly carBrandService = inject(CarBrandService);
  private readonly activatedRoute = inject(ActivatedRoute);

  // Listen for changes on the Router Params and map the params to an ID value
  private readonly id$ = this.activatedRoute.params.pipe(
    map((params) => params["id"])
  );

  // Every time the id$ changes, the carBand will be fetched
  public readonly carBrand$: Observable<CarBrand> = this.id$.pipe(
    switchMap(
      // SwitchMap returns an observable, in this case an Observable<CarBrand>
      (id) => this.carBrandService.getById(id)
    )
  );
}
```

## Typeahead with switchMap() and ReactiveForms

```typescript
@Component({
  selector: "my-app",
  standalone: true,
  imports: [CommonModule, FormsModule, ReactiveFormsModule],
  providers: [CarService],
  template: `
    <input [formControl]="searchTermControl" type="text" />
    <ul>
      <li *ngFor="let brand of filteredCarBrands$ | async"></li>
    </ul>
  `,
})
export class AppComponent {
  private readonly carBrandService = inject(CarService);

  public readonly searchTermControl = new FormControl("");

  public readonly filteredCarBrands$: Observable<string[]> =
    // Every time the value changes of the fornControl this stream will be executed again
    this.searchTermControl.valueChanges.pipe(
      debounceTime(300), // Wait 300ms before searching
      switchMap((searchTerm) =>
        // Returns a list of Car Brands
        this.carBrandService.searchCarBrands(searchTerm)
      )
    );
}
```

## Typeahead search with switchMap() and BehaviorSubject

```typescript
@Component({
  selector: "my-app",
  standalone: true,
  imports: [CommonModule, FormsModule],
  providers: [CarService],
  template: `
    <input
      [ngModel]="searchTerm$$.value"
      (ngModelChange)="searchTerm$$.next($event)"
      type="text"
    />
    <ul>
      <li *ngFor="let brand of filteredCarBrands$ | async"></li>
    </ul>
  `,
})
export class AppComponent {
  private readonly carBrandService = inject(CarService);

  public readonly searchTerm$$ = new BehaviorSubject("");
  private readonly searchTerm$ = this.searchTerm$$.asObservable();

  // Every time the searchTerm is changed then the carBrandService.searchCarBrands function is called
  public readonly filteredCarBrands$: Observable<string[]> =
    this.searchTerm$.pipe(
      debounceTime(300), // Wait 300ms before searching
      switchMap((searchTerm) =>
        // Returns a list of Car Brands
        this.carBrandService.searchCarBrands(searchTerm)
      )
    );
}
```

</div>

## Explain RxJS mergeMap operator?

[⬆️ Back to Top](#top)

![ mergeMap ](https://rxjs.dev/assets/images/marble-diagrams/mergeMap.png)

<div dir="auto" align="right">
الـ mergeMap في RxJS هو operator بيستخدم في التعامل مع الـ observables، واللي بيعمله إنه بياخد كل element جاية من الـ observable الأولانية وبيعملها subscribe في observable تانية. يعني لو عندك observable بيطلع بيانات، لكل قيمة جاية ممكن تستدعي observable تانية، والـ mergeMap هيعمل merge لكل الـ observables اللي جوا بعض.

فايدته الأساسية إنه بيشتغل بشكل متوازي، يعني لو عندك مثلاً HTTP requests وكل واحدة محتاجة تطلع observable تانية عشان تعمل حاجة زي جلب بيانات، الـ mergeMap هيشغل كل الطلبات دي مع بعض من غير ما يستنى واحدة تخلص عشان يبدأ التانية.

### التعامل مع Multi HTTP requests

مثال على تنفيذ طلبات HTTP متعددة بشكل متوازي باستخدام mergeMap

```typescript
import { fromEvent } from "rxjs";
import { mergeMap } from "rxjs/operators";
import { ajax } from "rxjs/ajax";

const button = document.getElementById("myButton");

fromEvent(button, "click")
  .pipe(mergeMap(() => ajax.getJSON("https://api.example.com/buttonData")))
  .subscribe((response) => {
    console.log("Button click data:", response);
  });
```

### ملحوظة

استخدم الmergeMap لو عند requests زي الPOST , DELETE الي لازم تكتمل بدون الغاء

</div>

## Explain RxJS concatMap operator?

[⬆️ Back to Top](#top)

![ concatMap ](https://rxjs.dev/assets/images/marble-diagrams/concatMap.png)

<div dir="auto" align="right">
الـ concatMap في RxJS بيشتغل بطريقة مشابهة شوية لـ mergeMap، لكن الفرق الرئيسي بينهم هو في طريقة التعامل مع الـ observables اللي طالعة.

الـ concatMap بياخد كل قيمة جاية من الـ observable الأساسي وبيطلع منها observable جديد، بس هنا الـ observables اللي بيطلعها بتشتغل واحدة واحدة بالتتابع. يعني مش هيبدأ الـ observable التاني غير لما الأولاني يخلص. بمعنى آخر، هو بيعمل flattening للـ observables بس بشكل متسلسل بدل ما يكون كله شغال بالتوازي زي ما بيحصل في mergeMap.

```typescript
of("Mohit", "Nilesh")
  .pipe(
    concatMap((se) =>
      of("Shree").pipe(
        delay(2000),
        map((e) => e + " " + se)
      )
    )
  )
  .subscribe((res) => console.log(res));
```

```typescript
 // the output.
(after 2 seconds)
Shree Mohit
(after 2 seconds)
Shree Nilesh
```

</div>

## Explain RxJS exhaustMap operator?

[⬆️ Back to Top](#top)

![ exhaustMap ](https://rxjs.dev/assets/images/marble-diagrams/exhaustMap.png)

<div dir="auto" align="right">
ببساطة كده، exhaustMap بيشتغل بطريقة إنه مش بيهتم غير بالـobservable اللي شغال حاليًا. يعني لو حاجة جديدة جات (زي حدث أو كليك مثلاً) وهو لسه مشغول بحاجة تانية، مش هيبدأ الحاجة الجديدة غير لما يخلص اللي في إيده.

خلينا نقول إن عندك زرار في تطبيق بيفتح حاجة معينة، لو المستخدم ضغط بسرعة على الزرار أكتر من مرة، exhaustMap هيهتم بالضغطة الأولى بس، وهيتجاهل الباقي لحد ما الحاجة اللي بدأها أول مرة تخلص، وبعد كده يبدأ يستقبل حاجات جديدة.

ليه ده مفيد؟
لأنه بيساعد إنك تمنع طلبات كتير تشتغل في نفس الوقت، زي لما تضغط على زر تسجيل الدخول أكتر من مرة، ومش عايز تبعت بياناتك للسيرفر كل مرة غير لما الطلب الأولاني يخلص.

```typescript
import { fromEvent } from "rxjs";
import { exhaustMap, interval, take } from "rxjs/operators";

const button = document.getElementById("myButton");
const clicks$ = fromEvent(button, "click");

clicks$
  .pipe(
    exhaustMap(() => {
      return interval(1000).pipe(take(3));
    })
  )
  .subscribe((val) => console.log(val));
```

هنا:

fromEvent بيتابع الكليكات اللي بتحصل على الزرار.
exhaustMap بيتأكد إن مفيش كليك جديد هيتم معالجته غير لما الطلب الحالي يخلص.
interval هنا مجرد مثال لعملية بتاخد شوية وقت (ممكن تعتبره طلب HTTP مثلاً).
كل ضغطة هتستنى لحد ما الكليك الأولاني يخلص قبل ما تقبل كليك جديد.

</div>

## How will you handle errors on observable using RxJS throwError?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في RxJS، لو حصل خطأ أثناء تشغيل الـobservable، ممكن نستخدم throwError عشان نبعت الخطأ ده في الـstream ونتعامل معاه باستخدام الـcatchError أو الـretry operators.

```typescript
import { of, throwError } from "rxjs";
import { catchError } from "rxjs/operators";

const myObservable = of("Data 1", "Data 2", "Data 3").pipe(
  throwError("Error occurred!"),
  catchError((error) => {
    return of("Default value");
  })
);

myObservable.subscribe(
  (data) => console.log("Data:", data),
  (error) => console.log("Error:", error),
  () => console.log("Complete")
);
```

throwError: لما يحصل خطأ، الـobservable هيعمل emit للخطأ ده.
catchError: بنستخدمه عشان نعمل handle للخطأ. في المثال ده، لو حصل خطأ، بنرجع observable تاني بقيمة بديلة (of('Default value')).
الـsubscribe: لو مفيش أخطاء، الـobserver هياخد الـdata اللي الـobservable بيعملها emit. ولو حصل خطأ هيتم الإمساك بيه في الـcatchError قبل ما يوصل للـsubscribe.

</div>

## Explain RxJS retry operator?

[⬆️ Back to Top](#top)

![ retry ](https://rxjs.dev/assets/images/marble-diagrams/retry.png)

<div dir="auto" align="right">
في RxJS، الـretry هو operator بيُستخدم لما يحصل خطأ في الـobservable، ويسمح بإعادة محاولة تشغيل الـobservable تلقائيًا لعدد معين من المرات قبل ما يدي خطأ نهائي. الفكرة إنه لو عندك عملية ممكن تفشل (زي طلب HTTP)، الـretry بيساعد في إعادة المحاولة كذا مرة على أمل إن المشكلة تتحل، زي مشكلة مؤقتة في الشبكة.

### ازاي تستخدم retry

الـretry بياخد عدد من المرات اللي عايز تكرر فيها المحاولة لما يحصل خطأ. لو عدد المحاولات خلص ولسه فيه خطأ، الـobservable هيرجع خطأ عادي.

```typescript
import { of, throwError } from "rxjs";
import { retry, catchError } from "rxjs/operators";

const myObservable = throwError("Error occurred!").pipe(
  retry(2),
  catchError((error) => {
    console.log("Failed after retries:", error);
    return of("Fallback value");
  })
);

myObservable.subscribe(
  (data) => console.log("Data:", data),
  (error) => console.log("Error:", error),
  () => console.log("Complete")
);
```

throwError: بنحاكي سيناريو إن الـobservable بيفشل وبيطلع خطأ.
retry(2): هنا بنقول للـobservable إنه يحاول مرتين لو حصل خطأ. يعني بعد أول خطأ، هيحاول مرة كمان، ولو فشل برضه، يحاول للمرة الأخيرة.
catchError: لو المحاولات كلها فشلت، بنمسك الخطأ ونتعامل معاه. في المثال، بنرجع قيمة افتراضية (Fallback value).
الـsubscribe: لو مفيش أخطاء، الـobservable هيعمل emit للـdata عادي، لكن لو كل المحاولات فشلت، هيوصل الخطأ للـcatchError وهنرجع القيمة البديلة.

سيناريوهات للاستخدام:
طلبات HTTP متكررة: ممكن تكون بتعمل طلب لـAPI وفيه مشاكل مؤقتة في الاتصال، زي انقطاع الشبكة. في الحالة دي، بدل ما الطلب يفشل مباشرة، ممكن تحاول كذا مرة باستخدام retry، وتدي فرصة إن المشكلة تتحل.

عمليات غير مستقرة: في عمليات زي الكتابة أو القراءة من قاعدة بيانات أو التعامل مع ملفات، ممكن يحصل فشل بسبب عوامل خارجية (زي مشكلة في التخزين المؤقت). باستخدام retry، تقدر تعيد المحاولة بدون الحاجة لتدخل المستخدم كل مرة.

```typescript
import { ajax } from "rxjs/ajax";
import { catchError, retry } from "rxjs/operators";
import { of } from "rxjs";

// مثال لطلب HTTP
const apiCall$ = ajax.getJSON("https://api.example.com/data").pipe(
  // هنحاول إعادة المحاولة 3 مرات لو فشل
  retry(3),
  catchError((error) => {
    console.log("Request failed after retries:", error);
    return of({ error: "Failed to fetch data", data: [] });
  })
);

apiCall$.subscribe(
  (response) => console.log("API Response:", response),
  (error) => console.log("Error:", error),
  () => console.log("Complete")
);
```

retry(3): بنطلب من RxJS إعادة المحاولة 3 مرات لو حصل فشل في طلب الـAPI.
catchError: لو كل المحاولات فشلت، بنعمل catch للخطأ ونتعامل معاه، مثلاً نرجع بيانات افتراضية بدل ما نوقف التطبيق.
الـretry بيكون مفيد في الحالات اللي بتحصل فيها أخطاء غير متوقعة أو مؤقتة، وبيسمح للتطبيق يكون أكثر مرونة في التعامل مع الأخطاء بدون الحاجة لتدخل المستخدم في كل مرة

</div>

## Explain RxJS filter operator?

[⬆️ Back to Top](#top)

![ filter ](https://rxjs.dev/assets/images/marble-diagrams/filter.png)

<div dir="auto" align="right">
في RxJS، الـfilter هو operator بنستخدمه عشان نعمل "فلترة" للـvalues اللي الـobservable بيعمل لها emit. بمعنى تاني، هو بيشغل callback function على كل قيمة، ولو الشرط اللي في الـcallback اتحقق، بيمرر القيمة دي، ولو لأ، بيتجاهلها.

### ازاي تستخدم filter

الـfilter بياخد كل قيمة جاية من الـobservable ويشوف لو القيمة دي بتوافق الشرط اللي في الـcallback.
لو القيمة مطابقة للشرط، بتكمل في الـobservable stream، ولو لأ، بتتفلتر وتتجاهل.

```typescript
import { from } from "rxjs";
import { filter } from "rxjs/operators";

// observable بيمثل مجموعة من الأرقام
const numbers$ = from([1, 2, 3, 4, 5, 6, 7, 8, 9]);

// بنستخدم filter عشان نخلي بس الأرقام الزوجية تعدي
const evenNumbers$ = numbers$.pipe(
  filter((num) => num % 2 === 0) // هنا الشرط إن الرقم لازم يكون زوجي
);

evenNumbers$.subscribe(
  (value) => console.log("Even number:", value),
  (error) => console.log("Error:", error),
  () => console.log("Complete")
);
```

### الاستخدام

فلترة الأحداث: مثلاً، في حالة استماعك لأحداث معينة (زي ضغطات المستخدم على زر معين)، ممكن تستخدم filter عشان تتعامل بس مع نوع معين من الأحداث (زي لو المستخدم ضغط على زرار معين في الـUI).

طلبات الـHTTP: لو عندك استجابة API وبيجيلك فيها بيانات كتيرة، ممكن تستخدم filter عشان تمرر فقط القيم اللي تحقق شروط معينة (مثلاً، طلبات فيها status معين أو بيانات بنطاق معين).

```typescript
import { fromEvent } from "rxjs";
import { filter } from "rxjs/operators";

const button = document.getElementById("myButton");
const clicks$ = fromEvent(button, "click");

// بنستخدم filter عشان نتعامل بس مع الكليكات اللي بتحصل في الجانب الأيسر من الشاشة
clicks$
  .pipe(filter((event: MouseEvent) => event.clientX < window.innerWidth / 2))
  .subscribe((event) => console.log("Clicked on the left side!", event));
```

fromEvent: بنعمل observable للضغطات على زرار معين.
filter: هنا بنفلتر الأحداث ونتعامل بس مع الضغطات اللي حصلت في النصف الأيسر من الشاشة (على أساس إن قيمة clientX أقل من نصف عرض الشاشة).

</div>
