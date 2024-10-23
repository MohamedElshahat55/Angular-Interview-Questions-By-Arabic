<a name="top"></a>

# Angular RxJS Interview Questions

> connect with me on [LinkedIn](https://www.linkedin.com/in/mohamed-elshahat-4017a1303) for more technical updates and content.

### Table of Contents

| No. | Questions                                                                                                                                                                                                                                                                                                        |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [Explain RxJS Observable?](#explain-rxjs-observable)                                                                                                                                                                                                                                                             |
| 2   | [What are RxJS operators?](#what-are-rxjs-operators)                                                                                                                                                                                                                                                             |
| 3   | [What is Observable.pipe() and how to use it?](#what-is-observablepipe-and-how-to-use-it)                                                                                                                                                                                                                        |
| 4   | [What is the difference between RxJS of and from?](#what-is-the-difference-between-rxjs-of-and-from)                                                                                                                                                                                                             |
| 5   | [Explain RxJS map operator?](#explain-rxjs-map-operator)                                                                                                                                                                                                                                                         |
| 6   | [Explain RxJS switchMap operator?](#explain-rxjs-switchmap-operator)                                                                                                                                                                                                                                             |
| 7   | [Explain RxJS mergeMap operator?](#explain-rxjs-mergemap-operator)                                                                                                                                                                                                                                               |
| 8   | [Explain RxJS concatMap operator?](#explain-rxjs-concatmap-operator)                                                                                                                                                                                                                                             |
| 9   | [Explain RxJS exhaustMap operator?](#explain-rxjs-exhaustmap-operator)                                                                                                                                                                                                                                           |
| 10  | [How will you handle errors on observable using RxJS throwError?](#how-will-you-handle-errors-on-observable-using-rxjs-throwerror)                                                                                                                                                                               |
| 11  | [How will you handle errors on observable using RxJS catchError?](#how-will-you-handle-errors-on-observable-using-rxjs-catcherror)                                                                                                                                                                               |
| 12  | [Explain RxJS retry operator?](#explain-rxjs-retry-operator)                                                                                                                                                                                                                                                     |
| 13  | [Explain RxJS filter operator?](#explain-rxjs-filter-operator)                                                                                                                                                                                                                                                   |
| 14  | [Explain RxJS tap operator?](#explain-rxjs-tap-operator)                                                                                                                                                                                                                                                         |
| 15  | [Explain RxJS takeUntil operator?](#explain-rxjs-takeuntil-operator)                                                                                                                                                                                                                                             |
| 16  | [Explain RxJS debounceTime operator?](#explain-rxjs-debouncetime-operator)                                                                                                                                                                                                                                       |
| 17  | [Explain RxJS combineLatestWith operator?](#explain-rxjs-combinelatestwith-operator)                                                                                                                                                                                                                             |
| 18  | [Explain RxJS fromEvent operator?](#explain-rxjs-fromevent-operator)                                                                                                                                                                                                                                             |
| 19  | [What is the difference between Subject, BehaviorSubject, ReplaySubject, and AsyncSubject in RxJS? How do they differ in terms of behavior and use cases?](#what-is-the-difference-between-subject-behaviorsubject-replaysubject-and-asyncsubject-in-rxjs-how-do-they-differ-in-terms-of-behavior-and-use-cases) |
| 20  | [What are the best practices for managing Observable subscriptions in Angular and ensuring there are no memory leaks?](#what-are-the-best-practices-for-managing-observable-subscriptions-in-angular-and-ensuring-there-are-no-memory-leaks)                                                                     |
| 21  | [What are the differences between cold observable and hot observable?](#what-are-the-differences-between-cold-observable-and-hot-observable)                                                                                                                                                                     |
| 22  | [What are the differences between Observables and Promises?](#what-are-the-differences-between-observables-and-promises)                                                                                                                                                                                         |
| 23  | [What is a higher-order Observable?](#what-is-a-higher-order-observable)                                                                                                                                                                                                                                         |
| 24  | [How can you share a single Observable among multiple subscribers?](#how-can-you-share-a-single-observable-among-multiple-subscribers)                                                                                                                                                                           |

# Angular Form Interview Questions

### Table of Contents

| No. | Questions                                                                                                                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [Describe the types of forms created in Angular application?](#describe-the-types-of-forms-created-in-angular-application)       |
| 2   | [How will you create reactive form in Angular?](#how-will-you-create-reactive-form-in-angular)                                   |
| 3   | [How will you create template-driven form in Angular?](#how-will-you-create-template-driven-form-in-angular)                     |
| 4   | [Explain FormControl?](#explain-formcontrol)                                                                                     |
| 5   | [Explain FormGroup?](#explain-formgroup)                                                                                         |
| 6   | [Explain FormArray?](#explain-formarray)                                                                                         |
| 7   | [Explain FormBuilder?](#explain-formbuilder)                                                                                     |
| 8   | [Explain FormRecord?](#explain-formrecord)                                                                                       |
| 9   | [How will you use valueChanges?](#how-will-you-use-valuechanges)                                                                 |
| 10  | [How will you use statusChanges?](#how-will-you-use-statuschanges)                                                               |
| 11  | [What is difference between setValue() and patchValue()?](#what-is-difference-between-setvalue-and-patchvalue)                   |
| 12  | [How will you add and remove controls on FormGroup dynamically?](#how-will-you-add-and-remove-controls-on-formgroup-dynamically) |
| 13  | [What is difference between (ngModelChange) and (change)?](#what-is-difference-between-ngmodelchange-and-change)                 |
| 14  | [How to add async validation in FormControl?](#how-to-add-async-validation-in-formcontrol)                                       |
| 15  | [How will you validate template-driven form?](#how-will-you-validate-template-driven-form)                                       |
| 16  | [How will you perform two-way binding using ngModel?](#how-will-you-perform-two-way-binding-using-ngmodel)                       |

## Explain RxJS Observable

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
  الـ Observable في RxJS هو طريقة لتبادل البيانات بين اللي بينتجها (الـ producer) واللي بيستخدمها (الـ consumer). تخيل إن فيه حد بيبعث لك بيانات، بس مش هتبعت لك غير لما تطلبها (ده نظام الـ pull)، أو ممكن البيانات تتبعت لك من غير ما تطلبها (ده نظام الـ push).

في الـ JavaScript العادي، أنت اللي بتطلب البيانات (ده زي الـ pull). لكن في الـ RxJS Observable، البيانات بتتبعت لك تلقائيًا أول ما تعمل subscribe للـ Observable (ده نظام الـ push).

في Angular، الـ Observable بتبدأ تشتغل لما تعملها subscribe، وبتقدر تعمل كده إما باستخدام subscribe مباشرةً أو باستخدام async pipe.

</div>

<hr/>

## What are RxJS operators?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
ببساطة RxJS operators هما functions بتساعدك في التعامل مع Observables وبتنقسم لنوعين:

### Pipeable Operators - 1

دي اللي بتشتغل مع Observable.pipe() وبتاخد observable كـ input وتطلع observable جديد. أمثلة عليها: map، switchMap، mergeMap، concatMap، takeUntil، retry، catchError، و throwError.

### Creation Operators - 2

دي اللي بنستخدمها كـ functions مستقلة عشان ننشئ observables. أمثلة عليها: of، from، interval، fromEvent، generate، و range.

</div>

<hr/>

## What is Observable.pipe() and how to use it?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ pipe في RxJS هو اللي بنستخدمه عشان نمرر مجموعة من الـ pipeable operators، اللي بنقدر نستخدمها مع observables. يعني ببساطة، تقدر تحط أي عدد من العمليات (operators) جوه الـ pipe، وهيشتغلوا بالتسلسل. الفكرة إن الـ observable الأساسي بيتبعت لأول operator، والنتيجة بتاعت أول واحد بتتبعت للتاني، وهكذا.

<div dir="auto" align="left">

```typescript
of(101, 102)
  .pipe(
    delay(1000),
    map((num) => num * 2)
  )
  .subscribe((v) => console.log(v)); // 202, 204
```

</div>

في المثال ده، أول حاجة بنستخدم delay(1000) علشان نأخر التنفيذ ثانية (1000 ميلي ثانية).
بعد كده، بنستخدم map اللي بيضرب كل رقم في 2.
النتيجة هتكون: 202، 204 (يعني الأرقام اتضربت في 2 بعد التأخير).

الخلاصة:
الـ pipe بيسهل عليك تنفيذ عمليات متتابعة على البيانات اللي جاية من observable، وده بيديك تحكم أكبر في تعديل الداتا أو توقيتها أو التعامل مع الأخطاء.

</div>

<hr/>

## What is the difference between RxJS of and from?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الفرق بين RxJS of و RxJS from ببساطة هو في نوع المدخلات اللي كل واحد فيهم بيتعامل معاها وطريقة تحويلهم لـ Observable

### of - 1

بتاخد مجموعة من القيم (زي "a" و "b" و "c") وتحولهم لـ observable sequence، يعني كل قيمة بتطلع لوحدها.

<div dir="auto" align="left">

```typescript
of("a", "b", "c").subscribe((e) => console.log(e));
```

</div>
في الحالة دي، كل حرف هيظهر في السطر على حدة.

### from - 2

بتاخد array أو حاجة شبهه (زي promise) وتحوّله لـ observable، يعني كل عنصر جوه الـ array بيتعامل معاه كجزء من الـ observable.

<div dir="auto" align="left">

```typescript
from(["a", "b", "c"]).subscribe((e) => console.log(e));
```

</div>
هنا، نفس القيم اللي كانت في الـ array (يعني "a", "b", "c") هتتعامل معاها كأن كل عنصر بيتطلع لوحده في الـ observable.

</div>

<hr/>

## Explain RxJS map operator?

[⬆️ Back to Top](#top)

![ map ](https://rxjs.dev/assets/images/marble-diagrams/map.png)

<div dir="auto" align="right">
الـ map operator في RxJS ببساطة بيطبق function معينة على كل عنصر بيتم إصداره من الـ Observable. يعني كل عنصر بيعدي من المصدر، بيتم تطبيق الـ function عليه والنتيجة هي اللي بتطلع.

<div dir="auto" align="left">

```typescript
of(1, 2, 3, 4)
  .pipe(map((e) => e * e))
  .subscribe((output) => console.log(output));
```

</div>
في المثال ده:

عندنا observable بيرسل القيم (1, 2, 3, 4).
كل قيمة من القيم دي بتدخل في map، اللي بتضرب القيمة في نفسها (يعني بتربع القيمة).
بعد كده الـ observable الجديد اللي طالع بيرجع القيم: 1, 4, 9, 16.
يعني لما بنعمل subscribe على الـ observable الناتج، بنشوف القيم الجديدة اللي هي 1، 4، 9، و 16 في الـ console.

بكده تقدر تستخدم map علشان تعدل أو تعمل عمليات على البيانات اللي بتيجي من الـ observable الأصلي بطريقة بسيطة.

</div>

<hr/>

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

<div dir="auto" align="left">

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

</div>

## Typeahead with switchMap() and ReactiveForms

<div dir="auto" align="left">

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

</div>

## Typeahead search with switchMap() and BehaviorSubject

<div dir="auto" align="left">

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

</div>

<hr/>

## Explain RxJS mergeMap operator?

[⬆️ Back to Top](#top)

![ mergeMap ](https://rxjs.dev/assets/images/marble-diagrams/mergeMap.png)

<div dir="auto" align="right">
الـ mergeMap في RxJS هو operator بيستخدم في التعامل مع الـ observables، واللي بيعمله إنه بياخد كل element جاية من الـ observable الأولانية وبيعملها subscribe في observable تانية. يعني لو عندك observable بيطلع بيانات، لكل قيمة جاية ممكن تستدعي observable تانية، والـ mergeMap هيعمل merge لكل الـ observables اللي جوا بعض.

فايدته الأساسية إنه بيشتغل بشكل متوازي، يعني لو عندك مثلاً HTTP requests وكل واحدة محتاجة تطلع observable تانية عشان تعمل حاجة زي جلب بيانات، الـ mergeMap هيشغل كل الطلبات دي مع بعض من غير ما يستنى واحدة تخلص عشان يبدأ التانية.

### التعامل مع Multi HTTP requests

مثال على تنفيذ طلبات HTTP متعددة بشكل متوازي باستخدام mergeMap

<div dir="auto" align="left">

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

</div>

### ملحوظة

استخدم الmergeMap لو عند requests زي الPOST , DELETE الي لازم تكتمل بدون الغاء

</div>

<hr/>

## Explain RxJS concatMap operator?

[⬆️ Back to Top](#top)

![ concatMap ](https://rxjs.dev/assets/images/marble-diagrams/concatMap.png)

<div dir="auto" align="right">
الـ concatMap في RxJS بيشتغل بطريقة مشابهة شوية لـ mergeMap، لكن الفرق الرئيسي بينهم هو في طريقة التعامل مع الـ observables اللي طالعة.

الـ concatMap بياخد كل قيمة جاية من الـ observable الأساسي وبيطلع منها observable جديد، بس هنا الـ observables اللي بيطلعها بتشتغل واحدة واحدة بالتتابع. يعني مش هيبدأ الـ observable التاني غير لما الأولاني يخلص. بمعنى آخر، هو بيعمل flattening للـ observables بس بشكل متسلسل بدل ما يكون كله شغال بالتوازي زي ما بيحصل في mergeMap.

<div dir="auto" align="left">

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

</div>

```typescript
 // the output.
(after 2 seconds)
Shree Mohit
(after 2 seconds)
Shree Nilesh
```

</div>

<hr/>

## Explain RxJS exhaustMap operator?

[⬆️ Back to Top](#top)

![ exhaustMap ](https://rxjs.dev/assets/images/marble-diagrams/exhaustMap.png)

<div dir="auto" align="right">
ببساطة كده، exhaustMap بيشتغل بطريقة إنه مش بيهتم غير بالـobservable اللي شغال حاليًا. يعني لو حاجة جديدة جات (زي حدث أو كليك مثلاً) وهو لسه مشغول بحاجة تانية، مش هيبدأ الحاجة الجديدة غير لما يخلص اللي في إيده.

خلينا نقول إن عندك زرار في تطبيق بيفتح حاجة معينة، لو المستخدم ضغط بسرعة على الزرار أكتر من مرة، exhaustMap هيهتم بالضغطة الأولى بس، وهيتجاهل الباقي لحد ما الحاجة اللي بدأها أول مرة تخلص، وبعد كده يبدأ يستقبل حاجات جديدة.

ليه ده مفيد؟
لأنه بيساعد إنك تمنع طلبات كتير تشتغل في نفس الوقت، زي لما تضغط على زر تسجيل الدخول أكتر من مرة، ومش عايز تبعت بياناتك للسيرفر كل مرة غير لما الطلب الأولاني يخلص.

<div dir="auto" align="left">

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

</div>

هنا:

fromEvent بيتابع الكليكات اللي بتحصل على الزرار.
exhaustMap بيتأكد إن مفيش كليك جديد هيتم معالجته غير لما الطلب الحالي يخلص.
interval هنا مجرد مثال لعملية بتاخد شوية وقت (ممكن تعتبره طلب HTTP مثلاً).
كل ضغطة هتستنى لحد ما الكليك الأولاني يخلص قبل ما تقبل كليك جديد.

</div>

<hr/>

## How will you handle errors on observable using RxJS throwError?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في RxJS، لو حصل خطأ أثناء تشغيل الـobservable، ممكن نستخدم throwError عشان نبعت الخطأ ده في الـstream ونتعامل معاه باستخدام الـcatchError أو الـretry operators.

<div dir="auto" align="left">

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

</div>

throwError: لما يحصل خطأ، الـobservable هيعمل emit للخطأ ده.
catchError: بنستخدمه عشان نعمل handle للخطأ. في المثال ده، لو حصل خطأ، بنرجع observable تاني بقيمة بديلة (of('Default value')).
الـsubscribe: لو مفيش أخطاء، الـobserver هياخد الـdata اللي الـobservable بيعملها emit. ولو حصل خطأ هيتم الإمساك بيه في الـcatchError قبل ما يوصل للـsubscribe.

</div>

<hr/>

## Explain RxJS retry operator?

[⬆️ Back to Top](#top)

![ retry ](https://rxjs.dev/assets/images/marble-diagrams/retry.png)

<div dir="auto" align="right">
في RxJS، الـretry هو operator بيُستخدم لما يحصل خطأ في الـobservable، ويسمح بإعادة محاولة تشغيل الـobservable تلقائيًا لعدد معين من المرات قبل ما يدي خطأ نهائي. الفكرة إنه لو عندك عملية ممكن تفشل (زي طلب HTTP)، الـretry بيساعد في إعادة المحاولة كذا مرة على أمل إن المشكلة تتحل، زي مشكلة مؤقتة في الشبكة.

### ازاي تستخدم retry

الـretry بياخد عدد من المرات اللي عايز تكرر فيها المحاولة لما يحصل خطأ. لو عدد المحاولات خلص ولسه فيه خطأ، الـobservable هيرجع خطأ عادي.

<div dir="auto" align="left">

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

</div>

throwError: بنحاكي سيناريو إن الـobservable بيفشل وبيطلع خطأ.
retry(2): هنا بنقول للـobservable إنه يحاول مرتين لو حصل خطأ. يعني بعد أول خطأ، هيحاول مرة كمان، ولو فشل برضه، يحاول للمرة الأخيرة.
catchError: لو المحاولات كلها فشلت، بنمسك الخطأ ونتعامل معاه. في المثال، بنرجع قيمة افتراضية (Fallback value).
الـsubscribe: لو مفيش أخطاء، الـobservable هيعمل emit للـdata عادي، لكن لو كل المحاولات فشلت، هيوصل الخطأ للـcatchError وهنرجع القيمة البديلة.

سيناريوهات للاستخدام:
طلبات HTTP متكررة: ممكن تكون بتعمل طلب لـAPI وفيه مشاكل مؤقتة في الاتصال، زي انقطاع الشبكة. في الحالة دي، بدل ما الطلب يفشل مباشرة، ممكن تحاول كذا مرة باستخدام retry، وتدي فرصة إن المشكلة تتحل.

عمليات غير مستقرة: في عمليات زي الكتابة أو القراءة من قاعدة بيانات أو التعامل مع ملفات، ممكن يحصل فشل بسبب عوامل خارجية (زي مشكلة في التخزين المؤقت). باستخدام retry، تقدر تعيد المحاولة بدون الحاجة لتدخل المستخدم كل مرة.

<div dir="auto" align="left">

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

</div>

retry(3): بنطلب من RxJS إعادة المحاولة 3 مرات لو حصل فشل في طلب الـAPI.
catchError: لو كل المحاولات فشلت، بنعمل catch للخطأ ونتعامل معاه، مثلاً نرجع بيانات افتراضية بدل ما نوقف التطبيق.
الـretry بيكون مفيد في الحالات اللي بتحصل فيها أخطاء غير متوقعة أو مؤقتة، وبيسمح للتطبيق يكون أكثر مرونة في التعامل مع الأخطاء بدون الحاجة لتدخل المستخدم في كل مرة

</div>

<hr/>

## Explain RxJS filter operator?

[⬆️ Back to Top](#top)

![ filter ](https://rxjs.dev/assets/images/marble-diagrams/filter.png)

<div dir="auto" align="right">
في RxJS، الـfilter هو operator بنستخدمه عشان نعمل "فلترة" للـvalues اللي الـobservable بيعمل لها emit. بمعنى تاني، هو بيشغل callback function على كل قيمة، ولو الشرط اللي في الـcallback اتحقق، بيمرر القيمة دي، ولو لأ، بيتجاهلها.

### ازاي تستخدم filter

الـfilter بياخد كل قيمة جاية من الـobservable ويشوف لو القيمة دي بتوافق الشرط اللي في الـcallback.
لو القيمة مطابقة للشرط، بتكمل في الـobservable stream، ولو لأ، بتتفلتر وتتجاهل.

<div dir="auto" align="left">

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

</div>

### الاستخدام

فلترة الأحداث: مثلاً، في حالة استماعك لأحداث معينة (زي ضغطات المستخدم على زر معين)، ممكن تستخدم filter عشان تتعامل بس مع نوع معين من الأحداث (زي لو المستخدم ضغط على زرار معين في الـUI).

طلبات الـHTTP: لو عندك استجابة API وبيجيلك فيها بيانات كتيرة، ممكن تستخدم filter عشان تمرر فقط القيم اللي تحقق شروط معينة (مثلاً، طلبات فيها status معين أو بيانات بنطاق معين).

<div dir="auto" align="left">

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

</div>

fromEvent: بنعمل observable للضغطات على زرار معين.
filter: هنا بنفلتر الأحداث ونتعامل بس مع الضغطات اللي حصلت في النصف الأيسر من الشاشة (على أساس إن قيمة clientX أقل من نصف عرض الشاشة).

</div>

<hr/>

## Explain RxJS tap operator?

[⬆️ Back to Top](#top)

![ tap ](https://rxjs.dev/assets/images/marble-diagrams/tap.png)

<div dir="auto" align="right">
في RxJS، الـtap هو operator بيُستخدم عشان تنفذ side effects على الـobservable، من غير ما تغير أو تعدل على الـvalues اللي بتخرج منه. هو بيكون مفيد لما تحتاج تطبع القيم في الـconsole، أو تعمل logging، أو أي عمليات أخرى أثناء مرور البيانات في الـstream، بس من غير ما تتدخل في البيانات نفسها.

### إزاي بيشتغل الـtap؟

الـtap بياخد function بتتنفذ لكل قيمة بتعدي في الـobservable.
القيم بتعدي بدون أي تعديل، فالـtap مش بيغير الـstream، لكنه بيسمح لك تعمل شيء إضافي أثناء مرور البيانات.

<div dir="auto" align="left">

```typescript
import { of } from "rxjs";
import { tap, map } from "rxjs/operators";

const numbers$ = of(1, 2, 3, 4, 5).pipe(
  tap((value) => console.log("Before map:", value)),
  map((value) => value * 10),
  tap((value) => console.log("After map:", value))
);

numbers$.subscribe(
  (value) => console.log("Final value:", value),
  (error) => console.log("Error:", error),
  () => console.log("Complete")
);
```

</div>

### فايدة الـtap

Logging: لو عايز تتابع القيم اللي بتعدي في الـobservable لأي سبب، زي الـdebugging.
Side effects: لو محتاج تعمل أي عملية أثناء مرور البيانات من غير ما تعدل على القيم. مثال على ده: تحديث UI، تسجيل أحداث، أو تعديل بيانات في مكان تاني بناءً على القيم اللي بتعدي.

</div>

<hr/>

## Explain RxJS takeUntil operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في RxJS، الـtakeUntil هو operator بيستخدم عشان يوقف الـobservable عن إصدار القيم (emit) لما observable تاني يعمل emit. بمعنى تاني، الـtakeUntil بيمسك الـobservable الأصلي وبيخليه شغال لحد ما observable معين (اللي بنسميه notifier) يصدر قيمة، وبعدين يوقف الـobservable الأصلي عن العمل.

### إزاي بيشتغل الـtakeUntil؟

عندك observable رئيسي بيرسل قيم (مثلاً، تدفق للأرقام، أو استجابة لأحداث).
وعندك observable تاني بنسميه notifier، وده مجرد observable بيتراقب لحد ما بيرسل أي قيمة.
بمجرد ما الـnotifier بيرسل أول قيمة، الـobservable الرئيسي بيتوقف عن ارسال أي قيم جديدة.

### من اكتر استخدماته اننا بنستخدمه في الdestroy

<div dir="auto" align="left">

```typescript
import { Component, OnInit, OnDestroy } from "@angular/core";
import { Subject } from "rxjs";
import { takeUntil } from "rxjs/operators";

@Component({
  selector: "app-my-component",
  templateUrl: "./my-component.component.html",
  styleUrls: ["./my-component.component.css"],
})
export class MyComponent implements OnInit, OnDestroy {
  // الـnotifier اللي هيشغل takeUntil
  private componentDestroyed: Subject<void> = new Subject<void>();

  constructor() {}

  ngOnInit() {
    // Example: لو عندك Observable مثلاً بيسمع للأحداث أو بيطلب بيانات
    this.someObservable()
      .pipe(
        takeUntil(this.componentDestroyed) // هيوقف الـObservable لما الـcomponent يتدمر
      )
      .subscribe((data) => {
        console.log("Data received:", data);
      });
  }

  someObservable() {
    // ده الـObservable اللي هيشترك فيه الـcomponent (مجرد مثال)
    return of("Some data");
  }

  ngOnDestroy() {
    // هنا بنعمل emit للقيمة عشان نوقف الـObservables
    this.componentDestroyed.next();
    this.componentDestroyed.complete(); // عشان نضمن إن الـSubject مش هيستخدم تاني
  }
}
```

</div>

### ليه بنستخدم takeUntil بالطريقة دي؟

إدارة الاشتراكات: الـtakeUntil بيضمن إن أي اشتراكات للـobservables بتتوقف تلقائيًا لما الـcomponent يتدمر، وده بيساعد على عدم تسرب الذاكرة (memory leaks).

مرونة: الطريقة دي سهلة وبتشتغل مع أي observable في الـcomponent سواء كان HTTP request، أو WebSocket، أو أي نوع تاني من الـobservables.

باستخدام takeUntil مع الـSubject<void>، بتقدر تضمن إن أي اشتراكات بتتوقف بطريقة منظمة وفعالة لما الـcomponent يخرج من الـDOM.

</div>

<hr/>

## Explain RxJS debounceTime operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
هو واحد من أقوى الـoperators في RxJS وبيفيد بشكل كبير لما بنحتاج نتعامل مع سلسلة من القيم اللي بتتبع بعضها بسرعة، زي في حالة البحث اللحظي أو الحفظ التلقائي. الـdebounceTime بيسمح لنا نفلتر القيم اللي بتتبع بشكل سريع من الـobservable، ونحافظ بس على القيمة الأخيرة بعد فترة معينة من الزمن، وده مفيد لما ما نكونش محتاجين نتعامل مع كل قيمة بتطلع.

### إزاي بيشتغل الـdebounceTime

تأخير القيم: أول ما تيجي قيمة من الـobservable، الـdebounceTime بيبدأ يعد الزمن المحدد (مثلاً 300 مللي ثانية).
إعادة ضبط المؤقت: لو حصلت قيمة جديدة قبل ما الزمن المحدد ينتهي، المؤقت بيبدأ يعد من الأول تاني.
القيمة الأخيرة فقط: لما الزمن المحدد ينتهي ومافيش قيم جديدة جات، القيمة الأخيرة هي اللي بتعدي.

### Basic Usage

<div dir="auto" align="left">

```typescript
const result = fromEvent(document, "click").pipe(
  // Click event is delayed for 1000ms or 1s
  // It emits the most recent click event, even after burst clicking
  debounceTime(1000)
);

result.subscribe((value) => console.log(value));
```

</div>

### Real-time search with debounceTime

لما المستخدم يكتب في خانة البحث، بنقدر نستخدم debounceTime عشان نمنع إرسال طلب للسيرفر مع كل ضغطة على الكيبورد. بدال ما نبعت طلب بعد كل حرف، بنستنى فترة قصيرة قبل ما نبعته فعليًا.

<div dir="auto" align="left">

```typescript
@Component({
  ...
  template: `
  <input [formControl]="searchBar" type="text">
  `,
})
export class AppComponent {
  public readonly searchBar = new FormControl();

  public readonly searchResults$ = this.searchBar.valueChanges.pipe(
    debounceTime(1000), // Waits for 1000ms or 1s before emitting
    distinctUntilChanged() // doesn't emit if current value = previous value
  );

  constructor() {
    this.searchResults$.subscribe((query) => {
      console.log(query);
    });
  }
}
```

</div>

### Autosave with debounceTime

<div dir="auto" align="left">

```typescript
@Component({
  ...
  template: `
    <form [formGroup]="form" (ngSubmit)="save()">
        <input type="text" formControlName="firstName">
        <input type="text" formControlName="lastName">
        <button type="submit">Save</button>
    </form>
  `,
})
export class UserFormComponent implements OnInit {
  ...

  public readonly form = this.fb.group(...);

  ngOnInit() {
    this.form.valueChanges
      // Wait for 500ms after each keystroke before saving the user
      .pipe(debounceTime(500))
      .subscribe((user: User) => {
        this.userService.saveUser(user);
      });
  }

  ...
}
```

</div>

### Conclusion

الـdebounceTime هو واحد من أفضل الـoperators في RxJS لما بتتعامل مع سلاسل متتابعة من القيم بسرعة، وبيساعد في تحسين الأداء وتجربة المستخدم عن طريق تقليل الطلبات أو الاستجابات اللي ممكن تكون غير ضرورية.

</div>

<hr/>

## Explain RxJS combineLatestWith operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـcombineLatest هو operator بيجمع أكتر من observable في واحد، وبيعمل emit للقيم بتاعته كل ما واحد منهم يغير القيم بتاعته. ده بيخليه operator قوي جدًا، لكن فيه شوية حاجات لازم ناخد بالنا منها لما نستخدمه.

### إزاي الـcombineLatest بيشتغل:

الـcombineLatest بياخد array من الـobservables كمصدر، وبيطلع observable جديد بيحسب بناءً على أحدث القيم من كل observable مصدر. الموضوع باين إنه بسيط، لكن فيه شوية حاجات لازم نكون عارفينها:

كل الـobservables اللي في المصدر لازم يعملوا emit مرة على الأقل قبل ما الـcombineLatest يبدأ يطلع بيانات.
كل مرة observable من المصادر يعمل emit لقيمة جديدة، الـcombineLatest بيحسب القيمة من الأول. وده ممكن يخلي الـobservable يطلع بيانات كتير بسرعة، ودي حاجة لازم نخلي بالنا منها.
في أغلب الأوقات، هتحتاج تستخدم الـcombineLatest مع Observables طويلة المدى (long-lived observables).

### Usage

ممكن نعمل فلتر متعدد باستخدام combineLatest في Angular لما يكون عندنا أكتر من مصدر للفلترة، زي فلترة على اسم، تاريخ، وكاتيجوري مثلاً. باستخدام combineLatest، بنقدر ندمج الفلاتر دي كلها عشان نعمل الفلترة المطلوبة.

خلينا نشوف مثال عملي على عمل فلتر متعدد باستخدام combineLatest.

خطوات:
هنفترض إن عندنا Array من العناصر اللي محتاجين نفلترها.
هنستخدم أكتر من FormControl عشان نتحكم في الفلاتر.
هنستخدم combineLatest عشان ندمج القيم من كل فلتر ونعرض النتيجة النهائية.

<div dir="auto" align="left">

```typescript
import { Component, OnInit } from "@angular/core";
import { FormControl } from "@angular/forms";
import { combineLatest, of } from "rxjs";
import { map, startWith } from "rxjs/operators";

@Component({
  selector: "app-multi-filter",
  template: `
    <input [formControl]="nameFilter" placeholder="Filter by name" />
    <input [formControl]="categoryFilter" placeholder="Filter by category" />
    <input
      type="date"
      [formControl]="dateFilter"
      placeholder="Filter by date"
    />

    <ul>
      <li *ngFor="let item of filteredItems$ | async">
        {{ item.name }} - {{ item.category }} - {{ item.date }}
      </li>
    </ul>
  `,
})
export class MultiFilterComponent implements OnInit {
  // الفلاتر
  nameFilter = new FormControl("");
  categoryFilter = new FormControl("");
  dateFilter = new FormControl("");

  // قائمة العناصر اللي هنفلترها
  items = [
    { name: "Item 1", category: "A", date: "2023-01-01" },
    { name: "Item 2", category: "B", date: "2023-01-02" },
    { name: "Item 3", category: "A", date: "2023-01-03" },
    { name: "Item 4", category: "C", date: "2023-01-04" },
  ];

  // الـObservable اللي هيحتوي على العناصر المفلترة
  filteredItems$ = combineLatest([
    this.nameFilter.valueChanges.pipe(startWith("")),
    this.categoryFilter.valueChanges.pipe(startWith("")),
    this.dateFilter.valueChanges.pipe(startWith("")),
  ]).pipe(
    map(([name, category, date]) => {
      return this.items.filter(
        (item) =>
          item.name.toLowerCase().includes(name.toLowerCase()) &&
          item.category.toLowerCase().includes(category.toLowerCase()) &&
          item.date.includes(date)
      );
    })
  );

  ngOnInit() {}
}
```

</div>
</div>

<hr/>

## Explain RxJS fromEvent operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في RxJS، الـfromEvent هو operator بنستخدمه عشان نعمل "observable" من الأحداث اللي بتحصل في الـDOM (أو أي مصدر أحداث تاني). بعبارة تانية، بنقدر نسمع لأي أحداث زي الكليكات، ضغطات الكيبورد، تحريك الماوس، وغيرها، ونتعامل معاها زي أي observable.

### إزاي بيشتغل الـfromEvent؟

بنمرر له العنصر اللي عايزين نسمع منه الأحداث (زي زرار أو صفحة كاملة).
بنحدد نوع الحدث اللي عايزين نسمعه (زي 'click'، 'keyup'، 'mousemove'، إلخ).
بعد كده بنستخدم الـobservable الناتج عشان نعمل اشتراك (subscription) ونتعامل مع الحدث.

<div dir="auto" align="left">

```typescript
import { fromEvent } from "rxjs";
import { filter } from "rxjs/operators";

const button = document.getElementById("myButton");

const clicks$ = fromEvent(button, "click").pipe(
  filter((event: MouseEvent) => event.clientX < window.innerWidth / 2) // نتعامل مع الكليكات في النصف الأيسر من الشاشة فقط
);

clicks$.subscribe((event) => {
  console.log("Clicked on the left side!", event);
});
```

</div>

</div>

<hr/>

## What is the difference between Subject, BehaviorSubject, ReplaySubject, and AsyncSubject in RxJS? How do they differ in terms of behavior and use cases?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الفرق بين Subject و BehaviorSubject و ReplaySubject و AsyncSubject في RxJS
كل واحد من هذه الأنواع له سلوك خاص في التعامل مع observables والبيانات اللي يتم بثها للمشتركين (subscribers). خلينا نشرح كل واحد بالتفصيل، مع ذكر الفروق بينهم في السلوك والاستخدامات.

### 1. Subject

Subject هو observable عادي، لكن مع ميزات إضافية. يمكنه أن يستقبل بيانات ويصدرها، ويستطيع أكثر من subscriber الاشتراك فيه.
لا يحتفظ بأي بيانات سابقة: لو اشتركت في الـSubject بعد ما أرسل بيانات بالفعل، لن تتلقى البيانات السابقة، وستبدأ في تلقي القيم الجديدة فقط.

### السلوك:

أي مشترك جديد يبدأ في استقبال البيانات من اللحظة اللي اشترك فيها فقط، ولا يتلقى أي قيم سابقة.

### الاستخدامات:

مناسب للبث المباشر (real-time broadcasting) حيث لا نحتاج للاحتفاظ بالبيانات السابقة.

<div dir="auto" align="left">

```typescript
import { Subject } from "rxjs";

const subject = new Subject();

subject.subscribe((value) => console.log("Subscriber 1:", value));

subject.next(1); // Subscriber 1: 1
subject.next(2); // Subscriber 1: 2

subject.subscribe((value) => console.log("Subscriber 2:", value));

subject.next(3); // Subscriber 1: 3, Subscriber 2: 3
```

</div>

💡**Hint**: المشترك الأول يتلقى جميع القيم، لكن المشترك الثاني يتلقى فقط القيم الجديدة التي تم إرسالها بعد الاشتراك.

### 2. BehaviorSubject

BehaviorSubject هو نوع خاص من الـSubject يحتفظ دائمًا بآخر قيمة تم إصدارها.
عندما يشترك أي subscriber جديد، يستلم فورًا آخر قيمة تم بثها حتى لو تم الاشتراك بعد إرسال هذه القيمة.

### السلوك:

كل مشترك جديد يستلم آخر قيمة تم إصدارها، ثم يتلقى التحديثات الجديدة.

### الاستخدامات:

مفيد عندما تحتاج أن يحصل المشترك الجديد على آخر حالة أو آخر قيمة تم إصدارها بالفعل (مثل تحديث حالة المستخدم، أو تحميل بيانات التطبيق).

<div dir="auto" align="left">

```typescript
import { BehaviorSubject } from "rxjs";

const behaviorSubject = new BehaviorSubject(0); // القيمة الافتراضية هي 0

behaviorSubject.subscribe((value) => console.log("Subscriber 1:", value));

behaviorSubject.next(1); // Subscriber 1: 1
behaviorSubject.next(2); // Subscriber 1: 2

behaviorSubject.subscribe((value) => console.log("Subscriber 2:", value)); // Subscriber 2: 2

behaviorSubject.next(3); // Subscriber 1: 3, Subscriber 2: 3
```

</div>

💡**Hint** المشترك الثاني استلم القيمة الأخيرة (2) فور اشتراكه، ثم استلم القيمة الجديدة التي أرسلت بعد ذلك (3).

### 3. ReplaySubject

ReplaySubject هو نوع آخر من Subjects يمكنه أن يحتفظ بعدد معين من القيم السابقة (أو حتى كل القيم) ويعيد بثها لأي مشترك جديد عند الاشتراك.
يمكن تحديد عدد القيم التي يتم إعادة بثها للمشتركين الجدد، مثل آخر قيمة أو آخر قيمتين أو أكثر.

### السلوك:

أي مشترك جديد يتلقى عددًا معينًا من القيم السابقة (يمكن تحديد العدد)، ثم يبدأ في تلقي التحديثات الجديدة.

### الاستخدامات:

مفيد في التطبيقات التي تحتاج إلى إعادة تشغيل التاريخ (history replay) لمشتركين جدد، مثل تسجيل النشاطات أو الأحداث السابقة.

<div dir="auto" align="left">

```typescript
import { ReplaySubject } from "rxjs";

const replaySubject = new ReplaySubject(2); // يحتفظ بآخر قيمتين

replaySubject.next(1);
replaySubject.next(2);
replaySubject.next(3);

replaySubject.subscribe((value) => console.log("Subscriber 1:", value)); // Subscriber 1: 2, 3

replaySubject.next(4); // Subscriber 1: 4

replaySubject.subscribe((value) => console.log("Subscriber 2:", value)); // Subscriber 2: 3, 4
3;
```

</div>

💡 **Hint**: المشترك الأول استلم القيمتين الأخيرتين (2 و 3)، بينما المشترك الثاني استلم (3 و 4) لأنه اشترك بعد إرسال القيم.

### 4. AsyncSubject

AsyncSubject هو نوع من الـSubject لا يصدر أي قيم للمشتركين إلا بعد اكتمال الـobservable، وعندها يقوم بإرسال آخر قيمة فقط تم بثها قبل الاكتمال لجميع المشتركين.
لا يصدر أي شيء حتى يتم استدعاء complete

### السلوك:

المشتركين يستلمون آخر قيمة فقط عندما يتم استدعاء complete

### الاستخدامات:

يستخدم عندما تحتاج إلى إصدار آخر قيمة فقط عند انتهاء العمل، مثل استرجاع بيانات بعد إتمام عملية معقدة أو عند اكتمال عملية حسابية.

<div dir="auto" align="left">

```typescript
import { AsyncSubject } from "rxjs";

const asyncSubject = new AsyncSubject();

asyncSubject.subscribe((value) => console.log("Subscriber 1:", value));

asyncSubject.next(1);
asyncSubject.next(2);
asyncSubject.next(3);

asyncSubject.subscribe((value) => console.log("Subscriber 2:", value));

asyncSubject.next(4);
asyncSubject.complete(); // عند الاكتمال، يتم إرسال آخر قيمة

// Subscriber 1: 4
// Subscriber 2: 4
```

</div>

💡 **Hint** : هنا، المشتركين الاثنين استلموا فقط القيمة الأخيرة (4) بعد اكتمال الـobservable.

### متى تستخدم كل نوع؟

Subject: لما تكون مش محتاج تحتفظ بأي بيانات سابقة، وعايز تبث القيم الجديدة فقط للمشتركين الحاليين.
BehaviorSubject: لما تحتاج أن يحصل المشترك الجديد على آخر قيمة تم إصدارها، حتى لو اشترك بعد إرسالها (مثل حالة المستخدم أو حالة التطبيق).
ReplaySubject: لما تحتاج أن يحصل المشترك الجديد على عدد من القيم السابقة أو كل القيم التي تم إصدارها (مثل تسجيل الأحداث السابقة).
AsyncSubject: لما تحتاج أن يحصل المشترك على آخر قيمة فقط بعد اكتمال العمل (مثل نتائج عملية معقدة أو حسابية).

</div>
<hr/>

## What are the best practices for managing Observable subscriptions in Angular and ensuring there are no memory leaks?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### ليه manage subscriptions مهمة؟

في Angular، لما بتشتغل مع Observables زي HTTP requests أو حتى events زي كليك أو تغيير بيانات، لازم تتأكد إنك بتفصل (unsubscribe) عنهم لما ما تكونش محتاجهم، زي لما الـcomponent يتشال من الصفحة أو يتدمر. لو ما عملتش كده، ممكن يحصل تسرب في الذاكرة (memory leaks)، وده بيأثر على أداء التطبيق بتاعك مع الوقت.

## أفضل الطرق manage subscriptions

1. استخدام async pipe
   دي أسهل طريقة ومريحة جدًا، وبتستخدمها لما يكون عندك observable في (template) بتاعك، وعايز تشتغل معاه. async pipe بيعمل كل الشغل الصعب عنك. يعني بيشترك في الـobservable، ولما الـcomponent يتدمر أو يخرج من الشاشة، بيعمل unsubscribe تلقائيًا.

<div dir="auto" align="left">

```typescript
<div *ngIf="data$ | async as data">
  {{ data }}
</div>
```

</div>
هنا لما البيانات (data$) تتغير، الـasync pipe بيجيبها لك ويعرضها.
ولو الـcomponent اتشال أو المستخدم راح لشاشة تانية، الـasync pipe بيعمل unsubscribe تلقائي.
<hr/>

2. استخدام takeUntil مع Subject
الفكرة إنك تعمل Subject كإشارة (notifier) عشان تدي أمر لجميع الـobservables إنهم يوقفوا لما الـcomponent يتم تدميره. بتستخدم takeUntil كـ operator في الـ pipe عشان يتحقق من الـ Subject، وأول ما تبعتله إشعار (signal)، هو هيوقف كل الاشتراكات.
<div dir="auto" align="left">

```typescript
import { Subject } from "rxjs";
import { takeUntil } from "rxjs/operators";

export class MyComponent implements OnDestroy {
  private destroy$ = new Subject<void>();

  ngOnInit() {
    this.myObservable$
      .pipe(takeUntil(this.destroy$)) // هنا بنوقف الاشتراك لما الـdestroy$ تعمل emit
      .subscribe((data) => {
        console.log(data);
      });
  }

  ngOnDestroy() {
    this.destroy$.next(); // بنعمل إشعار إن الـcomponent اتدمر
    this.destroy$.complete(); // بننهي الـSubject تمامًا
  }
}
```

</div>

في المثال ده، بنستخدم destroy$ كإشارة لوقف الاشتراكات لما ngOnDestroy يتنفذ (الـcomponent يتشال).
كل الاشتراكات بتقف لما الـcomponent يتدمر، وده بيمنع تسرب الذاكرة.

<hr/>

3. التحديث الجديد في Angular 16: takeUntilDestroyed
   في Angular 16، ظهر شيء جديد اسمه takeUntilDestroyed وده بيسهل الموضوع أكتر. بدل ما تكتب كود كتير عشان تعمل takeUntil مع Subject، دلوقتي Angular وفرت لك حل جاهز.

### إزاي بنستخدمه؟

دلوقتي، مفيش داعي لإنك تعمل Subject بنفسك وتتحكم فيه. Angular هتتعامل مع الموضوع بشكل أوتوماتيكي.

<div dir="auto" align="left">

```typescript
import { takeUntilDestroyed } from "@angular/core/rxjs-interop";

export class MyComponent {
  ngOnInit() {
    this.myObservable$
      .pipe(takeUntilDestroyed(this)) // هنا بنمرر الـcomponent كـcontext
      .subscribe((data) => {
        console.log(data);
      });
  }
}
```

</div>

takeUntilDestroyed بيخليك تعمل نفس اللي كنا بنعمله مع takeUntil و Subject، بس بشكل أبسط وأسرع.
مش محتاج تعمل أي Subject، ومجرد ما الـcomponent يتدمر، Angular هتعمل unsubscribe تلقائي.

</div>

<hr/>

## what are the differences between cold observable and hot observable?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الفرق بين Hot Observables و Cold Observables ممكن يتلخص في طريقة تصرفهم مع المشتركين (subscribers) والبيانات اللي بيبعتوها.

### Cold Observables

الـ Cold Observable هو النوع اللي بيبدأ يشتغل لما حد يشترك فيه. يعني إيه؟ يعني مش بيبدأ يبعث بيانات أو يعمل أي حاجة إلا بعد ما أول مشترك يظهر.

💡 مثال بسيط:
لو عندك طلب HTTP (زي لما تطلب بيانات من سيرفر)، الطلب ده بيكون Cold Observable. ليه؟ لأنه هيبدأ يجيب البيانات ويشتغل بس لما المشترك الأول يشترك فيه.

كل مشترك جديد هيبدأ من الأول كأنه بيطلب نفس البيانات لأول مرة. يعني، لو فيه أكتر من مشترك، كل واحد هيعمل الطلب الخاص بيه.

<div dir="auto" align="left">

```typescript
const coldObservable = new Observable((observer) => {
  observer.next(Math.random());
});

coldObservable.subscribe((value) => console.log("Subscriber 1:", value));
coldObservable.subscribe((value) => console.log("Subscriber 2:", value));
```

</div>

في المثال ده، كل مشترك هيستقبل قيمة مختلفة لأن الـobservable هيشتغل من الأول مع كل اشتراك

### Hot Observables

الـ Hot Observable، على العكس، بيبدأ يبعث بيانات بمجرد ما يشتغل، حتى لو مفيش حد مشترك فيه. وده معناه إن أي مشترك جديد هيشترك في النص ويبدأ ياخد البيانات من اللحظة اللي هو اشترك فيها، مش من الأول.

💡 مثال بسيط:
لو عندك event زي حركة الماوس أو ضغطات زرار، ده يعتبر Hot Observable، لأنه بيبعت البيانات أول ما يحصل الحدث، بغض النظر لو كان فيه مشتركين ولا لأ.

كل مشترك جديد بيشترك بياخد البيانات من اللحظة اللي اشترك فيها. لو حاجة حصلت قبل كده، المشترك الجديد مش هيشوفها.

<div dir="auto" align="left">

```typescript
const hotObservable = new Subject();

hotObservable.subscribe((value) => console.log("Subscriber 1:", value));

hotObservable.next(Math.random());

hotObservable.subscribe((value) => console.log("Subscriber 2:", value));

hotObservable.next(Math.random());
```

</div>
</div>

</hr>

## What are the differences between Observables and Promises?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
الفرق بين الـ Observables والـ Promises يعتبر مهم جدًا لما تيجي تتعامل مع الكود الـ Asynchronous في JavaScript أو Angular.

### التشابهات بين Promise و Observable

- الاتنين بيشتغلوا مع العمليات Asynchronous (غير المتزامنة).
- الاتنين بيتحكموا في إمتى الكود اللي حاطه المستخدم هياخد القيمة.

### الفرق بينهم

#### 🏃‍♀️ التنفيذ (Execution)

##### Promise

بيتنفذ فورًا بمجرد ما يتكتب. يعني بمجرد ما تكتب الكود اللي بيعمل promise، هيتنفذ على طول حتى لو لسه ماعملتش then عليه. يعني الكود اللي جواه هيشتغل مباشرة.

##### Observable

بيشتغل بس لما تعمل subscribe، يعني مش هيبدأ يشتغل غير لما تطلبه. ده معناه إنك ممكن "تحضر" الـobservable لعملية async لكن ما تنفذوش غير لما تحتاجه.

#### 📦 القيم (Values)

##### Promise

بيطلع قيمة واحدة بس أو خطأ. يعني هو يا إما يرجعلك النتيجة أو يرمي خطأ لو حصل مشكلة.

##### Observable

ممكن يطلعلك أكتر من قيمة أو قيمة واحدة أو مفيش قيمة خالص. ده معناه إنه مناسب لحاجات زي الأحداث المتكررة (زي الضغط على زرار أكتر من مرة) أو التعامل مع event emitters في Angular.

**مثال**: لو عندك حاجة بتعمل استجابة للأحداث زي حركة الماوس أو كتابة المستخدم، الـobservable هو الحل الأمثل.

#### 🚧 الإلغاء (Cancellation)

##### Promise

مينفعش يتلغي. بمجرد ما يبدأ، بيكمل شغله حتى لو مش محتاجه. فيه بعض الطرق أو المكتبات اللي بتحاول تحايل على الموضوع، بس الـPromise في الأساس مش معمول للإلغاء.

##### Observable

معمول إنه يكون قابل للإلغاء، وده بيساعدك في إدارة الموارد بتاعتك بشكل أحسن. تقدر تلغي الاشتراك باستخدام unsubscribe أو من خلال الـoperators.

**في Angular**، ده بيساعدك تعمل حاجات زي الـ typeahead (بحث مباشر) وتمنع تسرب الذاكرة باستخدام takeUntil اللي بيوقف الـobservable لما الـcomponent يتشال.

#### ⚙️ (Operators)

##### Promise

مفيهوش operators، يعني مفيش طرق جاهزة للتعامل مع البيانات اللي بترجع من promise غير بإنك تستعمل then أو catch.

##### Observable

عنده أنواع كتير من الـ operators، زي التحويل، الفلترة، التعامل مع الأخطاء، والـoperators دي بتخليك تعمل حاجات معقدة بطرق بسيطة جدًا.

**مثال**: تقدر تعمل حاجات زي map لتحويل البيانات، أو debounceTime عشان تأخر تنفيذ الـobservable، أو catchError للتعامل مع الأخطاء.

#### الخلاصة

##### Promise

بيبدأ الشغل فورًا وبيطلعلك قيمة واحدة بس.
مش قابل للإلغاء، لكن Observable قابل للإلغاء.

##### Observable

بيبدأ بس لما تعمل اشتراك وممكن يطلعلك قيم متعددة.
عندها operators قوية جدًا بتخليك تتعامل مع البيانات بسهولة، وده بيفرق كتير في المشاريع الكبيرة.

</div>
<hr/>

## What is a higher-order Observable?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
الـ Higher-order Observable ببساطة هو Observable اللي بيطلع Observables تانية، بدل ما يطلع قيم عادية زي أرقام أو نصوص. يعني تقدر تقول إنه بيطلع Observable داخل Observable

### إمتى بنحتاج الـ Higher-order Observable؟

لما يكون عندك عمليات غير متزامنة كتيرة، زي إنك تعمل طلبات HTTP متتابعة أو تتعامل مع أحداث معينة بشكل مرتب، هنا بيجي دور الـ Higher-order Observable. هو بيساعدك على إنك "تسلسل" العمليات دي بشكل مرتب وفعال.

### إزاي بنتعامل مع الـ Higher-order Observable؟

عشان نتعامل مع الـ Higher-order Observables، بنستخدم Operators زي:
mergeMap
switchMap
concatMap

الـ Operators دي بتساعد على "flatten " أو "دمج" الـObservables اللي طالعين من الـ Higher-order Observable عشان يكون عندك Observable واحد في النهاية، وتقدر تشترك فيه بشكل عادي وتتعامل مع القيم اللي بتطلع منه.

### كل Operator بيشتغل إزاي؟

#### mergeMap

بيعمل flatten للـObservables اللي بتطلع من الـObservable الأصلي، ويشغلهم كلهم بالتوازي. يعني لو فيه أكتر من Observable طالع، كلهم هيشتغلوا في نفس الوقت.

#### switchMap

ده بيعمل flatten زي mergeMap، لكن الفرق إنه بيبدل الاشتراك لو فيه Observable جديد طلع. يعني لو فيه Observable جديد طلع، بيكنسل القديم ويشتغل على الجديد بس.

#### concatMap

ده بيشتغل زيهم بس بالتتابع. يعني كل Observable يخلص الأول قبل ما اللي بعده يبدأ، وده بيفيد لما يكون فيه ترتيب مهم لازم يتبع.

#### 💡 مثال

 <div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable({
  providedIn: "root",
})
export class UserService {
  private apiUrl = "https://jsonplaceholder.typicode.com/users";

  constructor(private http: HttpClient) {}

  getUserById(id: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/${id}`);
  }
}
```

</div>
 نعمل component فيه input عشان المستخدم يكتب ID، ونعمل اشتراك (subscribe) في القيمة:

 <div dir="auto" align="left">

```typescript
import { Component, OnInit } from "@angular/core";
import { FormControl } from "@angular/forms";
import { UserService } from "./user.service";
import { switchMap, debounceTime, distinctUntilChanged } from "rxjs/operators";

@Component({
  selector: "app-user-search",
  template: `
    <h2>Search for User</h2>
    <input
      type="number"
      [formControl]="userIdControl"
      placeholder="Enter User ID"
    />

    <div *ngIf="userData">
      <h3>User Details:</h3>
      <p>Name: {{ userData.name }}</p>
      <p>Email: {{ userData.email }}</p>
      <p>Address: {{ userData.address.street }}, {{ userData.address.city }}</p>
    </div>
  `,
})
export class UserSearchComponent implements OnInit {
  userIdControl = new FormControl();
  userData: any;

  constructor(private userService: UserService) {}

  ngOnInit() {
    // Listen for changes in the user ID input
    this.userIdControl.valueChanges
      .pipe(
        debounceTime(300), // Small delay to allow the user to finish typing
        distinctUntilChanged(), // Ensure the new value is different from the previous one
        switchMap((id: number) => this.userService.getUserById(id)) // Switch to a new request based on the new ID
      )
      .subscribe((data) => {
        this.userData = data; // Store the user data from the API response
      });
  }
}
```

</div>

</div>

<hr/>

## How can you share a single Observable among multiple subscribers?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
لما تيجي تشارك Observable واحد بين أكتر من مشترك (subscriber)، ممكن تستخدم share أو shareReplay. دول operators في RxJS بيساعدوك إنك تخلي الـObservable يتشارك بين المشتركين بدل ما كل واحد يعمل اشتراك منفصل ويبدأ العملية من الأول.

### إزاي الكلام ده بيفيدك؟

لما يكون عندك Observable بيعمل عملية معينة زي طلب HTTP، الطبيعي إن كل مشترك هيعمل طلب جديد، وده ممكن يكون مشكلة لو عندك مشتركين كتير، لأن كل واحد هيبدأ الطلب من الأول.

لكن لما تستخدم share، المشتركين كلهم هيشتركوا في نفس الـObservable اللي شغال بالفعل، فمش هيعملوا طلبات متكررة، هيستفيدوا من نفس النتيجة.

### طيب إيه الفرق بين share و shareReplay؟

### share

ده بيشترك في الـObservable الأصلي ويشترك فيه كل المشتركين، بس المشكلة إنه ما بيحتفظش بالقيم اللي طلعت. يعني لو واحد اشترك متأخر، مش هيشوف القيم اللي طلعت قبل ما يشترك.

### shareReplay

هنا بقى، ده بيشتغل زي share بس بميزة إضافية، إنه بيحتفظ بعدد معين من القيم اللي طلعت، عشان لو مشترك جديد اشترك متأخر، يقدر يشوف القيم اللي طلعت قبل كده. يعني بيعيد إرسال القيم للمشتركين الجدد.

#### 💡 مثال

 <div dir="auto" align="left">

```typescript
import { HttpClient } from "@angular/common/http";
import { Component, OnInit } from "@angular/core";
import { shareReplay } from "rxjs/operators";

@Component({
  selector: "app-user",
  template: `
    <h2>User Information</h2>
    <div *ngIf="userData">
      <p>Name: {{ userData.name }}</p>
      <p>Email: {{ userData.email }}</p>
    </div>
  `,
})
export class UserComponent implements OnInit {
  userData: any;

  constructor(private http: HttpClient) {}

  ngOnInit() {
    const userObservable = this.http
      .get("https://jsonplaceholder.typicode.com/users/1")
      .pipe(
        shareReplay(1) // Replay the last emitted value for any new subscribers
      );

    // First subscriber
    userObservable.subscribe((data) => {
      console.log("Subscriber 1 received data:", data);
      this.userData = data;
    });

    // Second subscriber
    userObservable.subscribe((data) => {
      console.log("Subscriber 2 received data:", data);
    });
  }
}
```

</div>
</div>
<hr/>
## Describe the types of forms created in Angular application?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
الإجابة: فيه نوعين أساسيين من الفورم في Angular

### Reactive Forms

وده معناه إنك بتتحكم في الفورم من خلال كود الـ TypeScript بدل الـ HTML.
الفورم دي مناسبة جدًا لو عايز تعمل فورم معقدة أو فيها عناصر كتير، وبتقدر تتحكم في التحقق من البيانات (validation) بشكل أدق.

#### الأنواع الرئيسية اللي بتستخدمها في النوع ده هي:

##### FormControl

ده بيعمل عنصر تحكم واحد في الفورم (زي input واحد).

##### FormGroup

ده بيجمع مجموعة من عناصر التحكم (مثلاً inputs متعددة).

##### FormArray

ده بيعمل لك عناصر تحكم ديناميكية يعني ممكن تزود أو تقلل منهم زي ما تحب.

##### FormBuilder

بيسهل عليك عملية إنشاء الـ FormControl وFormGroup وFormArray بطريقة أسرع وبكود أقل.

### Template-Driven Forms

النوع ده بيستخدم أكتر مع الفورم البسيطة زي فورم تسجيل دخول  
هنا التحكم في الفورم بيكون عن طريق الـ HTML باستخدام ديركتيفات (Directives)، وده أسهل لكن أقل تحكم مقارنة بالـ Reactive Forms.

### الأدوات الرئيسية اللي بنستخدمها هنا:

##### NgModel

بتتابع تغييرات القيم في عناصر الفورم زي الـ input وبتتعامل مع التحقق من المدخلات.

##### NgForm

دي بتربط نفسها بالفورم كله وبتتابع القيم الكلية وحالة التحقق للفورم كله.

##### NgModelGroup

دي بتتعامل مع جزء معين من الفورم وتتحقق من البيانات فيه بشكل منفصل عن باقي الفورم.

##### 💡 يعني ببساطة

لو الفورم بتاعتك بسيطة وعايز تعملها بسرعة، استخدم Template-Driven Forms.
لو الفورم معقدة وعايز تحكم أكتر في البيانات والتحقق منها، استخدم Reactive Forms.

</div>
<hr/>
## How will you create reactive form in Angular?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
أول حاجة، لازم تعمل import لـ ReactiveFormsModule. في ملف الـ TypeScript (TS)، بتعمل FormGroup باستخدام الميثود FormBuilder.group وتبدأ تجمّع شوية form controls. وكمان هتعمل function اللي هتشتغل لما الفورم يتعمله submit.

<div dir="auto" align="left">

```typescript
userForm = this.formBuilder.group({
   name: ['', Validators.required ],
   pwd: ['', Validators.required ],
});

onFormSubmit() {
   console.log(this.userForm.value);
}

```

</div>

في ملف الـ HTML، هتعمل form فيه form controls. اربط الـ FormGroup في الـ <form> باستخدام الـ directive formGroup. وكمان اربط كل form control باستخدام الـ directive formControlName.

<div dir="auto" align="left">

```HTML
<form [formGroup]="userForm" (ngSubmit)="onFormSubmit()">
   <p>Username: <input formControlName="empId"></p>
   <p>Password: <input type="password" formControlName="empId"></p>
   <button>Submit</button>
</form>

```

</div>
لما تدوس على الزرار (Submit)، الفورم هيعمل submit والـ function onFormSubmit هتشتغل علشان تعرض القيم بتاعت الفورم في الـ console.

</div>
<hr/>

## How will you create template-driven form in Angular?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
أول حاجة، لازم تعمل import لـ FormsModule. بتربط الـ ngForm في الـ <form> element. كل عناصر الفورم لازم تستخدم name و ngModel وأي validation attributes لو موجودة. في ملف الـ TypeScript (TS)، بتعمل method عشان تعمل submit للفورم وبتربط الميثود دي بالـ ngSubmit event.
<div dir="auto" align="left">

```HTML
<form #userForm="ngForm" (ngSubmit)="onFormSubmit(userForm)">
   <input name="username" ngModel required>
   <input type="password" name="pwd" ngModel required>
   <button>Submit</button>
</form>


```

</div>
<div dir="auto" align="left">

```typescript
onFormSubmit(form: NgForm) {
   console.log(form.value);
}
```

</div>
</div>
<hr/>

## Explain FormControl?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
ال FormControl في Angular بيُستخدم عشان تتحكم في الـ input أو أي عنصر معين في الـ forms. يعني ببساطة، بيكون مسؤول عن القيمة اللي المستخدم بيدخلها، وحالة الـ validation (يعني هل الإدخال صحيح ولا لأ)، وأي errors ممكن تحصل.

لما بتعمل form، بتحتاج تتابع البيانات اللي المستخدم بيدخلها وتتأكد إنها صح عن طريق الـ validation، زي مثلًا إنها تكون إيميل صحيح، أرقام معينة، أو حتى قيم مش فاضية. هنا بييجي دور الـ FormControl، اللي بيساعدك تتابع وتحكم في كل الحاجات دي.

<div dir="auto" align="left">

```typescript
const control = new FormControl("initial value", Validators.required);
```

</div>
في المثال ده، عملنا FormControl بالقيمة الافتراضية 'initial value'، وضفنا Validator بيقول إن الإدخال لازم يكون مطلوب (يعني ميكونش فاضي).

#### أهم خصائص FormControl

###### value

دي القيمة اللي المستخدم دخلها حاليًا.

###### valid

ده بيحدد إذا كان الإدخال صحيح ولا لأ.

###### invalid

ده بيحدد إذا كان في أخطاء ولا لأ.

###### pristine

لو المستخدم ما عدلش في الإدخال، بتبقى true.

###### dirty

لو المستخدم غيّر في الإدخال، بتبقى true.

</div>
<hr/>

## Explain FormGroup?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>

ال FormGroup في Angular بيُستخدم عشان يجمع مجموعة من الـ FormControls في نموذج واحد. يعني لو عندك فورم فيه أكتر من input (زي اسم، إيميل، وكلمة مرور)، تقدر تجمعهم كلهم في FormGroup عشان تتحكم فيهم كلهم مع بعض.

الفكرة ببساطة إنك بتتعامل مع الفورم ككل، بدل ما تتعامل مع كل (input) لوحده. بتقدر تتابع الـ validation والحالة بتاعة كل جوا المجموعة (group).

<div dir="auto" align="left">

```typescript
const form = new FormGroup({
  name: new FormControl(""),
  email: new FormControl(""),
  password: new FormControl(""),
});
```

</div>

### الخصائص المهمة بتاعة FormGroup

###### controls

دي بترجعلك كل الـ FormControls اللي جوه المجموعة.

###### value

بترجع القيم بتاعة كل الحقول في صورة object.

###### valid

لو كل الـ FormControls جوا المجموعة صالحة (valid)، بتكون true.

###### invalid

لو فيه أي input (input) في المجموعة مش صالح، بتكون true.

###### pristine

بتكون true لو مفيش أي تعديل حصل في أي input.

###### dirty

بتكون true لو حصل تعديل في أي input.

</div>
<hr/>

## Explain FormArray?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
ال FormArray في Angular بيُستخدم عشان تدير مجموعة من الـ FormControls أو الـ FormGroups جوا (form). الفكرة إنك تقدر تعمل array  من inputs اللي ممكن تضيفها أو تشيلها بشكل ديناميكي على حسب احتياجاتك.

يعني مثلًا لو عندك form فيه أكتر من input والـ input ده ممكن يتكرر زي مثلًا لما المستخدم يضيف أكتر من عنوان بريد إلكتروني أو أكتر من رقم تليفون، هنا بتستخدم FormArray عشان تقدر تضيف الـ inputs دي وتتحكم فيها.

<div dir="auto" align="left">

```typescript
const formArray = new FormArray([new FormControl(""), new FormControl("")]);
```

</div>

### التعامل مع FormArray

ممكن تضيف FormControl جديد في الـ array باستخدام push

<div dir="auto" align="left">

```typescript
formArray.push(new FormControl(""));
```

</div>
وممكن تشيل FormControl باستخدام removeAt
<div dir="auto" align="left">

```typescript
formArray.removeAt(0);
```

</div>
تقدر كمان تتعامل مع الـ FormArray زي ما بتتعامل مع الـ FormGroup أو الـ FormControl من ناحية التحقق (validation) والحالة (status) والقيم (values).

<div dir="auto" align="left">

```typescript
const formArray = new FormArray([
  new FormControl("", Validators.required),
  new FormControl("", Validators.email),
]);
```

</div>
</div>

## Explain FormRecord?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>

الـ FormRecord في Angular شبه الـ FormGroup، بس الفرق إنه بيتعامل مع مجموعة من الـ FormControl اللي كلهم من نفس نوع القيمة. يعني، الـ FormRecord بيتتبع القيمة وحالة الـ validity لمجموعة من الـ FormControl اللي ليهم نفس نوع البيانات.

الـ FormRecord مفيد جدًا لما تحب تبني form بشكل ديناميكي. تقدر تضيف form controls باستخدام addControl، وتشيلهم بـ removeControl، وهكذا.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "my-app",
  standalone: true,
  imports: [CommonModule, ReactiveFormsModule],
  templateUrl: "./my.component.html",
})
export class MyComponent implements OnInit {
  userForm!: FormRecord;
  formData = [
    { title: "Name", key: "name" },
    { title: "City", key: "city" },
  ];
  ngOnInit() {
    this.userForm = new FormRecord<FormControl<string | null>>({});
    this.formData.forEach((data) =>
      this.userForm.addControl(data.key, new FormControl())
    );
  }
  onFormSubmit() {
    console.log(this.userForm.value);
  }
}
```

</div>

<div dir="auto" align="left">

```HTML
<form [formGroup]="userForm" (ngSubmit)="onFormSubmit()">
    <div *ngFor="let data of formData">
        {{data.title}}: <input [formControlName]="data.key"><br />
    </div>
    <button>Submit</button>
</form>

```

</div>
في الكود ده، إحنا بنستخدم FormRecord عشان ننشئ form ديناميكي. عندنا formData فيها الحقول اللي عايزينها في الـ form. في ngOnInit، بنعمل instance من الـ FormRecord وبنضيف الـ form controls باستخدام addControl.

لما المستخدم يضغط على زرار "Submit"، الـ onFormSubmit هتتنفذ وهتطبع قيم الـ form في الـ console.

بكده، تقدر تستخدم FormRecord عشان تبني forms ديناميكية بسهولة في Angular، وتتحكم في القيم والـ validation بتاعتها.

</div>
<hr/>

## How will you use valueChanges?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
الـ valueChanges ده Observable في Angular، بيعمل emit للقيمة بتاعة الـ form control أو الـ form group لما قيمتها بتتغير، سواء المستخدم غيرها أو برمجياً.

يعني لو المستخدم عدل في الـ input، الـ valueChanges هيشتغل وهيعمل subscribe لأي function انت محددها. وكمان لو انت برمجياً غيرت القيمة أو عملت enable/disable للـ control، برضه الـ valueChanges هيعمل emit.

تقدر تستخدمه مع FormControl، FormGroup، وFormArray.

<div dir="auto" align="left">

```typescript

studentForm = this.formBuilder.group({
  stdName: ['', [ Validators.required ]],
});

this.studentForm.get('stdName').valueChanges.subscribe(
  stdName => console.log(stdName);
);

this.studentForm.valueChanges.subscribe(student => {
  console.log(student.stdName);
});


```

</div>
في المثال ده، احنا عملنا subscribe للـ valueChanges بتاع الـ stdName control، فأي تغيير في القيمة هيطبع القيمة الجديدة في الـ console. وكمان عملنا subscribe للـ valueChanges بتاع الـ studentForm كله، فأي تغيير في أي control جوه الـ form هيطبع الـ student.stdName الجديدة.
</div>
<hr/>

## How will you use statusChanges?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
الـ statusChanges ده بيكون observable، يعني بيراقب أي تغيير في حالة الـ validation الخاصة بأي FormControl أو FormGroup أو FormArray. يعني كل ما يحصل إعادة حساب للـ validation، الـ statusChanges بيعمل emit بالقيمة الجديدة للحالة سواء كانت valid أو invalid.
<div dir="auto" align="left">

```typescript
studentForm = this.formBuilder.group({
  stdName: ['', [ Validators.required ]],
});
this.studentForm.get('stdName').statusChanges.subscribe(
  status => console.log(status);
);
this.studentForm.statusChanges.subscribe(status => {
	console.log(status);
});

```

</div>
هنا إحنا عاملين FormGroup اسمه studentForm وجواه FormControl اسمه stdName والـ validation بتاعه إنه required (يعني لازم المستخدم يدخل القيمة).

أول حاجة: بنستخدم statusChanges عشان نراقب حالة الـ stdName. لو حصل أي تغيير في الـ validation (يعني مثلاً المستخدم يدخل قيمة أو يسيبها فاضية)، هيتعمل emit للحالة سواء كانت valid أو invalid.

تاني حاجة: بنراقب حالة الـ FormGroup كله عن طريق الـ statusChanges بتاع الـ studentForm. وده بيعرض لنا حالة النموذج بالكامل.

يعني باختصار، الـ statusChanges ده بيساعدك تعرف إمتى الـ form أو الـ input بيغير حالته من صالح (valid) أو غير صالح (invalid) وتقدر تتصرف بناءً على الحالة دي.

</div>
<hr/>

## What is difference between setValue() and patchValue()?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
في Angular، الفرق بين setValue و patchValue بيظهر لما تيجي تتعامل مع الفورم وتحدث القيم اللي فيه.

setValue بيطلب منك تدي كل القيم لكل الـ controls اللي في الـ form أو الـ FormGroup. يعني لو الفورم بتاعك فيه 3 حقول، وانت استخدمت setValue، لازم تدي قيم للـ 3 حقول دول. لو نسيت أي حقل، هيطلعلك error.

patchValue بيبقى مرن أكتر. مش شرط تدي قيم لكل الـ controls. يعني ممكن تحدث جزء من الفورم بس من غير ما يحصل أي مشكلة. فلو الفورم فيه 3 حقول، وانت استخدمت patchValue لحقلين بس، الحقل التالت هيفضل زي ما هو من غير مشاكل.

<div dir="auto" align="left">

```typescript
form.setValue({
  name: "Abdelrahman",
  email: "abdelrahman@example.com",
  age: 30,
});

form.patchValue({
  name: "Abdelrahman",
  email: "abdelrahman@example.com",
});
```

</div>
في المثال الأول، لازم تدّي قيم لكل الـ inputs (name، email، و age)، لكن في المثال التاني، استخدمنا patchValue عشان نحدث بس الـ name والـ email من غير ما نضطر نحط قيمة للـ age.

باختصار:

setValue لازم تدي كل القيم لكل الـ inputs.
patchValue تقدر تدي قيم لجزء من الـ inputs بس.

</div>
<hr/>

## How will you add and remove controls on FormGroup dynamically?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
علشان تضيف وتزيل controls في FormGroup بشكل ديناميكي، بتستخدم الميثودز addControl وremoveControl.
<div dir="auto" align="left">

```typescript
addControl(name: string, control: AbstractControl)

```

</div>
<div dir="auto" align="left">

```typescript
this.customerForm.addControl(
  "city",
  this.formBuilder.control("", [Validators.required])
);
```

</div>
في المثال ده، بنضيف control اسمه 'city' للـ FormGroup بتاعنا.

<div dir="auto" align="left">

```typescript
removeControl(name: string)
```

</div>
<div dir="auto" align="left">

```typescript
this.customerForm.removeControl("city");
```

</div>
وده بيشيل الـ control اللي اسمه 'city' من الـ FormGroup.

#### 💡 مثال

هنفترض إن عندنا FormGroup اسمه customerForm، وعايزين نضيف حقل (control) اسمه "city" ونزيله بعد كده.

#### الخطوات:

أول حاجة هننشئ FormGroup.
هنستخدم addControl عشان نضيف الـ control.
بعد كده، لو عايزين نزيل الـ control، هنستخدم removeControl.

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";
import { FormBuilder, FormGroup, Validators } from "@angular/forms";

@Component({
  selector: "app-customer-form",
  templateUrl: "./customer-form.component.html",
})
export class CustomerFormComponent {
  customerForm: FormGroup;

  constructor(private formBuilder: FormBuilder) {
    this.customerForm = this.formBuilder.group({
      name: ["", Validators.required],
    });
  }

  addCityControl() {
    this.customerForm.addControl(
      "city",
      this.formBuilder.control("", [Validators.required])
    );
  }

  removeCityControl() {
    this.customerForm.removeControl("city");
  }
}
```

HTML

<div dir="auto" align="left">

```HTML
<form [formGroup]="customerForm">
  <label for="name">Name:</label>
  <input id="name" formControlName="name" />

  <div *ngIf="customerForm.get('city')">
    <label for="city">City:</label>
    <input id="city" formControlName="city" />
  </div>

  <button type="button" (click)="addCityControl()">Add City</button>
  <button type="button" (click)="removeCityControl()">Remove City</button>
</form>

```

</div>
</div>
عند الضغط على زرار "Add City"، بيتم إضافة حقل city.
عند الضغط على زرار "Remove City"، بيتم إزالة حقل city.
الطريقة دي بتخليك تتحكم في الحقول الديناميكية في النموذج بتاعك بكل سهولة.
</div>
<hr/>

## What is difference between (ngModelChange) and (change)?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
ببساطة، الفرق بين (ngModelChange) و (change) هو إن كل واحد منهم بيشتغل في مكان مختلف ولغرض مختلف:

الngModelChange ده بيشتغل مع حاجة اسمها ngModel، وده حاجة خاصة بـ Angular. يعني لو عندك input في النموذج بتاعك (form)، وعايز تتابع التغير اللي بيحصل في القيمة بتاعته بشكل مباشر، بتستخدم ngModelChange. كل ما القيمة تتغير جوه ngModel، الحدث ده بيشتغل وبيجيبلك القيمة الجديدة على طول باستخدام حاجة اسمها $event.

<div dir="auto" align="left">

```HTML
<input [(ngModel)]="name" (ngModelChange)="onNameChange($event)">
```

</div>
هنا كل ما المستخدم يغير الاسم في input ده، الحدث ngModelChange هيشتغل وهيجيبلك القيمة الجديدة اللي دخلها المستخدم.

الchange ده عبارة عن DOM event عادي خاص بـ HTML، وبيشتغل لما يحصل تغيير في القيمة بتاعت العنصر (زي input أو select)، لكنه بيتفاعل بس لما المستخدم يخلص التغيير (زي لما يكتب حاجة ويضغط Enter أو يطلع من input).

<div dir="auto" align="left">

```HTML
<input (change)="onInputChange($event)">
```

</div>
هنا change بيشتغل بس لما المستخدم يغير القيمة ويطلع من الـ input، وبيجيبلك القيمة من خلال event.target.value.

### الفرق الرئيسي

#### ngModelChange

بيراقب التغيير بشكل فوري جوه ngModel وبيجيبلك القيمة مباشرة من $event.

#### change

بيتفاعل مع التغيير في HTML elements العادية بعد ما المستخدم يخلص التغيير، وبتجيب القيمة باستخدام event.target.value.
يعني لو عايز تعرف التغيير أول ما يحصل في الـ input وتتحكم فيه، استخدم ngModelChange. لكن لو عايز تعرف التغيير بعد ما المستخدم يخلص تعديل القيمة، استخدم change.

</div>
<hr/>

## How to add async validation in FormControl?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
لو عايز تضيف async validation في FormControl، الموضوع بسيط

تقدر تمرر array من async validators كـ argument تالت في FormControl. مثال:

<div dir="auto" align="left">

```typescript
customerForm = this.formBuilder.group({
  customerName: ["", [Validators.required], [myCustomAsyncValidator()]],
});
```

</div>
الطريقة التانية، ممكن تمرر object كـ argument تاني يحتوي على خصائص زي validators و asyncValidators. مثال:

<div dir="auto" align="left">

```typescript
customerForm = this.formBuilder.group({
  customerName: [
    "",
    {
      validators: [Validators.required],
      asyncValidators: [myCustomAsyncValidator()],
    },
  ],
});
```

</div>

#### 💡 مثال

هديك مثال واقعي لموقف ممكن تستخدم فيه async validation في FormControl. خلينا نفترض إنك بتعمل form للمستخدم عشان يسجل بياناته، ومن ضمن البيانات دي اسم المستخدم (username)، ولازم تتأكد إن الاسم ده مش متسجل قبل كده في قاعدة البيانات (دي عملية بتحتاج تحقق من قاعدة البيانات، وبالتالي هتكون async).

#### create a service

<div dir="auto" align="left">

```typescript
@Injectable({ providedIn: "root" })
export class UserService {
  constructor(private http: HttpClient) {}

  checkUsername(username: string): Observable<boolean> {
    return this.http.get<boolean>(
      `/api/users/check-username?username=${username}`
    );
  }
}
```

</div>

#### UserFormComponent

<div dir="auto" align="left">

```typescript
export class UserFormComponent {
  constructor(
    private formBuilder: FormBuilder,
    private userService: UserService
  ) {}

  customerForm = this.formBuilder.group({
    username: ["", [Validators.required], [this.checkUsernameAvailability()]],
  });

  checkUsernameAvailability(): AsyncValidatorFn {
    return (control: AbstractControl): Observable<ValidationErrors | null> => {
      return this.userService.checkUsername(control.value).pipe(
        map((isAvailable) => {
          return isAvailable ? null : { usernameTaken: true };
        })
      );
    };
  }
}
```

</div>

#### template

<div dir="auto" align="left">

```HTML
<form [formGroup]="customerForm" (ngSubmit)="onSubmit()">
  <label for="username">Username</label>
  <input id="username" formControlName="username">

  <div *ngIf="customerForm.get('username').hasError('usernameTaken')">
    This username is already taken.
  </div>

  <button type="submit" [disabled]="customerForm.invalid">Submit</button>
</form>

```

</div>
دي ببساطة الطريقتين اللي تقدر تضيف بيهم async validation في FormControl في Angular.
</div>

<hr/>

## How will you validate template-driven form?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
عشان تعمل validation في الفورم اللي معمول بـ template-driven، بتحدد (validation attributes) في الـ form control، وبتستخدم   بـ # عشان تعرض رسائل الخطأ بناءً عليه.

<div dir="auto" align="left">

```HTML
<input name="uname" ngModel required maxlength="20" #usrname="ngModel">
<div *ngIf="usrname.errors?.['required']">
		Enter user name.
</div>
<div *ngIf="usrname.errors?.['maxlength']">
		Maxlength is 20.
</div>
{{usrname.status}}

```

</div>
</div>
<hr/>

## How will you perform two-way binding using ngModel?

[⬆️ Back to Top](#top)

<div dir="auto" align='right'>
عشان تعمل two-way binding باستخدام ngModel، بتستخدم الأقواس المربعة والعادية مع بعض [()] حوالين الـ ngModel كده: [(ngModel)]. الطريقة دي بتسمح بإرسال البيانات من الـ component للـ view target، وفي نفس الوقت من الـ view target للـ component.
<div dir="auto" align="left">

```typescript
message = "Hello World!";
```

</div>

<div dir="auto" align="left">

```HTML
<input [(ngModel)]="message">

{{message}}

```

</div>
في المثال ده، أي تعديل على الإدخال اللي في الـ input هيتم تحديثه فورًا في المتغير message اللي في الـ component، والعكس صحيح. يعني أي تغيير في المتغير هيظهر برضه في الـ input.

</div>
