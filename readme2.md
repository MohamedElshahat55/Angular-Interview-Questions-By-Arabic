## What are signals?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
خليني أقولك ببساطة: الـ"Signals" في Angular هي زي وعاء بيحتفظ بقيمة معينة (سواء رقم، نص، أو حتى بيانات معقدة)، والميزة الكبيرة فيها إنها بتقدر تبلغ أي "مستهلك"  لما القيمة دي تتغير.

فكرتها إنها بتسهّل متابعة أي تغييرات بتحصل على البيانات اللي بنعتمد عليها. يعني، لما مثلاً تبقى عندك واجهة بتظهر (Counter) بيزيد، ممكن تعمل الـ"counter" ده كـ"Signal". لما قيمة العداد تتغير، أي مكان بيستخدم القيمة دي هيعرف فوراً إن فيه تغيير حصل.

### دلوقتي عندنا نوعين من الـ"Signals"

##### الWritable Signal

النوع ده تقدر تغيره بنفسك. يعني تقدر تزود القيمة بتاعته، تنقصها، أو تعدلها بأي شكل.

<div dir="auto" align="left">

```typescript
const count = signal(0);
```

</div>

### ازاي نغير قيمة الـWritable Signal؟

#### تغيير مباشر باستخدام .()set

تقدر تستخدم ()set لو عايز تدي قيمة جديدة مباشرة للـ"signal"

<div dir="auto" align="left">

```typescript
count.set(3); // كده القيمة بقت 3
```

</div>

#### تحديث القيمة باستخدام ()update

تقدر كمان تستخدم ()update علشان تحسب قيمة جديدة بناءً على القيمة الحالية. زي إنك تزود القيمة بواحد:

<div dir="auto" align="left">

```typescript
count.update((value) => value + 1); // كده القيمة بتزيد 1
```

</div>

##### Read-only Signal

النوع ده بيكون للقراءة بس، مش هتقدر تعدل فيه مباشرة. وده بيبقى مفيد في الحالات اللي بتعتمد على حسابات من "signals" تانية، زي لما يبقى عندك مثلاً "double counter" اللي بيعتمد على قيمة "counter" تاني، فبيتحسب تلقائي.

✨ فالـ"Signals" دي بتبسط الموضوع لما يبقى عندك تطبيق معقد، لأن Angular بيتابع أي تحديثات بتحصل في "signals" تلقائياً ويرندر بس الأماكن اللي فعلاً اتغيرت، مش كل الصفحة.

### الComputed Signals

أما الـ"Computed Signals" فهي نوع تاني من "signals" لكن بتبقى للقراءة فقط (read-only)، لأنها بترتبط بقيم signals أخرى وبتحسب قيمة جديدة بناءً عليها. علشان تعمل "computed signal"، بتستخدم دالة ()computed وبتكتب طريقة الحساب بناءً على signals تانية.

<div dir="auto" align="left">

```typescript
const count = signal(0);
const doubleCount = computed(() => count() * 2);
```

</div>
✨ هنا، doubleCount بيحسب القيمة كضعف قيمة count، وبيحدث نفسه تلقائيًا لما count تتغير.

### مميزات الـComputed Signals

#### Lazy Evaluation

الـ"computed signals" بتحسب القيمة بس لما تحتاج تقراها لأول مرة. القيمة بعد كده بتبقى محفوظة (cached)، يعني لما تقراها تاني، Angular مش هيحسبها من الأول، إلا لو في حاجة اتغيرت.

#### Dynamic Dependencies

بتتابع بس الsignals اللي تم قراءتها أثناء الحساب. فلو مثلاً عندنا شرط بيحدد إذا كانت القراءة من count أو لأ، الـ"computed signal" هيتابع count بس في حالة تحقق الشرط، وإلا مش هيتابعها.

### 🔴 ملاحظة مهمة

الـ"computed signals" مش بتقبل التعديل المباشر باستخدام .()set أو .()update لأنها للقراءة بس، وده بيساعد في تأكيد إنه يتم تحديثها تلقائيًا بناءً على signals اللي بتعتمد عليها.

### ليه Signal مش زي المتغير العادي؟

