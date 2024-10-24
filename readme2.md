<!-- <a name="top"></a>

# Angular Interview Questions

| No. | Questions                                                                                                            |
| --- | -------------------------------------------------------------------------------------------------------------------- |
| 1   | [What is Angular Framework?](#what-is-angular-framework)                                                             |
| 3   | [What is TypeScript?](#what-is-typescript)                                                                           |
| 4   | [Write a pictorial diagram of Angular architecture?](#write-a-pictorial-diagram-of-angular-architecture)             |
| 5   | [What are the key components of Angular?](#what-are-the-key-components-of-angular)                                   |
| 6   | [What are directives?](#what-are-directives)                                                                         |
| 7   | [What are components?](#what-are-components)                                                                         |
| 9   | [What is a template?](#what-is-a-template)                                                                           |
| 10  | [What is a module?](#what-is-a-module)                                                                               |
| 11  | [What are lifecycle hooks available?](#what-are-lifecycle-hooks-available)                                           |
| 12  | [What is a data binding?](#what-is-a-data-binding)                                                                   |
| 13  | [What is metadata?](#what-is-metadata)                                                                               |
| 14  | [What is Angular CLI?](#what-is-angular-cli)                                                                         |
| 15  | [What is the difference between constructor and ngOnInit?](#what-is-the-difference-between-constructor-and-ngoninit) |
| 16  | [What is a service?](#what-is-a-service)                                                                             |
| 17  | [What is dependency injection in Angular?](#what-is-dependency-injection-in-angular)                                 |
| 18  | [What is the purpose of async pipe?](#what-is-the-purpose-of-async-pipe)                                             |
| 19  | [What is the purpose of \*ngFor directive?](#what-is-the-purpose-of-ngfor-directive)                                 |
| 20  | [What are pipes?](#what-are-pipes)                                                                                   |
| 21  | [What is a parameterized pipe?](#what-is-a-parameterized-pipe)                                                       |
| 22  | [How do you chain pipes?](#how-do-you-chain-pipes)                                                                   |
| 23  | [What is a custom pipe?](#what-is-a-custom-pipe)                                                                     |
| 24  | [What is the difference between pure and impure pipe?](#what-is-the-difference-between-pure-and-impure-pipe)         |
| 25  | [What is HttpClient and its benefits?](#what-is-httpclient-and-its-benefits)                                         |

## What is Angular Framework?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Angular Framework هو منصة مفتوحة المصدر معتمدة على TypeScript، وبيستخدموها عشان يبنوا تطبيقات ويب، موبايل، وديسكتوب بكل سهولة. من أهم المميزات اللي بيوفرها الفريم وورك ده هي الـ declarative templates، ودي بتسهل الكتابة والتصميم. كمان فيه الـ dependency injection اللي بيخلي إعادة استخدام الكود والمرونة في الشغل أسهل. بالإضافة لكده، عندك أدوات شاملة من البداية للنهاية end to end tooling اللي بتسهل تطوير التطبيقات بشكل كبير.
</div>
<hr/>

## What is TypeScript?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
ال TypeScript هو نسخة محسنة من JavaScript عملتها مايكروسوفت، والمميز فيه إنه بيضيف أنواع متغيرة (types) إلزامية زي الـ string و number، وكمان بيدعم حاجات زي الـ classes، والـ async/await، وميزات تانية كتير. وبعدين بيتحول الكود المكتوب بـ TypeScript إلى كود عادي مكتوب بـ JavaScript اللي كل المتصفحات بتفهمه.
الـ Angular كله متبني الـ TypeScript كلغة رئيسية.

### مثال بسيط لاستخدام TypeScript

<div dir="auto" align="left">

```typescript
function greeter(person: string) {
  return "Hello, " + person;
}

let user = "mohamed";

document.body.innerHTML = greeter(user);
```

</div>

في المثال ده، الـ greeter function مش بتقبل غير المتغيرات اللي نوعها string بس كـ argument، وده مثال على قوة TypeScript في تحديد نوع المتغيرات.

</div>
<hr/>

## Write a pictorial diagram of Angular architecture?

[⬆️ Back to Top](#top)

The main building blocks of an Angular application are shown in the diagram below:-

![alt text](./images/architecture.png)

<hr/>

## What are the key components of Angular?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### المكونات الأساسية في Angular بتشمل الحاجات دي:

#### Component

ال(Components) في Angular زي الطوب اللي بتبني بيه التطبيق بتاعك، كل Component مسؤول عن جزء معين من الصفحة اللي بتظهر للمستخدم. يعني هو اللي بيقول الـ HTML يتعرض إزاي ويشتغل إزاي. زي مثلاً لو عندك صفحة تسجيل دخول، الComponent هو اللي هيتحكم في الشكل والأزرار وكل حاجة بتظهر في الجزء ده.

#### Modules

في Angular هي عبارة عن مجموعة من Components Angular الأساسية زي الـ Components، والـ Directives، والـ Services وغيرها. التطبيق بيتقسم لقطع منطقية، وكل قطعة بتتسمى "Module" وبتقوم بمهمة واحدة محددة.

#### Templates

ال(Templates) في Angular زي الرسمة اللي بتقول Component يعرض إيه بالظبط. يعني هي اللي بتحدد الشكل اللي المستخدم هيشوفه، زي الأزرار، النصوص، والصور. Template ده بيبقى مليان كود HTML، بس ممكن كمان يكون فيه حاجات ديناميكية بتتغير حسب اللي بيحصل في التطبيق. يعني باختصار، Template هو اللي بيرسم شكل الواجهة اللي هتشوفها قدامك.

#### Services

دي زي حاجات بتعملها مرة واحدة وتقدر تستخدمها في أي حتة في التطبيق بتاعك. يعني لو عندك شغلانة معينة وعايز تعملها في كذا مكان، مش هتعيد الكود كل مرة، بتعملها كـ "Service" وتستخدمها في أي حتة.

#### Metadata

دي زي شوية معلومات إضافية بتضيفها على الكلاس عشان تخليه يشتغل بشكل معين في Angular. يعني زي ما تكون بتدي توجيهات زيادة للكلاس ده، عشان Angular يفهمه بطريقة أحسن.

</div>

<hr/>

## What are directives?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الDirectives في Angular هي زي تعليمات بتضيف تصرفات أو سلوكيات جديدة لعناصر الـ DOM اللي موجودة في الصفحة، أو حتى لComponent موجود بالفعل.
<div dir="auto" align="left">

```typescript
import { Directive, ElementRef } from "@angular/core";

@Directive({ selector: "[myHighlight]" })
export class HighlightDirective {
  constructor(el: ElementRef) {
    el.nativeElement.style.backgroundColor = "yellow";
  }
}
```

</div>
الكود ده بيعمل Directive اسمه myHighlight، وكل اللي بيعمله إنه بيغير لون الخلفية لأي عنصر HTML للون الأصفر. يعني مثلاً لو عندك فقرة (paragraph) وعايز تديها خلفية صفراء، هتكتب كود بالشكل ده:

<div dir="auto" align="left">

```HTML
<p myHighlight>Highlight me!</p>
```

</div>

</div>
<hr/>

## What are components?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في Angular، الـ Components تعتبر الوحدة الأساسية اللي بتستخدم عشان تبني واجهة المستخدم (UI). كل Component بيكون مسؤول عن جزء معين من الصفحة أو الواجهة. يعني مثلاً ممكن يكون عندك Component مسؤول عن عرض الـ header  وComponent تاني مسؤول عن عرض قائمة المنتجات، وهكذا.

الـ Components دي بتشتغل مع بعض وبتتجمع عشان تبني التطبيق كله، وعشان كده بنقول إنها بتكون شجرة من الـ Components، يعني كل Component ممكن يكون جواه Components تانية أصغر. زي ما يكون عندك صفحة فيها أجزاء مختلفة وكل جزء فيه تفاصيله الخاصة.

#### نيجي بقى للفرق بين الـ Component والـ Directive:

الComponent هو نوع من الـ Directives، بس الفرق الأساسي هو إن الـ Component لازم يكون ليه template، يعني لازم يعرض حاجة للمستخدم زي نصوص، صور، أزرار... إلخ.

في المقابل، الـ Directive العادي مش لازم يكون ليه template، وممكن يستخدم بس عشان يضيف أو يعدل سلوك عنصر HTML موجود. يعني بيغير في العنصر من غير ما يعرض محتوى جديد.

#### باختصار

الComponent بيكون ليه template وبيعرض حاجة للمستخدم.
كل تطبيق Angular بيتكون من مجموعة Components بتشتغل مع بعض زي شجرة.
الفرق الأساسي بين Component و Directive هو إن الأول بيعرض واجهة (UI) والثاني بس بيغير أو يضيف سلوك للعناصر اللي موجودة.

</div>
<hr/>

## What is a template?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ template في Angular هو ببساطة العرض اللي بيتشوف للمستخدم على هيئة HTML، وبتقدر تعرض فيه بيانات عن طريق ربط العناصر اللي في الـ HTML بالبيانات اللي جوا الـ Component. بمعنى تاني، الـ template هو المكان اللي بتعرض فيه البيانات اللي بيكون جوا الـ Component.

#### الـ template ممكن تخزنه في مكانين

##### Inline Template

يعني إنك تكتب كود الـ HTML مباشرة جوا الـ Component باستخدام الخاصية template. ده مناسب لو عندك HTML بسيط.

##### External Template

يعني إنك تخزن الـ template في ملف HTML منفصل وتربطه بالـ Component باستخدام templateUrl. ده بيكون مناسب لما يكون عندك HTML كبير أو معقد.

##### مثال على Inline Template

 <div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "my-app",
  template: `
    <div>
      <h1>{{ title }}</h1>
      <div>Learn Angular</div>
    </div>
  `,
})
export class AppComponent {
  title: string = "Hello World";
}
```

</div>
في المثال ده، كل كود الـ HTML مكتوب مباشرة جوه الـ Component عن طريق الخاصية template. وهنا بيتم ربط المتغير title اللي جوا الـ Component بالـh1  عن طريق {{}}، وده اسمه interpolation.

##### مثال على External Template

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "my-app",
  templateUrl: "app/app.component.html",
})
export class AppComponent {
  title: string = "Hello World";
}
```

</div>
في الحالة دي، كود الـ HTML بيكون موجود في ملف خارجي اسمه app.component.html، وبتربطه بالـ Component عن طريق templateUrl. وده مفيد لو عندك templates معقدة أو كبيرة عشان تبقى الصفحة أسهل في التنظيم والصيانة.
</div>
<hr/>

## What is a module?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Modules في Angular بتعمل زي الحدود المنطقية في التطبيق بتاعك، وبتقسم التطبيق لأجزاء منفصلة عشان كل جزء يقوم بوظيفة معينة. الفكرة الأساسية هي إنك تقسم الكود لموديولات (Modules) عشان تبقى الأمور منظمة وسهلة في الإدارة.

خلينا ناخد مثال على الملف app.module.ts، اللي هو الموديول الرئيسي في التطبيق، وبيتم الإعلان عنه باستخدام @NgModule decorator

<div dir="auto" align="left">

```typescript
import { NgModule } from "@angular/core";
import { BrowserModule } from "@angular/platform-browser";
import { AppComponent } from "./app.component";

@NgModule({
  imports: [BrowserModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent],
  providers: [],
})
export class AppModule {}
```

</div>
في المثال ده، عندنا الـ @NgModule اللي بيوفر شوية خيارات مهمة، وأهمها

##### imports

دي بتستخدم عشان تستورد موديولات تانية محتاجها في التطبيق. في المثال ده، بنستورد BrowserModule اللي بيكون مطلوب لأي تطبيق ويب في Angular.

##### declarations:

دي بتستخدم عشان تعلن عن الـ Components اللي موجودة في الموديول ده. هنا بنعلن عن AppComponent.

##### bootstrap

دي بتقول لـ Angular أي Component هو اللي هيبدأ تشغيل التطبيق. في الحالة دي، AppComponent هو اللي بيبدأ تشغيل التطبيق.

##### providers

بتستخدم عشان تحدد الحاجات اللي تقدر تعمل لها حقن (Injectable objects) في أجزاء مختلفة من التطبيق. يعني لو عندك (Services) معينة وعايز كل أجزاء التطبيق تقدر تستعملها، بتحطها في المكان ده. مثلاً، لو عندك Service بتجيب بيانات من سيرفر، بتقدر تحطها في الـ providers عشان أي Component في التطبيق يقدر يستخدمها من غير ما تضطر تعيد الكود في كل مكان.

الـ Modules بشكل عام بتساعد في تقسيم الوظائف بشكل منطقي في التطبيق وبتسهل تنظيم الكود وإعادة استخدامه.

</div>
<hr/>

## What are lifecycle hooks available?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Lifecycle hooks في Angular هي مجموعة من المراحل أو العمليات اللي بيمر بيها الـ Component أو الـ Directive من لحظة إنشاؤه لحد ما يتم تدميره.
Angular بيوفر مجموعة من الدوال اللي بتتفاعل مع كل مرحلة من مراحل الحياة دي.

![alt text](./images/lifecycle.png)

#### دي قائمة بأهم lifecycle hooks المتاحة في Angular:

##### ngOnChanges

بيتنفذ لما يحصل تغيير في قيمة أي خاصية مربوطة بالبيانات (data bound property). يعني كل ما تتغير بيانات الـ Component بيتنفذ الكود ده.

##### ngOnInit

بيتنفذ أول ما يتم تهيئة (initialize) الـ Component أو الـ Directive بعد ما Angular يعرض الخصائص اللي مربوطة بالبيانات لأول مرة.

##### ngDoCheck

بيتنفذ عشان يكتشف أي تغييرات Angular مش قادر يكتشفها لوحده، وبيخليك تعمل أي حاجات إضافية لو فيه تغييرات معينة محتاج تتعامل معاها يدوي.

##### ngAfterContentInit

بيتنفذ بعد ما Angular يعمل (project) للمحتوى الخارجي جوا الـ Component.

##### ngAfterContentChecked

بيتنفذ بعد ما Angular يتأكد من المحتوى اللي تم إسقاطه جوا الـ Component، يعني بيتشيك على المحتوى اللي جوا الـ Component بعد ما يتم عرضه.

##### ngAfterViewInit

بيتنفذ بعد ما Angular يهيئ (initialize) الـ Views الخاصة بالـ Component وأي Child Components (الأطفال اللي جواه).

##### ngAfterViewChecked

بيتنفذ بعد ما Angular يتأكد من الـ Views الخاصة بالـ Component وأي Child Components.

##### ngOnDestroy

ده بيكون المرحلة الأخيرة، بيتنفذ قبل ما Angular يدمر الـ Component أو الـ Directive. هنا بتعمل تنظيف (cleanup) لأي موارد أو اشتراكات (subscriptions) مستخدمة في الـ Component.

✨ باختصار، كل Lifecycle hook بيخليك تتحكم في سلوك الـ Component في مراحل معينة من حياته، زي لما يتغير، يتعرض، أو يتدمر.

</div>

<hr/>

## What is a data binding?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الData binding في Angular هو مفهوم أساسي بيسمح بتحديد طريقة التواصل بين الـ Component والـ DOM (واجهة المستخدم). الفكرة الرئيسية في الـ data binding هي إنك بتخلي التطبيق ديناميكي وتفاعلي من غير ما تقلق تسحب أو تدفع البيانات بشكل يدوي بين الـ Component والـ HTML.

#### فيه 4 أنواع للـ Data binding، وكل نوع بيسمح للبيانات تتحرك في اتجاه معين

##### من الـ Component للـ DOM (يعني من TS للview):

##### Interpolation

ده بيستخدم لما عايز تعرض قيمة متغير من الـ Component جوه الـ HTML. بتستخدم الأقواس المزدوجة {{ }} زي ما بنقول "خذ القيمة دي من الكود بتاعك وحطها هنا في للview".

<div dir="auto" align="left">

```HTML
<li>Name: {{ user.name }}</li>
<li>Address: {{ user.address }}</li>
```

</div>
هنا، user.name و user.address هما قيمتين موجودين في الـ Component، وبتظهر قيمهم للمستخدم جوا الـ HTML.

##### Property Binding

هنا، بتربط قيمة معينة من الـ Component بخاصية (property) من خصائص عنصر HTML. بتستخدم الأقواس المربعة [ ] حوالين الخاصية اللي عايز تتحكم فيها.

<div dir="auto" align="left">

```typescript
<input type="email" [value]="user.email">
```

</div>
في المثال ده، قيمة الinput value هتيجي من المتغير user.email اللي موجود في الـ Component.

##### من الـ DOM للـ Component (يعني من view للTS ):

##### Event Binding

ده لما عايز تربط حدث معين (زي click، أو keyup) بدالة أو وظيفة في الـ Component بتاعك. بتستخدم الأقواس العادية ( ) حوالين اسم الحدث.

<div dir="auto" align="left">

```HTML
<button (click)="logout()"></button>
```

</div>
هنا، لما المستخدم يضغط على الزرار ده، Angular هيستدعي دالة logout اللي موجودة في الـ Component.

##### (Two-way binding)

##### Two-way Data Binding

هنا بتربط البيانات بين الـ Component والـ DOM في الاتجاهين. يعني لو المستخدم غيّر حاجة في الواجهة، القيمة بتتحدث في الـ Component، ولو حصل العكس، القيمة اللي في الـ Component بتتغير في الواجهة. بتستخدم أقواس مربعة وعادية [( )] حوالين الـ ngModel.

<div dir="auto" align="left">

```HTML
<input type="email" [(ngModel)]="user.email">
```

</div>
هنا، ال input متصل بشكل مباشر مع المتغير user.email. يعني لو المستخدم كتب إيميل جديد في الinput قيمة user.email في الـ Component هتتحدث تلقائيًا. ولو حصل العكس، أي تغيير في user.email هيظهر مباشرة في الinput.

##### ✨ الخلاصة

-الInterpolation و Property Binding بيخلوا البيانات تمشي من الـ Component للـ DOM.
-الEvent Binding بيخلي البيانات تمشي من الـ DOM للـ Component.
-الTwo-way binding بيخلي البيانات تمشي في الاتجاهين، بين الـ Component والـ DOM في نفس الوقت.

</div>
<hr/>

## What is metadata?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Metadata في Angular هي بيانات إضافية بتتحط فوق  (classes) أو  (properties) أو  (methods) أو  (parameters) عشان تتحكم في سلوكهم. الـ Metadata بتتمثل في حاجة اسمها Decorators، وهي بتخلي Angular يفهم إزاي يتعامل مع الكود اللي انت كتبته. خلينا نبسط الموضوع مع الأنواع المختلفة من الـ Decorators:

### Class decorators

بتستخدم لتزيين الكلاس كله، زي لما بنستخدم Component@ أو NgModule@. دي بتحول الكلاس إلى Component أو Module.

<div dir="auto" align="left">

```typescript
import { NgModule, Component } from "@angular/core";

@Component({
  selector: "my-component",
  template: "<div>Class decorator</div>",
})
export class MyComponent {
  constructor() {
    console.log("Hey I am a component!");
  }
}

@NgModule({
  imports: [],
  declarations: [],
})
export class MyModule {
  constructor() {
    console.log("Hey I am a module!");
  }
}
```

</div>

##### Component@

هنا بيحول الكلاس MyComponent إلى Component بواجهة HTML مرتبطة بيه.

##### NgModule@

بيحول الكلاس MyModule إلى Module عشان يقدر يشتغل في التطبيق.

### Property decorators

بتستخدم لتزيين الخصائص جوا الكلاس. أشهر الأمثلة هي Input@ و Output@ اللي بيتحكموا في تبادل البيانات بين الـ Components.

<div dir="auto" align="left">

```typescript
import { Component, Input } from "@angular/core";

@Component({
  selector: "my-component",
  template: "<div>Property decorator</div>",
})
export class MyComponent {
  @Input()
  title: string;
}
```

</div>

### Method decorators

بتستخدم لتزيين (methods) جوا الكلاس، زي HostListener@ اللي بيتفاعل مع أحداث معينة زي الـ click أو hover.

<div dir="auto" align="left">

```typescript
import { Component, HostListener } from "@angular/core";

@Component({
  selector: "my-component",
  template: "<div>Method decorator</div>",
})
export class MyComponent {
  @HostListener("click", ["$event"])
  onHostClick(event: Event) {}
}
```

</div>

### Parameter decorators

بتستخدم لتزيين Parameters اللي جوا الـ Constructor. زي Inject@ و Optional@ اللي بيتحكموا في كيفية حقن القيم أو الخدمات جوا الكلاس.

<div dir="auto" align="left">

```typescript
import { Component, Inject } from "@angular/core";
import { MyService } from "./my-service";

@Component({
  selector: "my-component",
  template: "<div>Parameter decorator</div>",
})
export class MyComponent {
  constructor(@Inject(MyService) myService) {
    console.log(myService); // بيتم حقن MyService
  }
}
```

</div>
</div>
<hr/>

## What is Angular CLI?

[⬆️ Back to Top](#top)

### Angular CLI (Command Line Interface)

Angular CLI is a command line interface to scaffold and build Angular apps using nodejs style (commonJs) modules. You need to install using the npm command,

```bash
npm install @angular/cli@latest
```

i. Creating New Project:

```bash
ng new
```

ii. Generating Components, Directives & Services:

```bash
ng generate/g
```

The different types of commands would be:

- ng generate class my-new-class: add a class to your application
- ng generate component my-new-component: add a component to your application
- ng generate directive my-new-directive: add a directive to your application
- ng generate enum my-new-enum: add an enum to your application
- ng generate module my-new-module: add a module to your application
- ng generate pipe my-new-pipe: add a pipe to your application
- ng generate service my-new-service: add a service to your application

iii. Running the Project:

```bash
ng serve
```

<hr/>

## What is the difference between constructor and ngOnInit?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### الـ Constructor

الـ constructor هو زي "function" اللي بتشتغل أول ما تعمل نسخة جديدة من (class) في TypeScript. يعني مثلاً لما تيجي تعمل Component جديد، أول حاجة بتحصل هي إن الـ constructor بيشتغل.

وظيفته الأساسية إنه يجهز المتغيرات بتاعت الكلاس ويظبط حاجة اسمها Dependency Injection، ودي اللي بتخلي Angular يقدر يحط الـ services اللي محتاجها الكلاس بسهولة.

المهم إنك تستخدم الـ constructor عشان تجهز الحاجات الأساسية بتاعت الكلاس بس، يعني متعملش فيه أي "شغل" تقيل زي استدعاء دوال أو التعامل مع بيانات أو حاجات معقدة. الأفضل إنك تسيب الحاجات دي للـ ngOnInit لأن ده بيكون وقت مناسب أكتر عشان تبدأ الشغل الفعلي.

باختصار، خلي الـ constructor لتهيئة الحاجات الأساسية، من غير ما تعمل فيه حاجات كتير.

### الـ ngOnInit

هو واحد من الـ lifecycle hooks اللي Angular بتشغله بعد ما تكون خلصت إنشاء الـ Component وعرضته قدام المستخدم. يعني ببساطة، بيشتغل بعد الـ constructor.

عادة بنستخدم الـ ngOnInit لما نكون عايزين نجهز أو نعمل تهيئة لحاجات معينة زي البيانات أو لو عايزين نجيب بيانات من API، أو حتى لو في حاجات مربوطة (bindings) محتاجين نشتغل عليها.

الـ ngOnInit بيكون أنسب مكان تبتدي فيه الشغل التقيل، زي استدعاء بيانات أو التعامل مع الحاجات اللي جاية من بره الـ Component، لأن في الوقت ده بيكون Angular ظبط كل الـ bindings واتأكد إن البيانات اللي جايالك من بره (زي المتغيرات اللي بتجي من الـ parent component) جاهزة.

</div>
<hr/>

## What is a service?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الService في Angular هي ببساطة كود بتكتبه لما يكون عندك وظيفة معينة أو شغل عايز تعمله في أكتر من مكان في التطبيق. الفكرة من الـ Service هي إنها تخليك تفصل المهام المشتركة أو المنطق اللي بتحتاجه في كذا Component في مكان واحد، وتقدر تستخدمه بسهولة في أماكن كتير، وده بيساعد في تنظيم الكود وتجنب التكرار.

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import { Http } from "@angular/http";

@Injectable({
  providedIn: "root",
})
export class RepoService {
  constructor(private http: Http) {}

  fetchAll() {
    return this.http.get("https://api.github.com/repositories");
  }
}
```

</div>

### HTML

<div dir="auto" align="left">

```typescript
import { Component, OnInit } from "@angular/core";
import { RepoService } from "./repo.service";

@Component({
  selector: "app-repo-list",
  template: `
    <ul>
      <li *ngFor="let repo of repos">{{ repo.name }}</li>
    </ul>
  `,
})
export class RepoListComponent implements OnInit {
  repos: any[] = [];

  constructor(private repoService: RepoService) {}

  ngOnInit() {
    this.repoService.fetchAll().subscribe((data) => {
      this.repos = data;
    });
  }
}
```

</div>
</div>
 <hr/>

## What is dependency injection in Angular?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الDependency Injection (DI) في Angular هو ببساطة طريقة ذكية بتخلي الكلاس (class) يطلب الحاجات اللي محتاجها من بره بدل ما هو ينشئها بنفسه. يعني لو في service أو حاجة معينة الكلاس محتاجها عشان يشتغل، Angular بتساعده ويجيبله الحاجات دي جاهزة من بره.

#### الفكرة باختصار

بدل ما الكلاس يبقى مسؤول عن إنشاء كل حاجة بنفسه ، Angular بتشوف هو محتاج إيه، وتقوم تروح تجيبها وتحطها له جاهزة، عن طريق حاجة اسمها الـ Injector.

#### ليه نستخدم Dependency Injection؟

تنظيم الكود: بيساعد إن الكلاس مايبقاش مضطر ينشئ الحاجات اللي محتاجها بنفسه، وده بيفصل بين منطق الكود والحاجات اللي بيحتاجها.

إعادة الاستخدام: لو عندك service بتعمل حاجة معينة، تقدر تستخدمها في أكتر من Component بسهولة.

تسهيل الاختبارات: لما تيجي تختبر الكود، تقدر تستبدل الـ service الأصلية بحاجة وهمية بسهولة وتعمل اختباراتك من غير مشاكل.

</div>
<hr/>

## What is the purpose of async pipe?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Async Pipe في Angular بيساعدك في التعامل مع الـ Observable أو الـ Promise بشكل سهل وبدون ما تضطر تعمل subscribe بنفسك. يعني بدل ما تقعد تكتب كود عشان تراقب الـ Observable وتعمله unsubscribe لما الكومبوننت بتاعك يتدمر، الـ Async Pipe بيعمل كل ده لوحده.

تخيل إن عندك Observable بيرجع الوقت الحالي كل ثانيتين، وانت عايز تعرضه في الـ HTML بتاعك. باستخدام الـ Async Pipe، هتقدر تعمل ده من غير أي تعقيدات.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "async-observable-pipe",
  template: `<div>
    <code>observable|async</code>: Time: {{ time$ | async }}
  </div>`,
})
export class AsyncObservablePipeComponent {
  time$: Observable<string>;
  constructor() {
    this.time$ = new Observable((observer) => {
      setInterval(() => {
        observer.next(new Date().toString());
      }, 2000);
    });
  }
}
```

</div>
للي بيحصل هنا إنك عملت Observable اسمه time$ بيبعت القيمة الجديدة (الوقت الحالي) كل ثانيتين. بعد كده في التمبليت (template)، استخدمت الـ Async Pipe بالطريقة دي: {{ time$ | async }}.

الـ Async Pipe بيقوم بالاشتراك في الـ Observable أو الـ Promise وبيجيب أحدث قيمة منه ويعرضها. كل ما الـ Observable يبعث قيمة جديدة، الـ Pipe بيحدث القيمة في الـ View تلقائي.

</div>
<hr/>

## What is the purpose of \*ngFor directive?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ *ngFor directive في Angular هدفها الرئيسي هو إنها تساعدك تعرض مجموعة عناصر في الـ template بناءً على البيانات اللي عندك في الـ component. بمعنى إنك لو عندك array مثلاً من البيانات، زي users، ممكن بسهولة تكرر عرض كل عنصر من العناصر دي جوه الـ template بتاعك.
<div dir="auto" align="left">

```HTML
<li *ngFor="let user of users">
  {{ user }}
</li>
```

</div>
</div>
<hr/>

## What are pipes?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الpipes في Angular هي عبارة عن functions بسيطة بتشتغل عشان تاخد بيانات كمدخلات وتحوّلها لصيغة أو شكل معين يكون مفيد أكتر للمستخدم. وده بيتم عن طريق استخدام حاجة اسمها "template expressions"، اللي بتبقى موجودة جوا الHTML بتاع الcomponent.

خلينا نوضح بمثال عشان الصورة تكون أوضح. لو عندك component معمول في Angular وعايز تعرض تاريخ ميلاد معين (birthday) بس في شكل يكون سهل للفهم أو "human-friendly"، هنا ممكن تستخدم حاجة اسمها "date pipe". الـpipe دي هتخلي التاريخ يظهر بطريقة متنسيقة زي ما المستخدم ممكن يتوقع.

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-birthday",
  template: `<p>Birthday is {{ birthday | date }}</p>`,
})
export class BirthdayComponent {
  birthday = new Date(1987, 6, 18); // June 18, 1987
}
```

</div>
في الكود ده، انت عندك component اسمه BirthdayComponent وداخله birthday معمول على إنه object من نوع Date، بتحدده بتاريخ معين (18 يونيو 1987). بعد كده في الـHTML، استخدمت {{ birthday | date }} وده اللي بيسمى "pipe". الـ| هنا هي اللي بتحدد إنك بتستخدم pipe عشان تحول البيانات.

اللي بيحصل هو إن التاريخ اللي مخزن جوا الـbirthday هيظهر للمستخدم في شكل تاريخ مفهوم بسهولة، حسب الفورمات اللي Angular بيستخدمه افتراضيًا لعرض التواريخ.

<div dir="auto" align="left">

```HTML
Birthday is Jun 18, 1987
```

</div>
فالـpipes بتسهل عليك شغل كتير لو محتاج تعدل أو تنسق البيانات قبل عرضها للمستخدمين.
</div>
<hr/>

## Explain RxJS debounceTime operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ Parameterized Pipe في Angular ببساطة هو طريقة لتعديل الـ output بتاع الـ pipe باستخدام بارامترات إضافية. يعني تقدر تتحكم في النتيجة اللي هتطلع من الـ pipe عن طريق إضافة بارامترات بعد اسم الـ pipe باستخدام الـ colon " : ". لو الـ pipe بيقبل أكتر من باراميتر، بتفصل بينهم بـ colons تانية.

خلينا نوضح الموضوع بمثال بسيط زي اللي انت جبته عن عيد الميلاد. في الكود اللي انت كتبته، بنستخدم الـ date pipe عشان نعرض تاريخ معين لكن بالصيغة اللي احنا عايزنها (يوم/شهر/سنة).

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-birthday",
  template: `<p>Birthday is {{ birthday | date : "dd/MM/yyyy" }}</p>`, // 18/06/1987
})
export class BirthdayComponent {
  birthday = new Date(1987, 6, 18);
}
```

</div>
هنا، الـ date pipe بيقبل باراميتر وهو الصيغة اللي انت عايز تعرض بيها التاريخ، واللي هنا عبارة عن 'dd/MM/yyyy'. الـ pipe هيقوم بتحويل التاريخ اللي موجود في birthday (اللي هو 18 يونيو 1987) للصيغة اللي انت عايزها، وهيطلعلك 18/06/1987.

لو الـ pipe بيقبل أكتر من باراميتر، هتفصلهم بنفس الطريقة عن طريق colons.

</div>
<hr/>

## How do you chain pipes?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
انت بتستخدم أكثر من pipe وبتسميها chaining pipes. يعني بتربط أكثر من pipe مع بعض عشان تنفذ مجموعة عمليات على القيمة.

الفكرة ببساطة انك بتبدأ من القيمة الأولانية وبتعديها على أول pipe، وبعد ما الـ pipe الأول يخلص، النتيجة بتاعت الـ pipe الأول بتروح للـ pipe اللي بعده، وهكذا لغاية ما يخلصوا كل الـ pipes اللي انت حاططهم.

في المثال بتاعك، انت عندك خاصية birthday اللي هي تاريخ الميلاد:

<div dir="auto" align="left">

```typescript
birthday = new Date(1987, 6, 18);
```

</div>
ده معناه ان عندك التاريخ 18 يوليو 1987 (شهر 6 هو يوليو عشان الـ JavaScript بتمشي بالأصفار).

اللي بيحصل هنا:
الdate pipe: بيحول قيمة التاريخ ويعرضها بشكل معين. انت استخدمت الفورمات 'fullDate'، فالتاريخ هيظهر كامل زي "Thursday, June 18, 1987".

الuppercase pipe: بياخد النتيجة اللي طلعت من الـ date pipe وبيحولها لحروف كبيرة، فالناتج النهائي هيكون: "THURSDAY, JUNE 18, 1987".

### طريقة الكتابة

<div dir="auto" align="left">

```HTML
<p>Birthday is {{ birthday | date:'fullDate' | uppercase }} </p>
```

</div>

</div>
<hr/>

## What is a custom pipe?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ "custom pipe" ببساطة هو أن انت تكتب حاجة بنفسك في Angular عشان تحوّل البيانات بشكل معين، غير الـ "built-in pipes" اللي Angular بتوفّرها زي الـ date أو uppercase وكده.

أول حاجة لازم تعملها لما تيجي تكتب "custom pipe" هي إنك تستخدم الـ @Pipe ديكوريتور اللي بتجيبها من الـ core Angular.

<div dir="auto" align="left">

```typescript
@Pipe({name: 'myCustomPipe'})
```

</div>
بعد كده بتكتب class وبتخلّيه implement للـ PipeTransform interface اللي فيه الميثود الأساسية اللي هي transform. الميثود دي بتاخد الـ value اللي عاوز تحولها، وكمان ممكن تاخد شوية parameters إضافية. وتبقى النتيجة هي القيمة الجديدة اللي متحوّلة.

#### مثلا، لو هنعمل pipe بيحوّل أي input لقيمته مضروبة في رقم معيّن

<div dir="auto" align="left">

```typescript
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({ name: "multiply" })
export class MultiplyPipe implements PipeTransform {
  transform(value: number, multiplier: number): number {
    return value * multiplier;
  }
}
```

</div>
كده لو عندك template وعايز تستخدم الـ pipe ده، هتعمله زي ما بتعمل مع الـ built-in pipes:
<div dir="auto" align="left">

```HTML
{{ 5 | multiply: 2 }} // 10
```

</div>
النقطة اللي لازم تركز عليها إن اسم الـ pipe اللي بتكتبه في الـ @Pipe ديكوريتور هو اللي هتستخدمه في الـ template. والـ transform method دي هي اللي بتكتب فيها اللوجيك اللي عاوز تطبقه على البيانات.
</div>
<hr/>

## What is the difference between pure and impure pipe?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
طبعاً، الفرق بين الـ pure pipe والـ impure pipe في Angular بيكون في إزاي بيتعاملوا مع دورة التغيير (change detection)

### Pure Pipe

يتنفذ بس لما يكون في تغيير في القيمة أو في الـ parameters اللي اتبعتت للـ pipe.
يعني لو عندك قيمة primitive زي String أو Number أو Boolean، ولو اتغيرت القيمة دي، أو لو كان فيه تغيير في الـ object reference زي Date أو Array أو Function أو Object.
ده بيخلي الـ pure pipe أكتر كفاءة لأنها مش بتتنفذ كتير، وبتشتغل بس لما يكون في حاجة اتغيرت فعلاً.

### Impure Pipe

يتنفذ في كل دورة تغيير (change detection cycle) بغض النظر إذا كانت القيمة أو الـ parameters اتغيرت ولا لأ.
يعني ممكن الـ impure pipe يتنفذ كتير جداً، زي كل حركة مفتاح (keystroke) أو حركة ماوس (mouse-move).
ده ممكن يؤدي إلى أداء أبطأ لو استخدمته في أماكن كتير في التطبيق.

</div>
<hr/>

## What is HttpClient and its benefits?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الHttpClient هو واحد من الأدوات اللي بيوفرها Angular علشان تتعامل مع الـ backend services اللي بتشتغل بالـ HTTP. زمان كان الناس بتستخدم حاجات زي XMLHttpRequest أو fetch() API علشان يجيبوا البيانات من السيرفر، لكن دلوقتي Angular عامل لنا الموضوع أسهل شوية عن طريق الـ HttpClient اللي مبني أصلاً فوق الـ XMLHttpRequest. يعني، بيقدملك طريقة أبسط وأوضح علشان تشتغل مع الـ HTTP requests.

طيب، هو موجود فين؟ تقدر تضيفه في التطبيق بتاعك عن طريق تعمل import لل HttpClientModule من الباكدج اللي اسمها angular/common/http@ بالطريقة دي:

<div dir="auto" align="left">

```typescript
import { HttpClientModule } from "@angular/common/http";
```

</div>

### طيب إيه بقى فايدته؟

تقدر تختبر الكود بتاعك بسهولة لما تستخدمه في الـ HTTP requests.
تقدر تحدد أنواع البيانات اللي طالعين من وإلى الـ backend، وده بيخليك متأكد إنك شغال على البيانات الصح.
بيعمل intercept للrequest and response: يعني ممكن تتحكم في الطلبات اللي طالعة من التطبيق بتاعك أو الاستجابات اللي راجعة قبل ما توصل. ده بيساعد في حاجات زي إضافة headers أو التعامل مع الـ tokens.
بيدعم Observable APIs: لو متعود على الـ Observables في Angular، هتلاقي الـ HttpClient بيشتغل معاهم حلو جداً، وده بيخليك تستفيد من حاجات زي الـ RxJS.

</div>
<hr/>

## Explain RxJS debounceTime operator?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

</div>

 <!-- <hr/>
 ## Explain RxJS debounceTime operator?

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

</div> --> -->
