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
<hr/> -->

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