لما بنعمل متغير عادي، لو غيرنا قيمته مش بيأثر في الواجهة مباشرة، وعلشان يحصل ده محتاجين نعمل "تحديث" يدوي. إنما مع الـSignal، لما بتغير القيمة بشكل صحيح، التغيير ده بينعكس تلقائي على الواجهة اللي بتعتمد على القيمة دي.

### الSignal لعدد (Number)

<div dir="auto" align="left">

```typescript
import { signal } from "@angular/core";

const numberSignal = signal(10); // هنا بنخزن قيمة 10 كعدد
```

</div>

🔴 لو حاولنا نغير القيمة كده:

<div dir="auto" align="left">

```typescript
//❌  ده غلط
numberSignal = 20; // هنا بنحاول نغير المتغير نفسه مباشرة وده بيعمل مشكلة
```

</div>
🤨 المشكلة هنا: إننا غيرنا refrence  بتاع Signal نفسه، لكن Angular مش هيعرف إنه في تغيير لأننا عدينا على الـ Signal مباشرة.

### ✅ الطريقة الصح:

بنستخدم ()set عشان نحدث القيمة:

<div dir="auto" align="left">

```typescript
numberSignal.set(20); // كده بنغير القيمة بطريقة صح
```

</div>
ليه ده صح؟ لأن ()set بتعرف الـ Angular إن في تغيير، فبيحدث أي حاجة بتستخدم القيمة دي تلقائي.

### الSignal ل (Object)

إزاي نعملها:

<div dir="auto" align="left">

```typescript
const userSignal = signal({ name: "Ali", age: 25 });
```

</div>

### ❌ إزاي نعدلها غلط

<div dir="auto" align="left">

```typescript
//❌ ده غلط
userSignal().name = "Ahmed";
```

</div>

### ✅ الطريقة الصح:

<div dir="auto" align="left">

```typescript
userSignal.set({ ...userSignal(), name: "Ahmed" });
```

</div>
ليه ده صح؟ هنا استخدمنا ..().userSignal عشان ناخد object القديم بالكامل، وبعدها غيرنا name بس، وبعدين رجعنا object الجديد للـ Signal. كده Angular يعرف إنه في تغيير.

### Signal لقائمة (Array)

إزاي نعملها:

<div dir="auto" align="left">

```typescript
const numbersArraySignal = signal([1, 2, 3]);
```

</div>

### ❌ إزاي نعدلها غلط

<div dir="auto" align="left">

```typescript
//❌ ده غلط
numbersArraySignal().push(4); // هنا بنغير الأراي مباشرة وده غلط
```

</div>

### ✅ الطريقة الصح:

<div dir="auto" align="left">

```typescript
numbersArraySignal.set([...numbersArraySignal(), 4]); // بنعيد تعيين الأراي كلها
```

</div>
أو نقدر نستخدم ()update:

<div dir="auto" align="left">

```typescript
numbersArraySignal.update((numbers) => [...numbers, 4]);
```

</div>

### Signal لقائمة من (Array of Objects)

إزاي نعملها:

<div dir="auto" align="left">

```typescript
const usersArraySignal = signal([
  { name: "Ali", age: 25 },
  { name: "Mona", age: 30 },
]);
```

</div>

### ❌ إزاي نعدلها غلط

<div dir="auto" align="left">

```typescript
//❌ ده غلط
usersArraySignal()[0].name = "Hassan"; // هنا بنغير الأراي مباشرة وده غلط
```

</div>

### ✅ الطريقة الصح:

<div dir="auto" align="left">

```typescript
usersArraySignal.update((users) =>
  users.map((user) =>
    user.name === "Ali" ? { ...user, name: "Hassan" } : user
  )
);
```

</div>
</div>

## Why Signal?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الفكرة الأساسية
أولاً، في التطبيقات الكبيرة زي اللي بتعملها بـAngular، الموضوع بيكون مليان بيانات، والبيانات دي بتتغير كل شوية. لما تتغير بيانات معينة، عايزين نعرف إن الجزء ده من التطبيق يتحدث تلقائيًا من غير ما نرجع نرندر كل حاجة من أول وجديد. تقليديًا، الAngular بتعتمد على أدوات زي الـ"Observables" و"Subjects" علشان تتابع التغييرات وتحدث البيانات بشكل تلقائي، لكن الطريقة دي بتتطلب جهد شوية، وبالذات في الحالات اللي فيها حاجات بسيطة زي تغير قيمة عداد أو بيانات خفيفة.

