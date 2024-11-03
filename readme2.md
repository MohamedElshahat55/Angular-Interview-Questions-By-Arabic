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

<!-- ## A change detection, zone.js, zoneless, local change detection, and signals story

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

الAngular هو إطار عمل بيشتغل بطريقة الـ component-driven، يعني كل حاجة في التطبيق مبنية على مكونات (components). وزي أي إطار عمل تاني، فكرته الأساسية إنه يعرض الداتا للمستخدم ويعمل تحديث للواجهة (view) لما الداتا تتغير.

فكرة كشف التغييرات (change detection) ببساطة هي عملية متابعة التغييرات اللي بتحصل في الداتا، ولما يحصل تغيير، يبتدي يعرضه للمستخدم في الواجهة. يعني لو مثلا عندك اسم بيظهر على الشاشة والمستخدم غيره، Angular بيعمل تحديث تلقائي للعرض عشان يظهر الاسم الجديد.

زمان، Angular كانت بتستخدم حاجة اسمها Zone.js عشان تتتبع التغييرات دي. Zone.js كان مسؤول عن متابعة كل الأحداث اللي بتحصل في التطبيق، زيcilke و (server responses)، ولما يحصل تغيير، بيبدأ عملية كشف التغييرات عشان يحدّث الواجهة.

دلوقتي، في توجه جديد اسمه زونليس (zoneless)، وده يعني إننا بنحاول نبعد عن استخدام Zone.js عشان نخلي الأداء أسرع ونقلل التعقيدات. الفكرة هنا إنك تتابع التغييرات بشكل محلي في كل component لوحده، وده اللي بيسموه الكشف المحلي للتغييرات (local change detection). يعني كل component يتابع الداتا بتاعته بس، من غير ما يدخل Zone.js في كل عملية.

وفي مفهوم جديد ظهر اسمه (signals)، وده عبارة عن طريقة ذكية عشان تعرف Angular إن في حاجة اتغيرت، من غير ما تتابع كل التفاصيل الصغيرة. يعني بدل ما التطبيق كله يبقى بيراقب الداتا طول الوقت، signals هتدي إشارة لما يحصل تغيير، وده يخلي الأداء أحسن والتحميل أسرع.

