## When (Not) to use Effects in Angular — and what to do instead

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### إمتى تستخدم effects في Angular — وإمتى ما تستخدمهاش وإيه البدائل؟

الEffects أداة قوية في Angular، لكن مش لازم تستخدمها في كل الحالات.

في حالات معينة، استخدام effects بيكون مناسب، وفي حالات تانية ممكن يسبب تعقيد بدون فائدة حقيقية.

خلينا نستعرض إمتى نستخدمها وإمتى لأ، وإيه البدائل المتاحة.

الEffects مفيدة بشكل أساسي للتعامل مع الحاجات اللي مش بتقدر تعرضها باستخدام (data binding).

في Angular، ربط البيانات (data binding) هو الطريقة اللي تقدر بيها تعرض أو تربط البيانات بالواجهة (UI) بسهولة، زي لما تظهر قيمة في مكان معين أو تربط زرار بوظيفة. لكن في بعض الحالات، ربط البيانات ما بيكونش كافي أو ما ينفعش أصلاً بسبب احتياجك لتفاعل مباشر أكتر.

### أمثلة للاستخدامات الرئيسية لـEffects

#### 1) Logging

#### 2) Painting on a Canvas

#### 3) Custom DOM behavior

### Keep Auto-Tracking in Mind

في Angular، فيه حاجة اسمها (auto-tracking)، ودي شغالة مع computed و**effects**. يعني Angular بتراقب أي قيمة (Signal) حتى لو مش مستخدمة بشكل مباشر في الكود، لكن طالما فيه تأثير عليها بشكل غير مباشر.

### مثال للتوضيح

<div dir="auto" align="left">

```typescript

error = signal(null); // تبدأ بقيمة null أو undefined

effect(() => {
  this.logError();
});

logError(): void {
  const error = this.error();
  if (error) {
    console.error(error);
  }
}
```

</div>

هنا عندنا effect بيشغل logError، وداخل logError بنستخدم قيمة error. مع إن error مش موجودة مباشرة في effect،

الAngular عارفة إن فيه علاقة غير مباشرة بينها وبين effect. فلو حصل تغيير في error، effect هيشتغل تاني تلقائي.

### ليه الموضوع ده مهم؟

التصميم ده بيأكد إن Effects في Angular معمولة بشكل أساسي للتعامل مع عرض البيانات (rendering).

أي قيمة بيتم التعامل معاها أثناء العرض، Angular بتراقبها تلقائي، ولو حصل أي تغيير فيها، بيتم تحديث العرض مباشرة.

</div>

<!-- ## Angular Change Detection - How Does It Really Work?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في أنجولار، عندنا حاجة اسمها "Change Detection" ، اللي بتخلي أنجولار يقدر يعرف لو في أي بيانات اتغيرت في الكمبوننت، ويعيد تحديث UI أوتوماتيك عشان يظهر التغيير ده.

السؤال هنا، إزاي بيعمل كده بعد أحداث زي ضغطة زر، اللي ممكن تحصل في أي حتة في الصفحة؟

### change detection mechanism work

اللي بيحصل هو إن أنجولار بيبص على كل متغير مستخدم في الـHTML (الـTemplate)، زي لما تكتب `{{ user.name }}` أو تحط حاجة زي `[value]="counter"`، وبيقارن القيمة الحالية للمتغير ده بالقيمة اللي كانت موجودة قبل كده.

### الخطوات

1- أنجولار بيمر على كل متغير جوه الـTemplate عشان يشوف إذا حصل فيه تغيير ولا لأ.

2- بيقارن القيمة الجديدة بالقيمة القديمة. لو لقى إنهم مختلفين، بيقول "أيوة، حصل تغيير"، وبيخلي متغير داخلي اسمه isChanged يبقى true.

3- أنجولار بيستخدم دالة اسمها looseNotIdentical، ودي بتقارن بين القيم بطريقة مشابهة للمقارنة ===، لكنها بتتجنب مشاكل معينة زي NaN (عشان لو عندك NaN، جافاسكريبت بتتعامل معاه بشكل مختلف شوية).

4- لو isChanged بقت true، أنجولار بيروح يعمل تحديث للجزء ده في الواجهة عشان يظهر التغييرات.