### ليه Signals؟

الـ"Signals" بتقدم طريقة أبسط وأسرع للتعامل مع التغيرات في البيانات من غير ما تضطر تستخدم Observables وطرق معقدة. مثلاً لو عندك قيمة معينة عايزها تتغير وتؤثر على جزء معين في UI ممكن تحطها كـ"Signal". فلما القيمة دي تتغير، كل عنصر أو جزء بيعتمد عليها هيعرف بشكل تلقائي، وده من غير ما ترجع تشغل "change detection" لكل التطبيق.

### الـ"signals" ليها تأثير كبير على عملية change detection في Angular، وده لأنها بتساعد في تحسين الأداء وتبسيط عملية تحديث البيانات بشكل مباشر.

لما بنستخدم الـ"signals"، التحديث بيكون على مستوى كل جزء (أو "Component") بشكل مستقل، بمعنى إن أي جزء بيستخدم قيمة معينة من "signal" هيتم تحديثه بس لو حصل تغيير في القيمة دي، من غير ما يضطر Angular يشغل عملية change detection لكل التطبيق. فده بيوفر كفاءة أكبر في التطبيقات الكبيرة، ويقلل من كمية الأكواد المطلوبة للتحديث.

### التوافق مع "OnPush" Strategy

لو بتستخدم استراتيجية "OnPush" للتحديثات في Angular، فالـ"signals" بتتكامل معاها بشكل ممتاز، لأنها بتسمح بتحديث القيم اللي بتتأثر بشكل مباشر من غير ما يتم تحديث كل شيء. لما يكون عندك جزء معين بيعتمد على "signal"، و"OnPush" مفعل، الواجهة هتتحدث تلقائيًا لما تتغير قيمة الـ"signal" من غير تدخل أو إعادة حسابات غير ضرورية.

### تقليل الحمل على الذاكرة والبروسيسور

مع الـ"signals"، Angular مش بيحتاج يشغل كل الـ change detection cycles، لأن الـ"signal" بيبعت إشعار بإن التغيير حصل بس للأجزاء اللي بتعتمد على القيمة دي. فبكده بنقلل من الضغط على الذاكرة والبروسيسور، وده بيساعد في تحسين أداء التطبيق عمومًا.

### سهولة في التعامل مع التغيرات المتكررة

الـ"signals" بتتيح طريقة بسيطة للتعامل مع القيم اللي بتتغير بشكل متكرر، زي مثلاً counter أو حالة معينة. باستخدام signals، ممكن تتحكم في عملية التحديث من غير ما تحتاج تكتب أكواد إضافية لمتابعة التغييرات، وده بيسهل على المطورين التعامل مع الـUI بشكل ديناميكي وفعال.

### ✨ خلاصة

فايدة الـ"signals" الأساسية في الـchange detection هي إنها بتخلي التحديثات أكتر تركيزًا وأقل حملًا على النظام، وده بيحسن من استجابة التطبيق بشكل كبير وبيوفر وقت وجهد كبير على المطورين، خاصةً في التطبيقات اللي فيها بيانات كتير بتتحدث باستمرار.

</div>

## Angular signals vs. observables: How and when to use each

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### إيه هي مشكلة الـ Observables وليه ظهر الـ Signals؟

الـ Observables تعتبر أداة قوية في Angular بتخلينا نتحكم في البيانات المتغيرة على مدار الوقت، زي لما بيجيلك تحديثات لبيانات التطبيق من API أو WebSocket. يعني لو عندك حاجة بتتغير بانتظام (زي رقم بيزيد كل ثانية)، تقدر تستخدم Observable علشان تتابع التغييرات دي.

فكرة الـ Observable هي إنها بتطلع القيم الجديدة للبيانات وتبعت إشارات للتحديثات دي للتطبيق، وده بيحصل على مدار الوقت، مش مرة واحدة وخلاص. باستخدام الـ “async pipe” ممكن تخلي القيم تظهر في الـ UI مباشرةً. بس العيب إن استخدام الـ Observables أحياناً بيكون معقد، وخصوصًا لما بتجمع أكتر من مصدر للبيانات أو لما تستخدم عمليات معقدة كتير من RxJS، اللي ممكن تخلي الكود صعب يتفهم أو يتتبع، وممكن كمان يعمل مشاكل في الأداء والذاكرة لو مش متظبط صح.