![A UserCard component that shows user data in the template](https://justangular.com/cd-article/user-card-change.webp)

A UserCard component that shows user data in the template

![Component structure](https://justangular.com/cd-article/component-structure.webp)

### مع الوقت، وإحنا بنبني components أكتر في التطبيق، بنبدأ نركبهم مع بعض ونعمل شجرة من (component tree) زي اللي موضحة في الرسم اللي فوق.

### طيب، إزاي Angular بتعرف إمتى تحدث الUI؟

إزاي بتعرف إن في داتا اتغيرت؟ وإزاي بتعرف إنها محتاجة تشغل كشف التغييرات (change detection)؟

### 🔴 Change detection with synchronous code

خلينا نبدأ بمثال بسيط. عندنا (component) فيه خاصية اسمها `name` ودالة اسمها `changeName`. لما ندوس على الزرار، بنادي دالة `changeName` اللي بتغير قيمة `name`

<div dir="auto" align="left">

```typescript
@Component({
  template: `
    <button (click)="changeName()">Change name</button>
    <p>{{ name }}</p>
  `,
})
export class AppComponent {
  name = "John";

  changeName() {
    this.name = "Jane";
  }
}
```

</div>

لما بندوس على الزرار، changeName بتشتغل وبتغير القيمة بتاعت name من "John" لـ "Jane". لأن Angular بتحاوط كل حاجة بآلية كشف التغييرات، فإحنا نقدر نفترض بأمان إنه بعد تغيير الاسم، Angular هتشغل كود عشان تحدث العرض وتخلي كل حاجة متزامنة (in sync).

مثال للكود اللي Angular ممكن تشغله وراء الكواليس:

تخيل إن Angular شغلت كود زي ده ورا الكواليس:

<div dir="auto" align="left">

```typescript
component.changeName();
angular.runChangeDetection();
```

</div>

ده شغال تمام في الحالة البسيطة دي، عشان كل التغييرات بتحصل في نفس اللحظة (synchronously)، وده بيخلي Angular تشغل كشف التغييرات بدون مشاكل.

لكن في أغلب الوقت، لما بنغير الداتا، الموضوع مش بيحصل بشكل متزامن. غالباً بنبعت طلب HTTP، أو بنعتمد على مؤقتات (timers)، أو بنستنى أحداث تانية تحصل قبل ما نحدث الداتا. وده هنا اللي بيسبب المشاكل!

### فين المشكلة؟

لما يكون التغيير مرتبط بأحداث غير متزامنة (async)، Angular مش هتقدر تعرف لوحدها إن في حاجة اتغيرت. عشان كده بتعتمد على Zone.js (لو مش شغالين بزونليس)، اللي بيراقب الأحداث زي طلبات HTTP أو مؤقتات، وبيخبر Angular لما يحصل تغيير في الداتا، عشان تشغل كشف التغييرات وتحدث العرض.

لكن استخدام الأحداث غير المتزامنة مع Angular بيخلي الأمور معقدة أكتر وبيحتاج انتباه، عشان نتأكد إن Angular دايماً في حالة تحديث (in sync) مع التغييرات.

### 🔴 Change detection with asynchronous code

في المثال ده، إحنا عاوزين نغير قيمة `name` بعد ثانية واحدة، وهنعمل ده باستخدام `setTimeout`.

<div dir="auto" align="left">

```typescript
@Component({
  template: `
    <button (click)="changeName()">Change name</button>
    <p>{{ name }}</p>
  `,
})
export class AppComponent {
  name = "John";

  changeName() {
    setTimeout(() => {
      this.name = "Jane";
    }, 1000);
  }
}
```

</div>

لما ندوس على الزرار، `changeName` بتتنادي وsetTimeout بيشتغل. `setTimeout` هتستنى ثانية، وبعدها هتنفذ اللي جواها عشان تغير قيمة `name` لـ "Jane".

خلينا نضيف نفس الكود اللي تخيلنا إنه شغال ورا الكواليس في Angular:

<div dir="auto" align="left">

```typescript
component.changeName();

angular.runChangeDetection();
```

</div>

### إيه المشكلة هنا؟

بسبب ترتيب الكود في stack، الـ callback بتاع setTimeout مش هيتنفذ غير بعد ما Angular تكون شغلت runChangeDetection. فبالتالي، Angular هتشغل كشف التغييرات، لكن name لسه ما اتغيرتش، وده هيخلي (view) ما يتحدثش، عشان كده مش هنشوف اسم "Jane" على الشاشة بعد ما نضغط الزرار. وده بيسبب مشكلة في التطبيق ⚠️.

### لكن في الواقع، Angular بتحل المشكلة

لو فاكرين، Angular بتستخدم Zone.js، اللي بيراقب كل الأحداث غير المتزامنة زي setTimeout. فلما setTimeout ينفذ بعد ثانية ويغير name، Zone.js هيلاحظ التغيير ويخطر Angular إنها تشغل runChangeDetection مرة تانية. وده هيخلي (view) يتحدث ويظهر القيمة الجديدة "Jane".

### 🔴 Zone.js to the rescue

#### إيه هي Zone.js وإزاي بتشتغل؟

الZone.js موجودة من أيام Angular 2.0، وهي مكتبة بتعمل حاجة اسمها "monkey patching" لمجموعة من واجهات المتصفح (browser APIs) وتسمح لنا ندخل في دورة حياة (lifecycle) الأحداث اللي بتحصل في المتصفح. طيب إيه معنى الكلام ده؟ ببساطة، ده معناه إننا نقدر نشغل كود معين قبل أو بعد أحداث معينة بتحصل في المتصفح.

خلينا نشوف مثال بسيط:

<div dir="auto" align="left">

```typescript
setTimeout(() => {
  console.log("Hello world");
}, 1000);
```

</div>
الكود ده هيطبع "Hello world" بعد ثانية. طيب، لو إحنا عاوزين نشغل كود معين قبل أو بعد ما setTimeout ينفذ، لأي أسباب تتعلق بالشغل مثلًا 😄؟ ده بيكون مهم لإطار عمل زي Angular، اللي ممكن يكون عاوز يشغل كود معين قبل أو بعد ما setTimeout ينفذ، عشان يتأكد إن كل التغييرات متزامنة مع كشف التغييرات (change detection).

هنا بتيجي Zone.js بدورها. بتسمح لنا نعمل "zone" (ودي حاجة Angular نفسها بتستخدمها) ونتدخل في دورة حياة الـ setTimeout.

مثال مع Zone.js
هنعمل زون جديدة ونضيف عمليات قبل وبعد تنفيذ setTimeout

<div dir="auto" align="left">

```typescript
const zone = Zone.current.fork({
  onInvokeTask: (delegate, current, target, task, applyThis, applyArgs) => {
    console.log("Before setTimeout"); // الكود ده هيشتغل قبل `setTimeout`
    delegate.invokeTask(target, task, applyThis, applyArgs); // هنا بيشغل `setTimeout`
    console.log("After setTimeout"); // الكود ده هيشتغل بعد `setTimeout`
  },
});
```

</div>

عشان نشغل `setTimeout` داخل الزون، محتاجين نستخدم `zone.run` زي كده:

<div dir="auto" align="left">

```typescript
zone.run(() => {
  setTimeout(() => {
    console.log("Hello world");
  }, 1000);
});
```

</div>

الناتج
لما نشغل الكود ده، هنشوف التالي في الـ console

```
Before setTimeout
Hello world
After setTimeout

```

### ازاي Zone.js بتعمل ده؟

اللي Zone.js بتعمله هو إنها بتعدل في الطريقة اللي المتصفح بيشغل بيها الـ APIs زي setTimeout وsetInterval وغيرها. ده بيسمح ل Angular إنها "ترصد" التغييرات اللي بتحصل في الـ components وتحدث UI بشكل متزامن مع الأحداث، وده بيضمن إن كل حاجة في التطبيق شغالة بتناغم وكفاءة.

### 🔴 Zone.js + Angular

الZone.js و Angular: إزاي Angular بتستخدم NgZone في التطبيقات
الAngular بتشغل Zone.js تلقائيًا في كل تطبيق، وبتعمل حاجة اسمها NgZone، وده نوع من الـ zones المخصصة اللي بتراقب التطبيق. NgZone فيها حاجة اسمها onMicrotaskEmpty، ودي عبارة عن Observable، يعني زي عداد بيتابع الأحداث اللي بتحصل في التطبيق. الـ Observable ده بيبعث قيمة لما مفيش أي مهام صغيرة (microtasks) فاضلة في الطابور. وده اللي Angular بتستخدمه عشان تعرف إن كل الكود غير المتزامن (asynchronous code) خلص، وتقدر تشغل كشف التغييرات (change detection) بأمان.

![NgZone wraps every angular application today](https://justangular.com/cd-article/ngzone-1.webp)

NgZone wraps every angular application today

### 🔴 Component Dirty Marking in Angular

في Angular، لما يحصل تغيير جوه (component)، بتقوم بتمييز component كـ "متسخ" (dirty)، وده معناه إن component محتاج يتحدث عشان يظهر التغييرات الجديدة. فكرة "تمييز component كـ dirty" بتساعد Angular إنها تحدد إيه اللي محتاج يتحدث بدل ما تحدث كل حاجة في التطبيق.

#### إيه الحاجات اللي بتخلي Angular تميّز component كـ dirty؟

1. الأحداث (Events زي click، mouseover، إلخ)
   كل مرة بندوس على زرار أو بنعمل حدث معين في (template) عنده مستمع (listener)، Angular بيلف الدالة المستجيبة (callback function) بدالة تانية اسمها wrapListenerIn_markDirtyAndPreventDefault. زي ما الاسم بيوضح 😅، الدالة دي بتعلّم Component كـ dirty.

2. تغييرات (Changed Inputs)
   أثناء تشغيل كشف التغييرات، Angular بتشيك إذا كان فيه تغيير حصل في قيمة (input value) الخاصة بcomponent. لو Inputs اتغير، Angular بتميّز component كـ dirty. وده بيخلي component يعرف إنه محتاج يتحدث.

3. الـ Output Emissions
   عشان تستمع للـ outputs في Angular، بنسجل حدث في template. وزي ما شفنا قبل كده، الـ callback بتتلف بدالة تانية، ولما يتم استدعاء الحدث، component بيتعلّم كـ dirty.

### وظيفة markViewDirty

هي المسؤولة عن تمييز (view) الحالي وكل الأجداد (ancestors) كـ dirty.

### إزاي markViewDirty بتشتغل؟

دي بتعمل تمييز للview الحالي، وكمان لكل Components اللي فوقه (الأجداد) كـ dirty. وده معناه إن لما يحصل تغيير، Angular بتعرف إنها مش بس محتاجة تحدث Component ده، لكن كمان كل الأجزاء اللي بتعتمد عليه.

![Dirty marking component and its ancestor up to the root](https://justangular.com/cd-article/dirty-marking.webp)

Dirty marking component and its ancestor up to the root

### كيف يعمل تحديث البيانات في Angular عند الضغط على الزر؟

لما ندوس على الزر، Angular بتستدعي callback اللي هي هنا `changeName`. وبما إن دي ملفوفة داخل دالة `wrapListenerIn_markDirtyAndPreventDefault`، فده بيخلي Angular تميّز الـ component كـ dirty.

زي ما قولنا قبل كده، Angular بتستخدم Zone.js وبتحاوط التطبيق كله بيه.

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/cd-change.webp)

Dirty marking component and its ancestor up to the root

### الخطوات وراء الكواليس

التمييز كـ Dirty: لما `wrapListenerIn_markDirtyAndPreventDefault` تشتغل، بتقوم بتمييز الـ component وكل الأجداد كـ dirty، وبكده Angular بتعرف إن في حاجة اتغيرت في الـ component أو الـ components اللي فوقه.

تنبيه Zone.js: بعد تمييز الـ components، `wrapListenerIn_markDirtyAndPreventDefault` بتشغل Zone.js.

الonMicrotaskEmpty: بما إن Angular بتراقب الـ observable onMicrotaskEmpty، وأي حدث (زي click) بيسجل listener مع Zone.js، فالـ zone هيعرف إن الـ listener خلص شغله ويقدر يبعث قيمة لـ onMicrotaskEmpty.

إطلاق الـ onMicrotaskEmpty: لما onMicrotaskEmpty يشتغل، ده بيقول لـ Angular إن كل المهام الصغيرة (microtasks) خلصت، وبالتالي الوقت مناسب لتشغيل change detection.

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/zone-notifying.webp)

### تحديث الـ Component Binding

أول ما Angular تشغل change detection، بتبدأ تراجع كل الـ components من فوق لتحت. يعني بتمر على كل الـ components (سواء كانت marked كـ dirty أو لا) وبتشيك على كل الـ bindings. لو الـ binding اتغير، بيتم تحديث الـ view.

لكن ليه Angular بتشيك على كل الـ components 🤔؟ ليه ما تراجعش الـ components اللي marked كـ dirty بس؟ 🤔

الإجابة هنا ليها علاقة بـ استراتيجية change detection

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/cd-binding-refresh.webp)

### 🔴 OnPush Change Detection

في Angular، فيه استراتيجية اسمها OnPush لـ change detection. لما نستخدم الاستراتيجية دي، Angular هتشغل change detection فقط على الـ component اللي متعلم كـ dirty.

<div dir="auto" align="left">

```typescript
@Component({
  // ...
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class UserCard {}
```

</div>

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/cd-onpush.webp)

