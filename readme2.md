<!-- | No. | Questions                                                                                                  |
| --- | ---------------------------------------------------------------------------------------------------------- | --- |
| 59  | [What are dynamic components?](#what-are-dynamic-components)                                               |     |
| 70  | [What are router events?](#what-are-router-events)                                                         |
| 71  | [What is activated route?](#what-is-activated-route)                                                       |
| 72  | [How do you define routes?](#how-do-you-define-routes)                                                     |
| 73  | [What is the purpose of Wildcard route?](#what-is-the-purpose-of-wildcard-route)                           |
| 74  | [Do I need a Routing Module always?](#do-i-need-a-routing-module-always)                                   |
| 75  | [What is Angular Universal?](#what-is-angular-universal)                                                   | -->

<!-- ## What are dynamic components?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Dynamic Components هي components في Angular اللي مكانها مش بيتحدد في التطبيق وقت الـ Build، يعني مش بنستخدمها في أي Template ثابتة. الفكرة إنك بتعمل Instantiation للـ component دي وتضيفها في التطبيق وقت الـ Runtime. يعني بكل بساطة، بتحدد مكانها وطريقة عرضها وقت التشغيل مش وقت بناء التطبيق.

✨ مثال على كده، ممكن يكون عندك component مش عارف هيتعرض فين بالضبط، زي في Dialog، Popup، أو حتى جزء من الصفحة حسب تفاعل المستخدم أو رد من API. فبتستخدم الـ Dynamic Components عشان تضيف الـ component دي بشكل ديناميكي بناءً على اللي بيحصل في التطبيق وقت التشغيل.

ده بيكون مفيد جدًا لو عاوز تعمل تصميم مرن أو تعرض components معينة بناءً على ظروف أو اختيارات معينة للمستخدم.

</div>
<hr/>

## What are the various kinds of directives?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في عالم الـ Angular مثلاً، بنلاقي ٣ أنواع رئيسية من الـ Directives

### Components directives

دي عبارة عن directives بس معاها template. يعني بتتعامل كأنها حتة UI كاملة، زي ما تكون واجهة المستخدم اللي انت بتعرضها. الكمبوننتس دي بتحتوي على html و logic بتاعها. يعني تقدر تعتبرها مزيج ما بين شكل الصفحة والسلوك اللي فيها.

### Structural directives

دي بتشتغل على الـ DOM. بتغير في الـ layout بتاع الصفحة، يعني تقدر تضيف أو تشيل عناصر من الصفحة نفسها. مثال على كده عندنا الـ *ngIf أو الـ *ngFor اللي بتخلينا نتحكم في إذا كان العنصر يتعرض أو يتخفى أو يتكرر بناءً على شروط معينة.

### Attribute directives

النوع ده بيغير في شكل العنصر أو في الـ behavior بتاعه، زي الـ ngClass أو الـ ngStyle. دي بتتحكم في الخصائص أو الـ styles بتاعت العنصر اللي موجود في الـ DOM من غير ما تشيله أو تضيف عناصر جديدة.

</div>
<hr/>

## What are router events?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Router Events دي عبارة عن الأحداث اللي بتحصل لما الـ router في تطبيقك (زي في Angular مثلاً) بينقلك من صفحة للتانية.

يعني إيه؟ يعني لو إنت مثلاً فاتح صفحة "Home" وعايز تروح لصفحة "About"، الـ router ده هو اللي بيعمل التنقل ده. كل ما تتنقل من صفحة لصفحة، بيحصل شوية أحداث.

#### خلينا نبسطها أكتر:

١. NavigationStart: ده أول ما تبدأ تتحرك من صفحة للتانية، يعني كده بنقول إنك "بدأت التنقل".

٢. NavigationEnd: لما التنقل يخلص وتوصل للصفحة اللي رايح لها، الـ router بيقولك "التنقل خلص بنجاح".

٣. NavigationCancel: لو حصل حاجة وانت في النص، مثلاً أنت لغيت أو فيه مشكلة، يبقى كده التنقل "اتلغى".

٤. NavigationError: لو حصلت مشكلة وانت بتتنقل، زي مثلاً الصفحة مش موجودة أو السيرفر وقع، هنا بنقول "فيه خطأ".

٥. RoutesRecognized: هنا بقى الـ router بيقولك "أيوه أنا عرفت الصفحة اللي انت رايح لها ومستعد أروح لها".

✨الفكرة إنك ممكن تستفيد من الأحداث دي، زي إنك مثلاً تشغل loader (الحاجة اللي بتفضل تلف وانت مستني الصفحة تفتح) أول لما يبدأ التنقل، وبعد ما يخلص تخفيه. أو ممكن تعمل check لو فيه أخطاء في النص عشان تبلغ المستخدم إن في مشكلة.

يعني باختصار، الـ Router Events دي بتديك سيطرة على كل خطوة بتحصل وانت بتتنقل بين صفحات التطبيق.

</div>
<hr/>

## What is activated route?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الActivatedRoute في Angular زي اللي بيقولك إنت واقف فين في  (routes) بتاعت الأبليكيشن. يعني لو إنت فتحت صفحة معينة، هو اللي هيقولك كل التفاصيل بتاعت الصفحة دي، زي  (path) اللي إنت ماشي فيه، أو أي parameters اتحطت في ال URL، زي مثلا لو فتحت صفحة ب ID معين.
</div>
<hr/>

## How do you define routes?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
تعريف الـ Routes في Angular بيتم باستخدام الموديل RouterModule من خلال الطريقة RouterModule.forRoot. بتستخدم الطريقة دي عشان تحدد قائمة من المسارات اللي التطبيق بتاعك هيتعامل معاها. كل مسار (Route) بيبقى مرتبط بـ component معين، يعني لما المستخدم يدخل على المسار ده، الـ component المحدد بيتحمل ويظهر.
<div dir="auto" align="left">

```typescript
 const appRoutes: Routes = [
  { path: 'todo/:id',      component: TodoDetailComponent },
  {
    path: 'todos',
    component: TodosListComponent,
    data: { title: 'Todos List' }
  },
  { path: '',
    redirectTo: '/todos',
    pathMatch: 'full'
  },
  { path: '**', component: PageNotFoundComponent }
];

@NgModule({
  imports: [
    RouterModule.forRoot(
      appRoutes,
      { enableTracing: true } // <-- debugging purposes only
    )
    // other imports here
  ],
  ...
})
export class AppModule { }
```

</div>
</div>
 <hr/>

## What is the purpose of Wildcard route?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الغرض من الـ Wildcard route هو التعامل مع أي روابط (URLs) غير معروفة أو غير معرفة مسبقًا في التطبيق. يعني لو المستخدم دخل على رابط مش موجود في قائمة الـ routes اللي أنت معرفها، بدل ما التطبيق يرمي خطأ أو يتعطل، يتم توجيه المستخدم لصفحة مخصصة زي "صفحة غير موجودة" (Page Not Found).
<div dir="auto" align="left">

```typescript
{ path: '**', component: PageNotFoundComponent }
```

</div>

### '\*\*' path

دي معناها إن أي رابط ما اتعرفش في باقي المسارات هيتم التقاطه من المسار ده. الـ \*\* هو رمز الـ wildcard اللي بيمسك أي URL ما ينطبقش عليه أي من المسارات اللي قبله.

### component

الPageNotFoundComponent: هنا بتحدد الـ component اللي هيتعرض لما المسار يتحقق. في الحالة دي، صفحة الخطأ أو الصفحة اللي بتقول إن الرابط مش موجود.
✨الخلاصة: الـ Wildcard route بيضمن إن التطبيق مش هيكراش بسبب روابط غير معروفة وبيسمحلك تعرض رسالة أو صفحة مخصصة بدل من حدوث خطأ.
</div>
<hr/>

## What is Angular Universal?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
الAngular Universal ده ببساطة طريقة إنك تخلي تطبيق Angular بتاعك يشتغل بـ Server-Side Rendering (SSR)، يعني السيرفر هو اللي يولد الـ HTML بدل ما المتصفح يعمل كل حاجة. الطبيعي في تطبيقات Angular العادية إن كل حاجة بتتحمل في المتصفح (الـ HTML والـ JavaScript)، وده ممكن يخلي التحميل الأول للصفحة بطيء شوية خصوصًا على النت البطيء.

#### ليه بقى Angular Universal مهم؟

أداء أسرع: بدل ما المستخدم يقعد مستني لما الصفحة تتحمل بالكامل، السيرفر بيرسل له HTML جاهز أول ما يفتح التطبيق، فبيحس إن الصفحة ظهرت بسرعة.

تحسين الـ SEO: عشان محركات البحث زي جوجل تفهم محتويات الصفحات، لازم تلاقي HTML كامل أول ما تزور الصفحة. الـ SPA (Single Page Applications) زي Angular ممكن يكون عندها مشكلة في النقطة دي لأنها بتحتاج الجافاسكريبت يتنفذ الأول عشان يطلع المحتوى. لكن مع Angular Universal، الصفحة بتطلع بـ HTML جاهز، فمحركات البحث تقدر تقرأها وتحسن ترتيب الموقع.

تجربة أحسن على الشبكات البطيئة: المستخدمين اللي عندهم إنترنت بطيء هيتبسطوا إنهم يشوفوا الصفحة بسرعة من غير ما يقعدوا مستنيين تحميل كل حاجة.
</div>

## What is an Angular Service
## What Angular Services are used for
## Advantageous of Angular Service
<hr/> -->

<!-- ## What is an Angular Service

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ببساطة كده، الـ Services في Angular هي طريقة بنستخدمها علشان نكتب كود نقدر نستخدمه أكتر من مرة في كذا Component. يعني بدل ما نكرر نفس الكود في كل Component، بنكتب الكود ده مرة واحدة في Service ونستدعيه في أي Component يحتاجه.

طيب، إزاي بنستدعي الـ Service؟ بنعمل حاجة اسمها Dependency Injection، وده معناه إننا بنضيف الـ Service للـ Component أو لـ Service تانية عن طريق الـ constructor. Angular بتسهل لنا القصة دي باستخدام حاجة اسمها Providers، اللي بنحطها في الـ Module بتاعنا علشان تقول لـ Angular إن الـ Service دي متاحة للاستخدام في كل الـ Components اللي محتاجاها.

✨ النقطة التانية المهمة هي إن Angular بيبني حاجة اسمها Injector Tree. الفكرة إن لما يكون عندك (Components) كتيرة في التطبيق، Angular بيعمل شجرة Injectors علشان يعرف يوزع الـ Services دي بناءً على احتياجات كل Component. الطريقة دي اسمها Hierarchical Pattern، واللي معناها إن الـ Injectors بتتبنى بشكل شجري، زي ما الـ Components بتتبنى على شكل شجرة.

بالتالي، لو Component معين محتاج Service معينة، Angular هيدور عليها في أقرب Injector ليه في الشجرة. لو ملقهاش، هيكمل يدور لحد ما يطلع لفوق في الشجرة ويلاقيها.

#### لخلاصة: الـ Services بتوفر كود reusable، وAngular بتستخدم Dependency Injection مع نظام شجري من الـ Providers علشان توزع الـ Services دي في التطبيق كله بطريقة ذكية ومرتبة.

</div>

## What Angular Services are used for

[⬆️ Back to Top](#top)

1- Features that are independent of components such a logging services
2 -Share logic or data across components
3- Encapsulate external interactions like data access

## Advantageous of Angular Service

[⬆️ Back to Top](#top)

1- Services are easier to test.
2- They are easier to Debug.
3- We can reuse the service at many places.

## Benefits of Dependency Injection

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
بص، Dependency Injection هو أسلوب بنستخدمه عشان نخلي مكونات الـ Angular تشتغل مع بعضها بشكل مرن من غير ما تكون مرتبطة ببعضها بشكل مباشر. يعني إيه؟ يعني مثلاً عندنا مكون اسمه AppComponent وده محتاج يشتغل مع ProductService. في العادي، عشان الـ AppComponent يشتغل مع الـ ProductService، كان المفروض يبقى فاهم إزاي الـ ProductService بيتعمله إنشاء وبيشتغل، لكن هنا الفكرة في Dependency Injection إنه بيخلينا نمرر الـ ProductService للـ AppComponent من غير ما يبقى عارف تفاصيل إنشاؤه.

#### طيب إيه الفايدة؟

##### Loosely Coupled (غير مرتبط بشكل مباشر)

يعني الـ AppComponent مش مرتبط بالـ ProductService اللي انت بتديله. عادي ممكن تديله BetterProductService أو MockProductService من غير ما يعرف الفرق. هو مش محتاج يعرف كل التفاصيل.

##### Easier to Test (أسهل في الاختبار)

دلوقتي الاختبار بقى سهل. بما إن الـ AppComponent مش مرتبط بنوع معين من ProductService، فإنت ممكن تعمل mock للـ ProductService وتستخدمه في الاختبار من غير ما يبقى عندك مشاكل في الكود الأساسي.

##### إعادة استخدام الكود

دلوقتي بقى عندك component ممكن تعيد استخدامه في أماكن تانية بسهولة، لأن طالما الخدمة اللي بتشتغل مع component بتلتزم بالـ interface اللي محتاجه، خلاص مفيش مشكلة.

</div>

## There are five main players in the Angular Dependency injection Framework.

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ال Consumer

ده اللي هو الكلاس اللي محتاج الـ Dependency. يعني هو اللي عايز "الخدمة" أو "الـ Service" علشان يستخدمها في الكود بتاعه. وده ممكن يكون أي حاجة زي الـ Component أو الـ Directive أو حتى الـ Service تانية.

Dependency
الـ Dependency هو الحاجة اللي الـ Consumer محتاجها. يعني هي الـ Service اللي إحنا عايزين نحقنها في الـ Consumer

الInjection Token (DI Token)
ده حاجة زي "المفتاح" اللي بنستخدمه علشان نقول للـ Angular إحنا عايزين نحقن أي Dependency. كل Dependency لازم يبقى ليها حاجة بتحددها زي ID، علشان الـ Angular يعرف يلاقيها ويحقنها في الـ Consumer. يعني بنستخدم الـ DI Token علشان نسجل الـ Dependency بتاعتنا.

الProvider
ده الشخص اللي "بيوفر" الـ Dependencies. يعني عنده لستة بكل الـ Dependencies اللي بنستخدمها في الأبلكيشن بتاعنا، مع الـ Tokens بتاعتها. الـ Provider هو اللي بيستخدم الـ Token علشان يحدد الـ Dependency ويجهزها علشان الـ Consumer يقدر يستخدمها.

الInjector
ده هو المسؤول إنه يمسك الـ Providers ويشوف إيه الـ Dependency اللي الـ Consumer طالبها. بعد كده هو اللي بيعمل "إنشاء" للـ Dependency (يعني بيخلق instance منها) وبيحقنها في الـ Consumer. الـ Injector بيستخدم الـ DI Token علشان يدور على الـ Dependency ويحقنها في الكلاس اللي طالبها.

بمعنى تاني، لو انت في الـ Component بتاعك بتقول إنك محتاج "Service" معينة، الـ Injector بيدور في الـ Providers ويشوف الـ Service اللي انت طالبها ويبعتهالك.

</div>

## Service Scope

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
1- لما تيجي تعمل Service في الـAngular، لو وفرتها على مستوى الـ root module، ده معناه إن الـ service دي هتبقى متاحة في كل حتة في التطبيق. يعني أي component أو service تانية في التطبيق تقدر تستخدمها من غير مشاكل.

2- أما لو وفرت الـ service في مستوى الـ component نفسه، يبقى الـ service دي متاحة بس للـ component ده والـ child components اللي جواه. يعني لو في components برا مش هتقدر تستخدم الـ service دي.

3- لو وفرت الـ service دي في أي module تاني (غير الـ Lazy Loaded Module)، برضو هتبقى متاحة لكل التطبيق. يعني تقدر تستخدمها في أي حتة من المشروع بتاعك.

- الLazy Loaded Module هو module بيتم تحميله بس لما يبقى محتاجه، مش بيتحمل مع بداية التطبيق. عشان كده، الـ services اللي بتتوفر في الـ Lazy Loaded Module بتكون محصورة (scoped) جوا الـ module ده بس.

- يعني إيه الكلام ده؟ يعني لو أنت وفرت service معينة جوا Lazy Loaded Module، الـ service دي هتكون متاحة فقط للعناصر (components أو services) اللي موجودة جوا نفس الـ module ده. يعني لو في components أو services تانية موجودة في أجزاء تانية من التطبيق (مش موجودة جوه الـ Lazy Loaded Module) مش هتقدر تستخدم الـ service دي.

- ### مثال يوضح أكتر:
  لو عندك تطبيق كبير فيه Modules كتير، وليكن مثلاً:
  AdminModule
  UserModule
  لو عملت Lazy Loading للـ AdminModule ووفرت فيه service خاصة (مثلاً AdminService)، الخدمة دي هتبقى متاحة فقط في الـ AdminModule. لو حاولت تستخدمها في UserModule أو أي module تاني، مش هتشتغل ومش هتبقى متاحة هناك.

</div>

## What is Angular Injector

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

- الـ Angular Injector هو اللي بيقوم بإنشاء الـ dependency (يعني أي حاجة محتاجها الكومبوننت أو الخدمة عشان تشتغل) ويحقنها في الكومبوننت أو الخدمة اللي طالبة الحاجة دي.

- دلوقتي، عشان الـ Injector يعرف يجيب الـ dependency دي، بيشوف حاجة اسمها Injection Token. الـ Injection Token ده زي اسم أو علامة مميزة للـ dependency اللي انت طالبها. بعد كده، الـ Injector بيروح يبص في قائمة الـ Providers اللي هي المكان اللي بيحتفظ فيه Angular بطريقة إنشاء الـ dependency دي.

- الـ Provider ده بيحتوي على معلومات عن إزاي نعمل instance (نسخة جديدة) من الـ dependency دي. فاللي بيحصل إن الـ Injector أول ما يلاقي الـ Provider المناسب، بيعمل نسخة من الـ dependency دي، وبعد كده يحقنها في الكومبوننت أو الخدمة اللي محتاجاها.

✨ الموضوع زي لما تكون بتطلب خدمة معينة (زي سباك أو كهربائي)، والـ Injector هو الشخص اللي بيوصل الخدمة دي ليك، بس هو لازم يروح يدور في دليل الخدمات (اللي هو الـ Providers) عشان يلاقي الشخص المناسب (الـ dependency) اللي هيعمل الخدمة المطلوبة.

</div>

## When is Angular Injector is created

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ببساطة كده، لما بنقول إن Angular بيشتغل، بيبدأ بإنه يخلق حاجتين أساسيتين زي الشجر:
واحدة اسمها ModuleInjector tree للتعامل مع الـ Modules، وواحدة تانية اسمها ElementInjector tree للتعامل مع العناصر زي الـ Components والـ Directives.

### أول حاجة بتحصل عند الـ Bootstrap

لما البرنامج بيبدأ (الـ bootstrap)، Angular بيحمل أول حاجة Root Module اللي هي AppModule. الموديول ده بيبقى زي الأصل اللي كل حاجة بعد كده هتتحمل منه. مع تحميله، Angular بيخلق حاجة اسمها RootModule Injector. ده المسؤول عن البرنامج كله، وبنقول عليه الـ application-wide scope، يعني ينفع يستعمل أي حاجة في أي حتة في التطبيق.

### بعد كده بيجي دور الـ Components

لما Root Module يخلص تحميل، يروح يجيب الـ AppComponent اللي هو أهم Component في التطبيق لأنه الأب لكل الـ Components اللي بعد كده. مع كل Component بيتخلق Injector خاص بيه، فالـ AppComponent بيأخذ حاجة اسمها root Injector ودي اللي بتبقى جذر شجرة الـ ElementInjector tree اللي هي للشغل الخاص بالـ Components.

### إزاي بيتكون باقي الـ Injectors؟

كل Component تحت AppComponent بيبقى ليه أولاده من الـ Components، وكل واحد فيهم برضه بياخذ Injector خاص بيه. فكل ما التطبيق يكبر ويتفرع، الـ Injectors بتكبر وتتفرع بنفس الطريقة في شجرة موازية للـ Components tree، وده اللي بنسميه شجرة الـ ElementInjector.

#### باختصار، عندك شجرتين:

- الModuleInjector tree للتعامل مع الموديولز.
- الElementInjector tree اللي بتوازي شجرة الـ Components وبتبني Injectors ليهم.

✨ الموضوع ده بيساعد Angular إنه ينظم استدعاء الـ Dependencies بشكل سليم ويوفرها في الأماكن الصح.

</div>

## Registering the service with injector

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ببساطة كده، في Angular لما بتيجي تضيف Service في التطبيق، بيكون في حاجة اسمها Injector هو اللي بيقوم بعملية إدارة وإضافة الـ Service في المكان الصح في التطبيق. ده بيتم عن طريق حاجة اسمها Providers، ودي بتسجل الخدمات اللي انت عاوز تستخدمها.

### إزاي بتسجل الـ Service؟

لو سجلت الـ Service في الـ Module:

ده معناه إن الخدمة دي هتكون متاحة في كل مكان في التطبيق. يعني لو أنت ضفت الـ Service بتاعتك في الـ Providers بتاعة الـ NgModule@، هتكون متاحة في كل المكونات (components) وكل الحتت اللي في المشروع.

<div dir="auto" align="left">

```typescript
providers: [ProductService, LoggerService];
```

</div>
لو سجلت الـ Service في Component

في الحالة دي، الخدمة هتكون متاحة بس للمكون ده (Component) وأي مكونات (Components) بتكون جواه أو تابعاله. يعني هيكون ليها نطاق أصغر.

### استخدام providedIn مع الـ Injectable:

في طريقة تانية لتسجيل الـ Service وهي باستخدام الـ providedIn جوه الـ Injectable@. دي تعتبر طريقة مريحة لأنك بتسجل الـ Service بشكل مباشر في المكان اللي هي متعرفة فيه، وغالباً بنستخدم providedIn: 'root' علشان تكون الخدمة متاحة للتطبيق كله من غير ما نضيفها في الـ Module بشكل صريح.

<div dir="auto" align="left">

```typescript
@Injectable({
  providedIn: "root",
})
export class ProductService {}
```

</div>
 ✨ده معناه إن الـ ProductService متاحة للتطبيق كله من غير ما تضيفها في الـ Providers بتاعة الـ Module.

### وظيفية الـ Injectable

دي Decorator لازم تضيفها على أي خدمة علشان Angular يعرف إنه يقدر يعمل Inject للخدمة دي في (components) اللي محتاجاها. لما تستخدم Injectable@، Angular بيدير العملية دي ويقدر يجيب الخدمات اللي Component محتاجها ويضيفها أوتوماتيكي.

</div>

## What are Angular Providers?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Angular Provider هو زي تعليمات أو وصفة بنقول فيها للـ Angular إزاي ينشئ  (Object) معين بناءً على حاجة اسمها Token. الفكرة كلها إن كل خدمة (Service) أو Dependency عايز تستدعيها في التطبيق بتحتاج تكون متسجلة في الـ Providers Array عشان الـ Angular يعرف يجيبها ويستخدمها لما تحتاجها في الكود.

### إزاي بنسجل الـ Providers؟

في طريقتين أساسيين علشان تسجل الخدمة في الـ Providers:

- إنك تضيفها مباشرة في الـ Providers array سواء في NgModule@ لو عايزها على مستوى التطبيق كله، أو في Component@ أو Directive@ لو عايزها على مستوى مكون معين.

- أو إنك تستخدم خاصية providedIn في الـ Injectable@ decorator. ودي طريقة تانية أسهل شوية لأنك بتقول للـ Angular إن الخدمة دي متاحة على مستوى التطبيق كله (Root) أو على مستوى موديول معين (Module).

### الفكرة بتمشي إزاي؟

لما الـ Angular بيشغل التطبيق، بيعمل حاجة اسمها Injector. الـ Injector ده مسؤول عن إنه يجيبلك الكائنات أو الـ dependencies اللي محتاجها الكود. فيه Root-level Injector بيبقى شغال على مستوى التطبيق كله، وبيبقى فيه Module-level Injector لو عندك Lazy Loaded Modules (ودي أجزاء من التطبيق بتتحمل بس لما تحتاجها).

</div>

## The Types of Provider ?

[⬆️ Back to Top](#top)

### The Angular Dependency Injection provides several types of providers.

1- Class Provider : useClass
2- Value Provider: useValue
3- Factory Provider: useFactory
4- Aliased Class Provider: useExisting

<div dir="auto" align="right">

### 1- الClass Provider - useClass

يعني إيه؟: لما بنستخدم الـ useClass بنقول للـ Angular يعمل إنستنس جديدة (instance) من كلاس معين، وده زي ما بنستخدم الكلمة المفتاحية new لإنشاء كائن من الكلاس.
إزاي نستخدمها؟: لو عندك كلاس اسمه ProductService وعايز توفر إنستنس منه في التطبيق:

<div dir="auto" align="left">

```typescript
providers: [{ provide: ProductService, useClass: ProductService }];
```

</div>
في الكود ده، ProductService هو الـ token اللي بيستخدمه الـ Angular علشان يتعرف على الخدمة اللي محتاج يوفرها. والـ useClass بتخلي الـ Injector يعمل instance جديدة من ProductService.

### فايدتها إيه؟

فايدة الطريقة دي إنك تقدر بسهولة تبدل الكلاس الأصلي بكلاس تاني (مثلاً كلاس فيك للاختبارات). ده مفيد جدًا في unit testing لما مش عايز تتعامل مع البيانات أو العمليات الحقيقية، وبدلها بتستخدم بيانات وهمية.

<div dir="auto" align="left">

```typescript
providers: [{ provide: ProductService, useClass: FakeProductService }];
```

</div>

### 2 - الValue Provider - useValue

يعني إيه؟: هنا بنستخدم useValue عشان نوفر قيمة ثابتة مش خدمة أو كلاس، يعني مثلاً لو عايز توفر URL أو إعدادات عامة.

<div dir="auto" align="left">

```typescript
providers: [{ provide: "USE_FAKE", useValue: true }];
```

</div>
ولما تيجي تستدعيها في الـ Component
<div dir="auto" align="left">

```typescript
constructor(@Inject('USE_FAKE') public useFake: boolean) {}
```

</div>

### 3-الFactory Provider - useFactory

بنستخدم useFactory لما نحتاج نرجع قيمة أو object بعد تنفيذ function. يعني لو عايز ترجع قيمة بناءً على شرط معين.

<div dir="auto" align="left">

```typescript
providers: [{ provide: "GREETING", useFactory: () => "Hello World" }];
```

</div>
وتستدعيها بعدين:
<div dir="auto" align="left">

```typescript
constructor(@Inject('GREETING') public greetingFunc: any) {
  console.log(greetingFunc());
}
```

</div>
كرة الـ Factory إنك بتقدر تتحكم أكتر في اللي بيرجع من function بناءً على شروط معينة، ودي حاجة بنستخدمها كتير في حالة مثلاً الإعدادات اللي بتتغير حسب البيئة (production أو development).

### 4- الAliased Class Provider - useExisting

بنستخدم useExisting لما عايزين نوفر نفس الإنستنس بتاعت كلاس تاني، يعني بدل ما نعمل إنستنس جديدة، نستخدم إنستنس موجودة بالفعل.

<div dir="auto" align="left">

```typescript
providers: [{ provide: "ExistingService", useExisting: ProductService }];
```

</div>
كده بنستخدم نفس الإنستنس اللي اتعملت للـ ProductService تحت اسم جديد هو ExistingService.

✨ ببساطة، لما تيجي تستدعي الـ Service اللي استخدمت فيها useExisting، تقدر تستدعيها باستخدام الـ Token اللي حطيته في الـ provide.

<div dir="auto" align="left">

```typescript
constructor(@Inject('ExistingService') private productService: ProductService) {}
```

</div>
</div>

## How Dependency Injection & Resolution Works in Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
بص، في Angular بيشتغل بنظام حاجة اسمها Dependency Injection (DI)، واللي معناها باختصار إنك بدل ما تبني كل حاجة من الصفر في كل Component أو Service، Angular هو اللي بيوفر الحاجات اللي محتاجها (Dependencies) بشكل أوتوماتيكي عن طريق Injector.

### 1. Injector
الـ Injector ده هو المسئول إنه يجيب الـ Dependency اللي أي Component أو Service محتاجها. يعني لو عندك Service معينة وعايز تستخدمها في Component، مش هتعمل new بنفسك، لكن هتعتمد على الـ Injector إنه هو اللي يعملها لك.

### 2. Injector Tree (شجرة الـ Injectors)
في الحقيقة، Angular مش بيعمل Injector واحد بس. لأ، هو بيعمل Injector Tree (شجرتين في الحقيقة، واحدة للـ Modules وواحدة للـ Elements زي Components وDirectives).

- الModule Injector Tree: الشجرة دي خاصة بالـ Modules زي Root Module أو أي Lazy Loaded Module.
- الElement Injector Tree: دي خاصة بالـ Components والـ Directives اللي بتتعامل مع الـ DOM.

### 3. Module Injector Tree
الModule Injector بيتبني لما التطبيق بيبدأ، وبيحتوي على كل الـ Providers اللي أنت معرفها في الـ Module.
فيه طريقتين عشان تسجل الـ Providers على مستوى الـ Module
تحطهم في providers بتاع الـ NgModule@
تستخدم providedIn: 'root' في الـ Injectable@ عشان تعمل الـ Service متاحة في كل التطبيق.

### 4. Dependency Resolution
لما الـ Component يطلب Service معينة، Angular بيشوف الأول الـ Injector بتاع الـ Component نفسه، لو لقاها بيجبها، لو ملقهاش، بيطلع لفوق للـ Injectors الأعلى (زي بتاع الـ Module أو حتى الـ Root Injector) لحد ما يلاقي الـ Dependency المطلوبة. لو ملقهاش خالص، بيرجع Error.

### 5. Null Injector
في أعلى شجرة الـ Injectors، Angular بيعمل حاجة اسمها Null Injector، اللي دايماً بترمي Error لو حاولت تجيب منها حاجة مش موجودة، إلا لو كنت حاطط عليها الـ Optional@ عشان ماترميش Error.

### مثال على الـ Hierarchical Dependency Injection
مثال بسيط لو عندك Module معين بيستخدم Service، تقدر تحط الـ Service دي في providers بتاع الـ NgModul@، ساعتها الـ Injector اللي خاص بالـ Module ده بس هو اللي هيجيب الـ Service. ولو عايزها متاحة في كل التطبيق، تحط providedIn: 'root

![Hierarchical Dependency Injection](https://www.tektutorialshub.com/wp-content/uploads/2021/05/Module-Injector-Tree-Hierarchy-2.png)
</div>


## Element Injector Tree?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

- ببساطة، شجرة Element Injector في Angular بتُستخدم علشان توفر الـ services على مستوى العناصر زي Components و Directives. لما التطبيق بيبدأ، Angular بيبني شجرة Injectors دي بحيث كل عنصر في التطبيق سواء كان Component أو Directive يكون ليه Injector خاص بيه.

- أول Injector بيتعمل هو بتاع Root Component، وده اللي بيبقى بمثابة الأب لكل العناصر اللي بعد كده. كل عنصر في التطبيق ممكن يبقى له عناصر تانية بداخله، وده بيخلق شجرة من العناصر وكل عنصر ليه Injector خاص بيه.
- ببساطة، كل Injector في Angular بياخد الـ Providers من الـ Component@ أو Directive@ اللي بيكون مربوط بيه. بمعنى، لو عندك Component معين فيه قائمة من services أو dependencies محتاجة تكون متاحة، Angular بيستخدم الـ providers الموجودة في الـ Component@ علشان يوفرها للـ Injector.

- لكن لو الـ Component@ أو Directive@ مش بيحتوي على أي Providers (يعني القائمة فاضية)، Angular بيعمل Injector، لكنه بيبقى فاضي، ومش بيحتوي على أي خدمات أو services متاحة للعنصر ده.

- لما ينتهي عمر العنصر أو الـ component (يعني لما يتم إزالته من الـ DOM أو يخلص دورة حياته)، Angular بيتخلص من الـ Injector اللي مرتبط بيه علشان يحرر الذاكرة ويحسن الأداء.

### الهرمية بتاعة Element Injector Tree

- لو عندك Component بيطلب Service معينة في الـ constructor، Angular بيبدأ يدور على الـ dependency دي في الـ Injector اللي خاص بالـ component نفسه. لو لقاها، بيحقنها جوه الـ Component. لو مش لقاها، بينادي على الأب بتاع الـ Component ويدور في الـ Injector بتاعه.


- لو في النهاية مش لقى الـ dependency في شجرة الـ Element Injector كلها، يبدأ يدور في شجرة الـ Module Injector، والبحث يبدأ من الـ Root Module Injector (أو Lazy Loaded Module Injector لو بتستخدم lazy loading).

</div>

 ## ProvidedIn root, any & platform in Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

### 1. ال providedIn: 'root'
لو عندك  (Service) وعايزها تكون متاحة لكل التطبيق كله (بما في ذلك كل Components والكود اللي بتم تحميله سواء Lazy أو Eager)، تقدر تستخدم providedIn: 'root'. ده معناه إن Service دي هتكون singleton يعني موجودة بنسخة واحدة في كل التطبيق.
الفكرة هنا إن لو Service دي متمتش استخدامها في أي مكان في التطبيق، Angular هيشيلها من الملف النهائي عشان يحافظ على حجم التطبيق خفيف.

### 2- Lazy Loaded Service
لو عايز Service تكون متاحة بس في module معين ومش على مستوى التطبيق بالكامل، ممكن تضيفها في الـ providers بتاع الموديول ده فقط. في الحالة دي، Service هتكون singleton بس جوه الموديول ده، يعني مش هتتشارك مع باقي الموديولات أو التطبيق.

- ### ماذا يحدث لو استخدمت الطريقتين؟
 - لو قمت بتسجيل Service باستخدام الطريقتين (يعني حطيت providedIn: 'root' وفي نفس الوقت أضفتها في الـ providers لموديول معين):

- هتكون  singleton Service على مستوى التطبيق كله، ما عدا في الموديول اللي سجلتها فيه في الـ providers، لأنه هيكون عنده نسخة جديدة منفصلة عن باقي التطبيق. ده بيدي كل موديول القدرة إنه يستخدم نسخة خاصة بيه من Service من غير ما يشاركها مع موديولات تانية.


### 3. providedIn: 'any'
ده بقى مختلف شوية. لو عندك أكتر من lazy-loaded module وكل موديول محتاج نسخة خاصة بيه من الخدمة، تستخدم providedIn: 'any'. يعني كل lazy-loaded module هيكون عنده نسخة جديدة من الخدمة دي.
لكن eager-loaded modules (اللي بتتحمل في أول التطبيق) هيفضلوا يستخدموا النسخة اللي في Root Module Injector زي العادي.

### 4. providedIn: 'platform'
دي بقى للناس اللي بتعمل حاجات أكتر تعقيدًا. لما عندك أكتر من تطبيق Angular شغالين على نفس الصفحة، ومحتاج خدمة تكون مشتركة بينهم كلهم، تستخدم providedIn: 'platform'.
الـ Platform Injector هو الأب بتاع Root Module Injector، يعني أي خدمة بتتحط هنا تبقى متاحة لكل التطبيقات اللي شغالة في الصفحة.
مفيد جدًا لما تكون بتستخدم حاجة زي Angular Elements عشان تشارك نفس الخدمة بين العناصر المختلفة اللي شغالة على نفس الصفحة.
</div>

## @Self, @SkipSelf & @Optional Decorators Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
في Angular، فيه ديكوراتورز معينة زي Self@، SkipSelf@، و Optional@ بتتحكم في إزاي Angular بيدور على الdependencies اللي بيحتاجها عشان يعمل Dependency Injection.

### 1- Self@
الديكوراتور ده بيقول لـ Angular يدور على الـ dependency اللي انت محتاجها فقط في المكان اللي انت حقنت فيه الـ dependency. بمعنى إن لو فيه component أو service معين وحقنت فيه dependency وكنت مستخدم Self@، Angular مش هيبص في الأماكن الأعلى (الـ parent injectors) عشان يجيب الـ dependency دي، لو مش لقاها في المكان المحدد، هيطلع error.

##### مثال: لو انت بتقول لـ Angular: "ادور على الـ Service دي في نفس الـ component ده، ومش عايزك تبص في أي مكان تاني."
<div dir="auto" align="left">

```typescript
constructor(@Self() private myService: MyService) { }
```

</div>
✨ لو ما لاقاش الـ MyService في نفس المكان ده، هيحصل error.

### 2. SkipSelf@
الديكوراتور ده بيعمل العكس. هو بيقول لـ Angular "أنا عايز الـ dependency دي، بس متدورش عليها في نفس الـ injector اللي فيه الـ component ده، دور عليها في الـ parent injectors بس." يعني بيتخطى (skip) المكان الحالي ويروح يدور في الأماكن الأعلى (الـ parent injectors).

##### مثال: لو عايز تعتمد على service موجودة في مكان أعلى من الـ component اللي انت فيه، تقدر تستخدم SkipSelf@
<div dir="auto" align="left">

```typescript
constructor(@SkipSelf() private myService: MyService) { }
```

</div>
✨ هنا Angular هيبص في الـ parent injector ولو لقى الـ MyService هناك، هيحقنه، لو مش لاقيها في الـ parent برضه هيطلع error.

### 3.Optional@
الديكوراتور ده بيقول لـ Angular "لو لقيت الـ dependency اللي بطلبها، حقنها عادي، ولو ملقتهاش، متطلعش error." يعني ببساطة بـ Optional@، Angular بيعمل الموضوع ده اختياري، وبيسيب الـ dependency بـ null لو ملقهاش.

##### مثال: لو انت مش متأكد لو الـ MyService موجودة ولا لأ، بس مش عايز تطلع error لو مش موجودة، تقدر تستخدم Optional@

<div dir="auto" align="left">

```typescript
constructor(@Optional() private myService: MyService) { }
```

</div>
✨ في الحالة دي، لو Angular ملقاش الـ MyService، مش هيطلع error وهيخلي myService بـ null.

#### مثال توضيحي لكل الأنواع
<div dir="auto" align="left">

```typescript
constructor(
  @Self() private serviceA: ServiceA,  // لازم يلاقيها في نفس المكان
  @SkipSelf() private serviceB: ServiceB,  // متدورش عليها هنا، بس دور في اللي فوق
  @Optional() private serviceC: ServiceC  // لو ملقتهاش متطلعش error
) { }
```

</div>
</div> -->

 <!-- <hr/>
 ## How do you define routes?

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