### طيب.. إيه الجديد في الـ Signals؟

الـ Signals بقت جزء من Angular من أول الإصدار 16، وبتقدم طريقة جديدة وأبسط في التعامل مع البيانات المتغيرة. الفكرة ببساطة إنك بدل ما تستخدم Observable وتتعامل مع التعقيد بتاع RxJS، تقدر تستخدم Signal لتحديث البيانات. الميزة هنا إنها بتسمحلك تتابع التغيرات بطريقة أبسط وأكتر تحكم، وده بيفيد في حاجات كتير خاصة في التطبيقات الكبيرة اللي فيها تفاصيل كتير عايزة تحديث بانتظام من غير ما تعمل عبء كبير على الأداء.

### إمتى تستخدم الـ Signals ومتى تستخدم الـ Observables؟

#### 🔴 أولاً: امتى تستخدم الـ observables؟

الـ observables بتكون مناسبة جدًا في حالة البيانات اللي بتيجي على شكل تدفق مستمر زي الداتا اللي جايه من API، إشعارات الـ real-time، أو العمليات اللي بتم بشكل غير متزامن. يعني لو عندك service بتجيب بيانات كل شوية أو بتتغير كل شوية زي إشعارات أو حاجة بتتحدث بانتظام، فالأفضل هنا إنك تستخدم observable.

لازم تشترك subscribe في الـ observable عشان تاخد البيانات، ولما تخلص بتحتاج تعمل unsubscribe عشان تقفل الاتصال وتوفر موارد.
كمان في الـ observables تقدر تعمل حاجات زي التصفية، الترتيب، والتعديل باستخدام الـ pipe والـ operators، ودي بتساعدك تعمل معالجة للداتا اللي جاية بشكل مرن وسهل.

#### 🔴 ثانيًا: امتى تستخدم الـ signals؟

الـ signals في Angular بتكون أفضل في الجزء الخاص بالـ UI، يعني الجزء اللي بيتعامل مع UI أو components بشكل مباشر. لو عندك بيانات عايز تعرضها وتتغير بشكل ديناميكي مع كل تعديل، الـ signals هتكون مناسبة.

مش بتحتاج تعمل subscribe أو unsubscribe زي الـ observable؛ هنا بتستخدم set عشان تغير القيمة أو update عشان تحدث القيمة بناءً على الحالة الحالية.

كمان تقدر تستخدم حاجة اسمها computed signals اللي بتسمح لك تعمل إشارات جديدة بتعتمد على إشارات موجودة فعلاً، ودي مفيدة لما يكون عندك أكتر من عنصر بيعتمد على داتا واحدة.
استخدام الـ signals هيكون مناسب لو التصميم بتاع الـ template بيعتمد على تغيير لحظي، عشان تتأكد إن components بتتحدث مع كل تعديل في الداتا بدون لخبطة أو مشاكل.

</div>

## What is Effect in signal?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ببساطة، الـEffects في Angular هي عبارة عن عمليات بتشتغل بشكل تلقائي كل مرة تحصل فيها أي تغييرات في قيمة معينة بنسميها Signal.

الفكرة هي إن الـEffect بيسجل قيمة الـSignal اللي بيتتبعها، ولما يحصل تغيير في قيمة الـSignal دي، الـEffect ده بيشتغل تاني ويعمل العمليات المطلوبة.

يعني مثلا لو عندك عداد وعايز تسجل القيمة كل مرة تتغير فيها، ممكن تستخدم الـEffect كالتالي

<div dir="auto" align="left">

```typescript
effect(() => {
  console.log(`The current count is ${count()}`);
});
```

</div>
هنا، كل مرة قيمة count تتغير، الـEffect هيشتغل وهيطبع القيمة الجديدة للعداد. الفايدة هنا إنك مش محتاج تكتب كود منفصل للتأكد إن القيمة اتغيرت، Angular بيقوم بالموضوع ده تلقائيًا نيابة عنك.

#### إيه هي حالات الاستخدام للـEffects؟