### إزاي change detection بيشتغل مع OnPush؟

دلوقتي خلينا نشوف الرسوم التوضيحية عشان نفهم أكتر إزاي change detection بيشتغل لما نستخدم استراتيجية OnPush.

بعض الـ components هتكون معلمة كـ OnPush (وأي children ليها هيبقوا تلقائيًا كمان OnPush).

خلينا نعمل نفس الخطوة اللي فاتت، ندوس على زرار في الـ component ونغير قيمة `name`.

1. مرحلة Dirty Marking

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/cd-on-push-click.webp)

2. إشعار Zone.js بالـ Event
   بعدها، الـ event listener هيشعر Zone.js بالحدث.

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/on-push-zone-notify.webp)

3. انتظار انتهاء الكود غير المتزامن
   لما كل الكود غير المتزامن يخلص، onMicrotaskEmpty هتشتغل.

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/on-push-microtask-empty.webp)

4. تشغيل tick في Angular
   بعد كده، Angular هتشغل tick وتبدأ تمر على كل الـ components من فوق لتحت وتشيك عليهم.

لو الـ component حالته كانت:

لوOnPush + Non-Dirty -> تتجاهله
لوOnPush + Dirty -> تشيك الـ bindings -> تحدث الـ bindings -> تشيك الـ children