![Angular component tree and its change detector (CD)](https://mokkapps.twic.pics/mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/cd-cycle_wfdcsk.gif)

الصورة بتوضح شجرة الكومبوننتات (Component Tree) في Angular، ولكل كومبوننت فيه (Change Detector) خاص بيه بيتعمل أثناء عملية تشغيل التطبيق لأول مرة

والchange detector بيعمل نفس الخطوات السابقة

### ننتقل لنقطة تانية وهي Zone.js

#### يعني إيه Zone.js؟

الZone.js هو مكتبة في Angular بتعمل حاجة زي "مراقبة" للعمليات غير المتزامنة، زي لما تعمل استدعاء API أو تعدادات زمنية (timers) زي setTimeout أو setInterval.

المكتبة دي بتسمح لـ Angular إنه "يتصنت" على العمليات دي، وده بيساعده إنه يقدر يكتشف التغييرات اللي بتحصل في البيانات بتاعت التطبيق لما أي من العمليات دي تتنفذ.

#### إيه فايدة المراحل في Zone.js؟

الـ Zone بتعدي بمراحل معينة علشان Angular يقدر يتحكم في متى يشغل آلية اكتشاف التغييرات:

1- المرحلة المستقرة (Stable): التطبيق بيكون شغال عادي من غير أي عمليات غير متزامنة شغالة، يعني التطبيق هادي.

2- المرحلة غير المستقرة (Unstable): لو حصلت عملية غير متزامنة (زي طلب HTTP أو حدث كليك على زر)، الـ Zone بتتحول لغير مستقرة، وبتبدأ تراقب العمليات دي لحد ما تخلص.

3- المرحلة المستقرة تاني: بعد ما تخلص العمليات دي، الـ Zone بترجع مستقره، ووقتها Angular بيبدأ عملية change detection علشان يحدث واجهة المستخدم لو في أي تغيير حصل.

اللي بيحصل إن Angular عامل منطقة خاصة بيه اسمها NgZone، ودي بتمثل المكان اللي Angular بيقدر يشغل فيه change detection على العمليات غير المتزامنة اللي بتحصل فيه. يعني مثلاً:

لما يحصل حدث في المتصفح زي ضغطة زر (click) أو كتابة حرف (keyup).
لما يستعمل setTimeout أو setInterval.
لما تعمل طلب HTTP عن طريق XMLHttpRequest.
أي حاجة بتحصل في NgZone دي هتشغل change detection وتخلي Angular يحدث UI لو حصل أي تغيير في البيانات.

### Change Detection Strategies

Angular provides two strategies to run change detections

#### 🔴 Default

#### 🔴 OnPush

بشكل افتراضي، Angular بيستخدم ChangeDetectionStrategy.Default، واللي معناها إن كل مرة يحصل حدث ممكن يؤثر على البيانات، زي حدث من المستخدم، أو مؤقت (timer)، أو طلب HTTP (XHR)، أو promise وغيره، Angular بيمر على كل الكومبوننتات في شجرة الكومبوننتات من فوق لتحت.

العملية دي بيسموها الفحص المتكرر (dirty checking)، وده لأنه Angular بيتأكد من كل كومبوننت من غير ما يفترض إن فيه علاقات معينة أو اعتماد على عناصر تانية جواه.

![Angular component tree and its change detector (CD)](https://mokkapps.twic.pics/mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/cd-cycle_wfdcsk.gif)

الطريقة دي محافظة أكتر، لأنها بتفحص كل الكومبوننتات وتفترض إنها ممكن تكون اتغيرت، لكن ده ممكن يأثر سلبًا على أداء التطبيق، خصوصًا في التطبيقات الكبيرة اللي فيها عدد كبير من الكومبوننتات. فحص كل الكومبوننتات كل مرة بيكون بطيء وممكن يقلل سرعة التطبيق مع زيادة الحجم والتعقيد.

### استراتيجية OnPush لاكتشاف التغييرات في Angular

علشان نستخدم استراتيجية ChangeDetectionStrategy.OnPush، ممكن نضيف خاصية changeDetection في الديكوريتور بتاع الكومبوننت بالشكل ده:

<div dir="auto" align="left">

```typescript
@Component({
    selector: 'hero-card',
    changeDetection: ChangeDetectionStrategy.OnPush,
    template: `...`
})
export class HeroCard {
    ...
}
```

</div>

![Angular component tree and its change detector (CD)](https://mokkapps.twic.pics/mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/cd-on-push-cycle_te8dai.gif)

### إيه اللي بتعمله استراتيجية OnPush؟

استراتيجية OnPush بتديك ميزة كبيرة في تحسين الأداء، لأنها بتقلل الفحوصات اللي Angular بيعملها. لما نستخدم OnPush، Angular مش هيفحص الكومبوننت ده ولا أي كومبوننت فرعي جواه إلا في حالات معينة، زي:

<div dir="auto" align="left">

### Using this strategy, Angular knows that the component only needs to be updated if:

- the input reference has changed
- the component or one of its children triggers an event handler
- change detection is triggered manually
- an observable linked to the template via the async pipe emits a new value

### Input Reference Changes

</div>

لما تستخدم استراتيجية OnPush في Angular، فآلية changeDetection بتشتغل بس لما يتغير refrence.

### يعني إيه "تغيير الrefrence "؟

#### في جافاسكريبت، عندنا نوعين من البيانات

ال(Primitive types): زي الأرقام (numbers)، النصوص (strings)، القيم المنطقية (booleans)، null، وundefined. لما تعدل قيمتها، بيعتبر ده تغيير، وده معناه إن changeDetection هيشتغل تلقائيًا.

ال(Objects) و (Arrays): هنا الموضوع مختلف. لو عدلت خاصية جوا object أو عنصر جوا array الrefrence بتاعهم مبيختلفش، يعني Angular مش هيشغل changeDetection لأن refrence ثابت.

علشان االchangeDetection يشتغل، لازم تبعت object جديد أو array جديدة بreference جديد.

### مثال توضيحي

تخيل عندك كومبوننت بياخد بيانات كـ Input@ بالطريقة دي

<div dir="auto" align="left">

```typescript
@Component({
  selector: "example-component",
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `...`,
})
export class ExampleComponent {
  @Input() data: any;
}
```

</div>

🔴 السيناريو الأول:

لو البيانات كانت رقم (مثلاً data = 5) وعدلتها إلى data = 6، الAngular هيلاحظ التغيير لأن Primitive types بيتغير بالقيمة، وchangeDetection هيشتغل.

🔴 السيناريو الثاني

تعديل object أو array

<div dir="auto" align="left">

```typescript
this.data = { name: "John" };
```

</div>
لو عدلت الobject نفسه:
<div dir="auto" align="left">

```typescript
this.data.name = "Doe";
```

</div>
في الحالة دي، الrefrence ثابت، فـ Angular مش هيشغل Change Detection، ومش هيلاحظ التغيير، لأنه object نفسه لسه بنفس الrefrence.

### إزاي تخلي Angular يلاحظ التغيير؟

لو عايز الـ Change Detector يشتغل، لازم تعمل Object أو Array جديد بrefrence جديد، كده Angular هيقدر يشغل الـ Change Detector ويلاحظ التغيير.

<div dir="auto" align="left">

```typescript
this.data = { ...this.data, name: "Doe" };
```

</div>
 ✅في الحالة دي، Angular هيلاحظ التغيير لأنك عملت object جديد وrefrence جديد.

 ### Event Handler Is Triggered

 خد بالك ان  في بعض الحالات زي setTimeout وPromise واشتراكات RxJS، التغييرات بتحصل بشكل "خارج" عن نطاق الكشف التقليدي. وبالتالي، الـOnPush مش بيكتشف التغييرات دي تلقائيًا.

 لما بنستخدم setTimeout أو setInterval في الـcomponent، الكود بينفذ بعد وقت معين، لكن ده بيحصل "خارج" نطاق Angular change detection.

  يعني Angular مش عارف إن فيه تغيير حصل ومش هيعرف يظهره مباشرة على الشاشة لأن OnPush مش بيشوف التغييرات دي.

  #### طيب إيه الحل عشان نخلي التغييرات تظهر؟
  استخدام ```ChangeDetectorRef.markForCheck``` اللي بيقول لـAngular يشوف التغييرات حتى لو جت من حاجات زي setTimeout أو Promise

  #### مثال
  <div dir="auto" align="left">

```typescript
import { Component, ChangeDetectionStrategy, ChangeDetectorRef } from '@angular/core';

@Component({
  selector: 'app-hero-card-on-push',
  template: `
    <div>
      <p>Age: {{ age }}</p>
      <button (click)="changeAge()">Change Age with setTimeout</button>
    </div>
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class HeroCardOnPushComponent {
  age = 25;

  constructor(private cdr: ChangeDetectorRef) {}

  changeAge() {
    setTimeout(() => {
      this.age = 30;  // غيرنا العمر هنا
      this.cdr.markForCheck(); // بنستخدم markForCheck عشان نقول لـAngular يشوف التغيير
    }, 1000);
  }
}
```

</div>

 بعد ما نغير age، بنستخدم ```this.cdr.markForCheck``` عشان نطلب من Angular إنه يعمل كشف عن التغييرات ويحدث الشاشة. بدون ```markForCheck```، التغيير في age مش هيظهر لأننا بنستخدم OnPush.

 #### ليه نستخدم markForCheck؟
الmarkForCheck بيقول لـAngular إن فيه تغيير حصل وبيحتاج يتشاف حتى لو كان جاي من setTimeout أو Promise أو حاجة تانية خارج نطاق الكشف التقليدي للتغييرات.

### Trigger Change Detection Manually

#### فهم طرق تشغيل الكشف عن التغييرات يدويًا في Angular
في Angular، فيه ٣ طرق أساسية ممكن تستخدمها عشان تشغل الكشف عن التغييرات يدويًا، وده مفيد لما تكون محتاج تحديث الـcomponent أو التطبيق في حالات خاصة، زي ما بيحصل في setTimeout أو Promise، اللي ما بيشغلوش الكشف عن التغييرات بشكل تلقائي

##### 🔴 ١- detectChanges
إيه اللي بيعمله؟
الdetectChanges بتشغل الكشف عن التغييرات للـcomponent الحالي وأي مكونات فرعية ليه.

فين ممكن تستخدمه؟
لما عايز تحدث الـcomponent الحالي فقط بعد ما يحصل تغيير معين من غير ما تعمل تحديث لكل التطبيق.

مثال عملي:

لو عندك component فيه قيمة age بتتغير بعد فترة باستخدام setTimeout، وعايز تشغل الكشف عن التغييرات يدويًا عشان تظهر القيمة الجديدة

<div dir="auto" align="left">

```typescript
import { ChangeDetectorRef } from '@angular/core';

constructor(private cdr: ChangeDetectorRef) {}

changeAge() {
  setTimeout(() => {
    this.age = 30;
    this.cdr.detectChanges();
  }, 1000);
}
```

</div>

##### 🔴 ٢. ApplicationRef.tick

إيه اللي بيعمله؟

الApplicationRef.tick بتشغل الكشف عن التغييرات على مستوى التطبيق بالكامل، يعني بتشيك على كل الـcomponents، وده بيكون تأثيره أوسع من detectChanges.

فين ممكن تستخدمه؟
لو حصل تغيير في جزء معين من التطبيق وعايز تشغل الكشف عن التغييرات في كل components بس نادرًا بنحتاجها لأن تأثيرها على الأداء كبير

##### 🔴 ٣. markForCheck
إيه اللي بيعمله؟

الmarkForCheck ما بيشغّلش الكشف عن التغييرات مباشرةً، لكنه بيوصّل للـOnPush components إنهم يتفحصوا في أقرب دورة كشف تغييرات.

فين ممكن تستخدمه؟
لو فيه تغييرات بتحصل خارج نطاق الكشف عن التغييرات، وعايز تأكد إن component هيعمل فحص ليها في الدورة الجاية.


![Angular component tree and its change detector (CD)](https://mokkapps.twic.pics/mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need/change-detector-ref_j3gyml.jpg)

#### ✅ خلاصة استخدام كل طريقة:
###### detectChanges: لما تحتاج تحديث للـcomponent الحالي وcomponents الفرعية فقط.

###### ApplicationRef.tick: لو عايز تحديث لكل التطبيق مرة واحدة (بيستخدم في حالات نادرة).

###### markForCheck: لما تحتاج تضمن تحديث الـcomponent في الدورة القادمة بدون ما تشغّل الكشف عن التغييرات في الحال.

### Async Pipe

الAsync Pipe هو Pipe جاهز في Angular بيقوم بالاشتراك في الـObservable أو Promise تلقائيًا، وبيرجع آخر قيمة تم إصدارها منه.

 ده بيخليك تستفيد من التحديثات اللي بتحصل في البيانات بدون ما تحتاج تتعامل مع الاشتراكات subscribe بنفسك، وده بيسهل عليك كتابة كود أنظف وأكثر ترتيبًا

#### كيف يعمل Async Pipe داخليًا؟
الAsync Pipe بيستخدم markForCheck عشان يضمن إن التحديثات تظهر حتى لو الـcomponent بيستخدم استراتيجية OnPush.

 في كل مرة الـObservable أو الـPromise يرجع قيمة جديدة، Async Pipe بيستخدم markForCheck عشان يخلي Angular يشوف التغييرات دي ويحدث الـcomponent

 #### لماذا يفضل استخدام Async Pipe؟
التوافق مع الOnPush:  متوافق تلقائيًا مع استراتيجية OnPush، مما يجعله مناسب جدًا لو انتقلنا لاستخدام OnPush في التطبيق.

إدارة الذاكرة: Async Pipe بيلغي الاشتراك تلقائيًا في الـObservable أو الـPromise لما يتم تدمير الـcomponent، وبالتالي بيقلل من مخاطر التسريبات (Memory Leaks).

بساطة الكود: Async Pipe بيقلل من الحاجة لكتابة كود معقد لعملية الاشتراك والإلغاء، مما يجعل الكود أنظف وأقل عرضة للأخطاء.

<div dir="auto" align="left">

```typescript
import { Component } from '@angular/core';
import { Observable, of } from 'rxjs';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class UserComponent {
  user$: Observable<{ name: string }> = of({ name: 'John Doe' });
}
```

</div>
<div dir="auto" align="left">

```HTML
<div *ngIf="user$ | async as user">
  <p>{{ user.name }}</p>
</div>

```

</div>
</div> -->

 <!-- <hr/>
 ## ContentChild and ContentChildren in Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

</div>


<div dir="auto" align="left">

```typescript

```

</div>
<div dir="auto" align="left">

```HTML

```

</div> -->