مش مطلوب إنك تستخدم الـEffects دايمًا، لكن فيه شوية حالات معينة ممكن تحتاج تستخدمها فيها:

##### Logging data being displayed and when it changes, either for analytics or as a debugging tool.

مثلا لو محتاج تسجل أي تغير بيحصل في الداتا اللي بتظهر للمستخدم، عشان التحليل أو التتبع.

##### Keeping data in sync with window.localStorage.

مزامنة البيانات مع localStorage: عشان البيانات تحفظ محليًا وتتحدث تلقائيًا.

##### Adding custom DOM behavior that can't be expressed with template syntax.

#### Injection context

في Angular، التعامل مع Injection Context أمر أساسي لإنشاء الـEffects بطريقة صحيحة، إذ تحتاج هذه البيئة (Injection Context) لتشغيل ()effect داخل سياق تقدر تستدعي فيه دوال inject، مثل الكومبوننت، (directives)، أو (services). فيما يلي طرق مختلفة لتنفيذ الـEffects ضمن Injection Context:

وبذلك يظل الـEffect يعمل فقط أثناء حاجة الكومبوننت له، ويتوقف تلقائيًا عندما يتم تدمير الكومبوننت.

تسجيل Effect داخل كود البناء (constructor)
أبسط طريقة هي تسجيل الـEffect داخل الـconstructor مباشرة في الكومبوننت أو الخدمة. مثلًا

باختصار، استخدام Injection Context يسهل إنشاء وإدارة الكائنات والخدمات بطريقة تجعل التطبيق مرنًا، مستقرًا، وقابلاً للصيانة

<div dir="auto" align="left">

```typescript
@Component({...})
export class EffectiveCounterComponent {
  readonly count = signal(0);

  constructor() {
    // Register a new effect.
    effect(() => {
      console.log(`The count is: ${this.count()}`);
    });
  }
}
```

</div>

##### ممكن كمان تسجل الـEffect كجزء مستقل في الكومبوننت وتدي له اسم يوضح وظيفته.

الطريقة دي بتساعد لو عايز تتابع أو توضح الهدف من الـEffect بشكل أوضح، وكمان بتخلي الكود منظم أكتر.

<div dir="auto" align="left">

```typescript
@Component({...})
export class EffectiveCounterComponent {
  readonly count = signal(0);
  private loggingEffect = effect(() => {
    console.log(`The count is: ${this.count()}`);
  });
}
```

</div>

##### إنشاء Effect خارج الـconstructor باستخدام Injector

في بعض الحالات، قد تحتاج إلى إنشاء Effect خارج الـconstructor، ويمكنك هنا تمرير Injector إلى effect كخيار (Option)

<div dir="auto" align="left">

```typescript
@Component({...})
export class EffectiveCounterComponent {
  readonly count = signal(0);
  constructor(private injector: Injector) {}
  initializeLogging(): void {
    effect(() => {
      console.log(`The count is: ${this.count()}`);
    }, {injector: this.injector});
  }
}
```

</div>

### Destroying effects

الـEffects في Angular بيتم تدميرها تلقائيًا لما ينتهي المكان اللي اتسجلت فيه (زي الكومبوننت أو service). يعني لو عندك Effect معمول في كومبوننت، هيتدمر بشكل تلقائي لما الكومبوننت نفسه يتدمر.
نفس الكلام بينطبق على التوجيهات (directives) و (services).

في نفس الوقت، كل Effect بيرجع حاجة اسمها EffectRef، ودي بتديك القدرة على تدمير الـEffect يدويًا لو احتجت كده.
عن طريق استدعاء ()destroy على الـEffectRef، تقدر تنهي الـEffect وقت ما تحب.

 <div dir="auto" align="left">

```typescript
@Component({...})
export class ExampleComponent {
  private count = signal(0);
  private effectRef = effect(() => {
    console.log(`The count is: ${this.count()}`);
  }, { manualCleanup: true });

  ngOnDestroy() {
    this.effectRef.destroy();
  }
}
```

</div>
 ✨في المثال ده، الـEffect مش هيتدمر تلقائيًا، وإنت مسؤول عن تدميره يدويًا في الدالة ngOnDestroy للتأكد إنه مش هيبقى شغال بعد انتهاء الكومبوننت.
</div>

 <!-- <hr/>
 ## What is ng-content?

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