![ Dirty marking component and its ancestor up to the root
](https://justangular.com/cd-article/onpush-refresh.webp)

الفائدة من OnPush
باستخدام OnPush، Angular تقدر تتخطى أجزاء من الشجرة اللي مفيهاش أي تغييرات، وده بيقلل من تكلفة التحديث ويحسن أداء التطبيق.

### 🔴 OnPush + Observables + async pipe

في الAngular، observables بقت الأداة الأساسية لإدارة البيانات وتحديث الحالة (state changes). ولأن Angular بتدعم observables، هي بتوفر async pipe اللي بيعمل اشتراك (subscription) في الـ observable ويرجع آخر قيمة.

عشان Angular تعرف إن القيمة اتغيرت، `async pipe` بيستخدم `markForCheck` اللي جاية من كلاس `ChangeDetectorRef`.

### ازاي بيشتغل async pipe مع OnPush؟

الكود التالي بيوضح الأساس اللي async pipe بيشتغل عليه:

<div dir="auto" align="left">

```typescript
@Pipe()
export class AsyncPipe implements OnDestroy, PipeTransform {
  constructor(ref: ChangeDetectorRef) {}

  transform<T>(obj: Observable<T>): T | null {}

  private _updateLatestValue(async: any, value: Object): void {
    // code removed for brevity
    this._ref!.markForCheck();
  }
}
```

</div>

الasync pipe بيتابع الـ observable، وأول ما يحصل تغيير في القيمة، بيشغل markForCheck. الطريقة دي هي اللي بتعلّم الـ component كـ dirty، وده بيخلّي Angular تعرف إنه محتاج تحديث.

### ليه ده مهم؟

باستخدام async pipe مع الobservables، Angular بتقدر تتأكد من إن الـ component بيتحدث تلقائيًا لما البيانات تتغير، بدون الحاجة لاستخدام .subscribe بشكل مباشر في الكود. وبما إن markForCheck بيشتغل مع OnPush، Angular بتعرف إنها محتاجة تشيك فقط على الـ components اللي اتعلمت كـ dirty، وده بيخلي التحديثات أكتر كفاءة وأقل تكلفة.

![ Dirty marking component and its ancestor up to the root](https://justangular.com/cd-article/onpush-async-pipe.webp)

### 🔴 OnPush + Observables + Who is triggering zone.js?

في حالة إن البيانات اتغيرت بدون أي event مباشر (زي click أو mouseover)، غالبًا بيكون فيه حاجة شغالة في الخلفية زي setTimeout أو setInterval أو استدعاء HTTP بيحفز Zone.js.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "todos",
  standalone: true,
  imports: [AsyncPipe, JsonPipe],
  template: `{{ todos$ | async | json }}`,
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class TodosComponent {
  private http = inject(HttpClient);
  private ngZone = inject(NgZone);

  todos$ = of([] as any[]);

  ngOnInit() {
    this.ngZone.runOutsideAngular(() => {
      setTimeout(() => {
        // هنا البيانات هتتحدث، لكن مفيش حاجة هتشغّل Zone.js
        this.todos$ = this.getTodos();
      });
    });
  }

  getTodos() {
    return this.http
      .get<any>("https://jsonplaceholder.typicode.com/todos/1")
      .pipe(shareReplay(1));
  }
}
```

</div>

### إيه اللي بيحصل هنا؟

في `ngOnInit`، استخدمنا `ngZone.runOutsideAngular`، وده API بيسمح لنا نشغّل حاجات خارج نطاق Angular zone.

استخدمنا setTimeout (عشان نتخطى أول عملية تكون شغالة وكمان عشان Angular بيشغّل change detection على الأقل مرة واحدة بشكل تلقائي)، وفي داخل setTimeout، أسندنا قيمة جديدة للـ observable (todos$).

بما إن setTimeout شغّال خارج نطاق Angular zone، كمان استدعاء الـ API هيشتغل خارج الـ zone عشان الكود كله جوه runOutsideAngular. وبكده، مفيش حاجة بتنبّه Zone.js إن فيه حاجة اتغيرت.

### النتيجة

لما تشغّل الكود ده في التطبيق، هتلاقي إن اللي بيظهر في المتصفح هو “[]” بس.

### Broken State 🧨!

ده وضع غير مثالي 😄، وبيفتح لنا تساؤل تاني: ازاي Angular تقدر تتعامل مع التغييرات اللي بتحصل خارج نطاق Zone.js، وخصوصًا مع استراتيجية OnPush؟

### الحل؟

في الحالة دي، نقدر نستخدم `ChangeDetectorRef` وندعي `markForCheck` بعد التحديث عشان نجبر Angular على تشغيل change detection على الـ component ده بالتحديد، وده هيضمن إن التحديثات بتظهر في العرض حتى لو التغييرات حصلت خارج Zone.js.

### 🔴 Why can’t we just run the change detection for the component that is marked as dirty?

#### ليه ما نقدرش نكتفي بتشغيل change detection للـ component اللي متعلم كـ dirty؟

ممكن نعمل كده باستخدام detectChanges في كلاس ChangeDetectorRef، لكن ليها مشاكلها. لأن detectChanges بيشغل change detection بشكل متزامن، وده ممكن يسبب مشاكل في الأداء. لأن كل حاجة هتتنفذ في نفس مهمة المتصفح (browser task)، وده ممكن يسبب "performance issues" في الـ main thread ويخلي الأداء متقطع (jank).

تخيل مثلاً إنك بتشيك على التغييرات في قائمة فيها 100 عنصر كل ثانية أو ثانيتين، ده هيكون عبء كبير على المتصفح

#### الفرق بين markForCheck و detectChanges (تشغيل متزامن vs تشغيل مؤجل)

الmarkForCheck: لما بنستخدم markForCheck، إحنا بس بنقول لـ Angular إن فيه component متعلم كـ dirty، لكن مفيش أي تحديث بيحصل في اللحظة دي. حتى لو دعينا markForCheck 1000 مرة، مش هيبقى فيه مشكلة، لأن التحديث الفعلي هيحصل في دورة الـ change detection التالية، وده بيوفر أداء أفضل.

الdetectChanges: لما نستخدم detectChanges، Angular بتعمل الشغل الحقيقي فورًا، زي إنها تراجع الـ bindings وتحدث العرض (view) لو في حاجة محتاجة تتحدث. وده ممكن يسبب ضغط على الأداء، وخصوصًا لو عندنا مكونات كتيرة أو
تحديثات متكررة.

#### ليه يفضل نستخدم markForCheck بدل detectChanges؟

الmarkForCheck بيسمح لـ Angular إنها تشتغل بكفاءة أعلى عن طريق تأجيل التحديثات لحد ما تكون جاهزة لتشغيل change detection بشكل مجمع (coalesced run) بدل ما يكون فيه تحديثات متزامنة (sync runs) لكل component منفصل. وده بيخلي أداء التطبيق سلس أكتر ويقلل الضغط على الـ main thread في المتصفح.

### Signals 🚦

الـ Signals في Angular جابت تحسينات كبيرة في تجربة المطورين. نقدر بسهولة نخلق ونعمل اشتقاق للـ state وكمان نشغل side effects لما الـ state يتغير باستخدام الـ effects. مش محتاجين نعمل اشتراك ولا إلغاء اشتراك فيها، ومش محتاجين نقلق من مشاكل الـ memory leaks 🧯.
<div dir="auto" align="left">

```typescript
const name = signal('John');
const upperCaseName = computed(() => name().toUpperCase());

effect(() => {
  console.log(name() + ' ' + upperCaseName());
});

setTimeout(() => {
  name('Jane');
}, 1000);

// Output:
// John JOHN
// Jane JANE
```

</div>
كمان بنقدر نستخدم الـ signals في الـ template زي ما بنستخدم الـ function calls العادية.

<div dir="auto" align="left">

```HTML
@Component({
  template: `
    <button (click)="name.set('Jane')">Change name</button>
    <p>{{ name() }}</p>
  `
})
export class AppComponent {
  name = signal('John');
}
```

</div>

### 🔴 Signals and Change Detection

في الإصدار الجديد من Angular v17، حصل تطوير في موضوع الـchange detection أو "كشف التغيرات" في الـtemplates، اللي بيخليها تستجيب لأي تحديثات في البيانات تلقائيًا بطريقة أسهل وأسرع.

#### 1. الـSignals بدل الـAsync Pipe
زمان كنا بنستخدم حاجة اسمها async pipe عشان نقدر نستجيب لتحديثات البيانات في الـtemplate. يعني لو في قيمة بتتغير، الـasync pipe كان بيخلي Angular يعرف إن في تحديث ويعمل markForCheck للـtemplate عشان يرندر التغييرات دي. بس دلوقتي مع الإصدار الجديد، Angular بقى بيفهم إن الإشارات (signals) اللي بنستدعيها في الـtemplate مش مجرد استدعاءات دوال، لأ بقى بيشوفها كحاجات تستاهل المتابعة. وبالتالي، لو استخدمنا signal، Angular أوتوماتيك هيسجل حاجة اسمها effect (أو consumer) عشان يرائب الـsignal دي ويعمل markForCheck كل ما يحصل أي تغيير في قيمتها.

![ Dirty marking component and its ancestor up to the root](https://justangular.com/cd-article/signals-data-in-template.webp)

#### فإيه الفايدة هنا؟
مش محتاجين الـasync pipe: دلوقتي بقى سهل تستدعي الـsignal في الـtemplate عادي من غير ما تضطر تستخدم async pipe.

أداء أسرع: الـsignals دلوقتي بتوفر أداء أفضل لإن الـchange detection بيحصل في الأماكن اللي محتاجينها بس.


###  🔴Improving “how” – signals

لما signal  ياخد قيمة جديدة في الـ template بتاعة الـ component، اللي بيحصل إنه بيقول لـ reactive consumer (اللي هو الكود اللي بيتابع التغيرات) إنه فيه تغيير محتاج يتشاف. لكن هنا التركيز على حاجة معينة: اللي بيتم تعليمه كأنه "dirty" أو محتاج تحديث هو reactive consumer اللي متعلق بالـ component view مش component view نفسها. يعني مش الكومبوننت ككل اللي بيتعلم كأنه عايز يتحدث، زي اللي بيحصل في الحالة العادية لو كنت بتستخدم OnPush.

#### يعني إيه Reactive Consumer؟
ببساطة، reactive consumer هو كود أو جزء من البرنامج وظيفته إنه "يراقب" signals أو بيانات معينة عشان يشوف لو حصل عليها تغيير، ويقرر إزاي يتصرف بناءً على التغيير ده. يعني هو "المستهلك" للتحديثات اللي بتحصل على البيانات، وبيشتغل بطريقة reactive (تفاعلية).

#### مثال توضيحي
تخيل عندك تطبيق فيه قائمة مهام، وكل ما المستخدم يضيف مهمة جديدة أو يحذف مهمة، عايز القائمة تتحدث تلقائيًا. هنا، الـ reactive consumer بيكون الجزء من الكود اللي "منتظر" يشوف لو فيه تغيير في قائمة المهام عشان يظهرها أو يخفيها من الشاشة. لما يحصل تغيير (زي إضافة مهمة جديدة)، الـ reactive consumer يعرف إنه فيه حاجة جديدة وبيتعلم إنه "dirty" أو محتاج يتحدث عشان يعرض التغيير.


#### ليه بنحتاج الـ Reactive Consumer؟
الفكرة هنا إنك مش عايز التطبيق يعيد بناء كل الكومبوننت أو الـ UI من الأول في كل مرة يحصل فيها تغيير بسيط. بدل كده، بنستفيد من إن عندنا reactive consumers، بحيث يقدروا يتابعوا البيانات المطلوبة ويحدثوا بس الأجزاء المتأثرة. ده بيساعدنا نحسن الأداء، لأننا مش بنعيد بناء الكل، بس بنركز على اللي اتغير.


#### يعني إيه Component View؟
الComponent view هي الشكل أو  (View) اللي بيظهر للمستخدم من component معين في Angular. كل component بيكون ليه "view" خاص بيه، وده اللي بيعرض واجهة المستخدم (UI) اللي مرتبطة بالكومبوننت ده.

#### علاقة Component View بـ Change Detection
الـ Component View هو الجزء اللي Angular بيعمل عليه "فحص للتغييرات" (change detection)، بحيث لما يحصل تغيير على البيانات اللي مرتبطة بالـ view، بيتم تحديثها على الشاشة للمستخدم بدون الحاجة لتحديث الكومبوننت بالكامل. الفكرة دي بتساعد في تحسين أداء التطبيق لأنك مش مضطر تعمل إعادة بناء لكل الكومبوننتات مرة واحدة، لكن بس الجزء اللي فعلاً حصل فيه تغيير.


![ Dirty marking component and its ancestor up to the root](https://wp.angular.love/wp-content/uploads/2024/10/one-path.gif)

#### قبل Angular 17
قبل إصدار Angular 17، لما الـ reactive consumer كان بيتعلم إنه "dirty"، ده كمان كان بيخلي الـ component view نفسها تتعلم كأنها محتاجة تحديث. وده بيخلي الطريقة شبيهة باللي بتعمله AsyncPipe: بيشوف لو فيه تحديث، ويعمل التحديث على مستوى الكومبوننت ككل.


بالتالي، لو عايز تطبق الاستراتيجية دي وتقلل الكشف على التغيرات (عشان تتحسن الكفاءة)، كنت هتستخدم OnPush على كل الـ components، بحيث الكشف على التغيرات يتم على مسار واحد بس، ومش بيشمل كل مكونات التطبيق مرة واحدة.


#### بعد Angular 17
مع إصدار Angular 17 والأحدث، الوضع اتغير شوية. لما الـ reactive consumer يتعلم كأنه "dirty"، ده مش بيأثر على component view نفسها. بدل من كده، فيه دالة جديدة اسمها markAncestorsForTraversal بتشتغل. الدالة دي بتعمل حاجة شبيهة، لكنها بتمشي من الـ component لغاية فوق عند كل الـ components الجدود (من الـ component الحالي لغاية الكومبوننت الرئيسية اللي فوق الكل).


لكن الفرق هنا إن الدالة دي مش بتعلمهم إنهم كلهم محتاجين تحديث، لا! هي بتعلم بس الجدود إن عندهم مكون فرعي (child component) محتاج تحديث. وبتديهم علامة اسمها HasChildViewsToRefresh كإشارة إنه فيه تغيير جاي من تحت، لكن مش بتعمل تحديث فعلي غير لما يوصل عند الـ component اللي فيه التغيير الفعلي.

![ Dirty marking component and its ancestor up to the root](https://wp.angular.love/wp-content/uploads/2024/10/mark-traversal.gif)

التقنية الجديدة للتأكد من التغيير (change detection) اتحدثت. دلوقتي لما العملية تبدأ والشجرة في الحالة دي، بيعدي على الـcomponents A وE من غير ما يعمل لهم change detection، وده لأنهم OnPush لكن مش dirty. بفضل الـHasChildViewsToRefresh flag، Angular بيكمل يزور النودز اللي معمول لها علامة بالـflag ده ويدور على الـcomponent اللي محتاج change detection (في مثالنا هنا هو اللي فيه reactive consumer ومتعلّم عليه إنه dirty). لما يوصل للـcomponent F، يلاقي إن الـreactive consumer بتاعه dirty، فـcomponent ده بس اللي بيحصل له change detection – وده component الوحيد!


حلو، صح؟ بدل ما يعمل change detection للمسار الكامل بتاع الـcomponents، دلوقتي بقى بيعمله component واحد بس. ده مثال مبسط لشجرة components، لكن المكاسب في الأداء في التطبيقات الفعلية أكبر بكتير.

النهج الجديد في الـchange detection، اللي بيخلي component واحد بس يحصل له change detection بفضل الـsignals، بيطلق عليه "شبه محلي" أو “global-local/glocal” change detection.

🔴 تحذيرات لكن في شوية تحذيرات لازم تاخد بالك منها. خلينا نبص على مثال، لما ضغط المستخدم على الزرار وتسبب في تغيير إشارة signal:

### الـglocal change detection caveat


![ Dirty marking component and its ancestor up to the root](https://wp.angular.love/wp-content/uploads/2024/10/caveat1.gif)


### فين المشكلة؟

المشكلة بتحصل لو التغيير جاي من حاجة معينة، زي لما المستخدم يدوس على زرار، وده بيعمل تغيير في البيانات. في الحالة دي، Angular بيطبّق القواعد القديمة وبيعتبر إن الوحدة نفسها وكل اللي فوقها في الشجرة dirty، وده بيرجعنا للطريقة التقليدية اللي بتفحص الوحدات كلها، حتى لو بس وحدة واحدة محتاجة تحديث.

### إيه اللي نتعلمه من ده؟

لو التغيير في البيانات جاي من حاجة زي setTimeout أو Observable، ساعتها Angular هيشتغل بالنظام الجديد ويفحص الوحدات اللي محتاجة فقط. لكن لو التغيير سببه حاجة زي ضغط زرار، النظام القديم بيشتغل وبيعمل فحص لكل الوحدات اللي فوق الوحدة دي.

### 🔴 تحذير تاني:

لو في وحدات مش بتستخدم نظام OnPush، فحتى مع النظام الجديد، الوحدات دي هيتعمل لها فحص كل مرة، لأنها مش متعلّم عليها بالنظام الجديد.

![ Dirty marking component and its ancestor up to the root](https://wp.angular.love/wp-content/uploads/2024/10/caveat2a.gif)

### إيه اللي بيحصل لو مفيش OnPush؟

لو عندنا شجرة فيها وحدات زي A، B، C، وD، وكلهم مش شغالين بـOnPush، والوحدة F فيها تغيير بسيط أو تحديث، اللي هيحصل هو إن مش بس الوحدة F اللي هيتعمل لها change detection، لكن كمان الوحدات اللي في الشجرة ABCD هيتعمل لها فحص كامل في نفس الوقت. السبب إن الوحدات اللي مش بتستخدم OnPush بتشتغل على النظام الافتراضي اللي بيفحصها كل مرة يحصل فيها أي تغيير في التطبيق، حتى لو مش محتاجة.

### ليه ده بيأثر علينا؟

ده بيأثر على كفاءة التطبيق، لأنه بيزود عدد الوحدات اللي بيتم فحصها مع كل تغيير، حتى لو التغيير حصل في جزء بعيد عنها. وبالتالي، وجود وحدات مش بتستخدم OnPush بيلغي جزء من الفائدة اللي بنحصل عليها من نظام الـsemi-local change detection، لأنه بيخلينا نفحص وحدات أكتر من اللي محتاجة فعلاً.


### 🔴 Zoneless Angular — Let’s remove zone.js from Angular

ليه نشيل Zone.js أصلاً؟ خلينا نفكر الأول ليه ممكن نحب نتخلص من Zone.js. فيه شوية أسباب:

تقليل حجم الـ bundle في البداية: بص كده على الـ outputs اللي قدامك (واحد Zone-full وواحد Zoneless). زي ما انت شايف، Zone.js حجمه حوالي 30kB خام، وبيقل لـ 10kB لما يتضغط. ده حجم مش قليل، خصوصاً إنه بيدخل ضمن الحاجات اللي لازم تتحمل قبل ما التطبيق يبدأ يشتغل.

![Zone-full vs Zoneless build output](https://wp.angular.love/wp-content/uploads/2024/10/build-output.png)

تجنب الـ change detection اللي ملهاش لازمة: Zone.js بيساعد في إن Angular يعمل change detection من خلال إنه بيبلغه لما أي عملية تخلص. لكن هو في الحقيقة مش بيعرف إذا كانت العمليات دي غيرت أي داتا ولا لأ. عشان كده، الفريم وورك بيبالغ شوية وبيعمل run "للاحتياط".

عايز أوضح حاجة – Zone.js كان أداة رهيبة (أو على الأقل كان كده لما بدأ) وساهم كتير في نجاح Angular من الأول. كان بيخلي التعامل مع الفريم وورك سهل حتى للمطورين المبتدئين – يركزوا بس على شغلهم، وكل حاجة تشتغل بطرق سحرية.

لكن، زي ما شوفنا، السحر ده له تكلفة. متأكد إن كتير من التطبيقات شغالة كويس جداً مع Zone.js. بس في حالات التطبيقات المعقدة اللي محتاجة أداء أعلى، أكيد البحث عن بدائل خطوة منطقية.

###  🔴Zoneless scheduler

الـ "Zoneless Scheduler" الجديد اللي تم تقديمه في الإصدار 17.1 بيغير طريقة عمل الـ "Zone.js" events وبيستنى لحد ما يجي له إشعار صريح من أجزاء تانية في الفريمورك عن أي تغييرات. التغيير ده مهم لأنه بدل ما يشغل عملية الـ "change detection" لما "أي عملية تحصل وخلاص"، النظام بقى يشغله "لما يوصل له إشعار أن فيه بيانات اتغيرت".

عشان يحقق ده، الجدول الجديد بيعرض طريقة خاصة اسمها "notify" وبتتدعي في الحالات دي:

لما "signal" اللي بيتقرا في الـ "template" يوصل له قيمة جديدة (بالتحديد، لما "markAncestorsForTraversal" تتدعي).

لما الـ "component" يتعلم أنه بقى "dirty" عن طريق "markViewDirty". ده ممكن يحصل بسبب وصول قيمة جديدة من "AsyncPipe"، أو "template-bound event"، أو عن طريق استدعاء "ComponentRef.setInput"، أو استدعاء "ChangeDetectorRef.

markForCheck" بشكل مباشر، أو حاجات تانية.

لما "afterRender hook" يتسجل، أو لما "view" يتضاف تاني للـ "change detection tree" أو يتشال من الـ "DOM". في الحالات دي، "notify" بتتدعي لكنها بس بتنفذ الـ "hooks" من غير ما تعمل "refresh" للـ "view".

ممكن تسأل لو "change detection" ممكن يشتغل كتير لو "signals" كتيرة اتغيرت في نفس الوقت أو لو حصلت "events" بسرعة ورا بعض. لكن التنفيذ بتاع الـ "scheduler" معمول عشان يتعامل مع ده بكفاءة. بيجمع الإشعارات على مدار فترة قصيرة وبيعمل "schedule" لتشغيل "change detection" مرة واحدة بدل ما يشغله كذا مرة. السلوك ده مبني على سباق بين "setTimeout" و "requestAnimationFrame"، بس مش هندخل في التفاصيل دي هنا. المهم إن "notify" دي بتتجمع، عشان تضمن أحسن أداء.

![Zone-full vs Zoneless build output](https://wp.angular.love/wp-content/uploads/2024/10/zoneless.gif)

</div> -->

<!-- <div dir="auto" align="left">

```typescript

```

</div>
<div dir="auto" align="left">

```HTML

```

</div> -->
