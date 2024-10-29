<!-- ## How to Use @ViewChild and @ViewChildren

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

ال@ViewChild بتستخدمها لو عايز تجيب عنصر معين من عناصر الـ DOM (زي زرار أو كومبوننت تاني) عشان تتعامل معاه من الكود، وبتديك أول عنصر يطابق الشرط اللي حطيته.

ال@ViewChildren بتديك كل العناصر اللي بتطابق الشرط اللي حطيته، وبتطلعهم في QueryList تقدر تلف عليها وتستخدم كل عنصر منها.

### إزاي تستخدم ViewChild@؟

<div dir="auto" align="left">

```typescript
@ViewChild(ChildComponent, { static: true }) child: ChildComponent;
```

</div>

### خليني أوضح أكتر النقطة دي:

```bash
@ViewChild(ChildComponent, { static: true })
```

هنا ChildComponent هو نوع أو كلاس العنصر اللي عايزين نجيبه (في الحالة دي، بنجيب عنصر معين اللي هو الكومبوننت ChildComponent).

🔴static: true و static: false
الخيار static بيحدد امتى Angular تجيب العنصر وتديك مرجع ليه. فيه حالتين هنا:

### static: true

لو حطينا static: true، ده معناه إن Angular هتجيب المرجع للعنصر قبل ما تعمل أول تغيير (Change Detection). بمعنى تاني، Angular هتجيب العنصر من الـ DOM في بداية تحميل الصفحة أو الكومبوننت، وده مفيد لو العنصر دايمًا بيبقى موجود في التيمبلت بتاعنا.

### static: false

لو حطينا static: false، ده معناه إن Angular هتستنى لحد ما تكمل أول Change Detection وتحدد العناصر اللي هتظهر حسب شروط معينة زي *ngIf أو *ngSwitch.

يعني لو العنصر بيظهر بناءً على شرط معين أو بيتم تحميله ديناميكيًا، لازم تستخدم static: false، عشان Angular تستنى لحد ما الشرط يتحقق أو العنصر يظهر في التيمبلت.

### مثال للتوضيح

لو عندنا عنصر بيتحكم في ظهوره شرط معين، زي \*ngIf، لازم نستخدم static: false عشان نضمن إن Angular هتنتظر لحد ما يتحقق الشرط ده ويظهر العنصر في التيمبلت.

<div dir="auto" align="left">

```HTML
<div *ngIf="showChildComponent">
  <child-component></child-component>
</div>
```

</div>

<div dir="auto" align="left">

```typescript
@ViewChild(ChildComponent, { static: false }) child: ChildComponent;
```

</div>
هنا، Angular هتستنى لحد ما يحصل تغيير (Change Detection) ويتحقق شرط *ngIf، وبعد كده هتجيب ChildComponent لما يكون موجود في التيمبلت.

### مثال بسيط

عندنا كومبوننت صغير اسمه ChildComponent فيه عداد، وفيه زراير لزيادته أو نقصانه:

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "child-component",
  template: `<h2>Child Component</h2>
    <p>Current count: {{ count }}</p>`,
})
export class ChildComponent {
  count = 0;

  increment() {
    this.count++;
  }
  decrement() {
    this.count--;
  }
}
```

</div>
في الكومبوننت الأب (Parent Component)، عايزين نجيب الـ ChildComponent ونتحكم في العداد بتاعه. نستخدم ViewChild@ كالتالي:

<div dir="auto" align="left">

```typescript
import { Component, ViewChild } from "@angular/core";
import { ChildComponent } from "./child.component";

@Component({
  selector: "app-root",
  template: `
    <h1>Parent Component</h1>
    <button (click)="increment()">Increment</button>
    <button (click)="decrement()">Decrement</button>
    <child-component></child-component>
  `,
})
export class AppComponent {
  @ViewChild(ChildComponent, { static: true }) child: ChildComponent;

  increment() {
    this.child.increment();
  }

  decrement() {
    this.child.decrement();
  }
}
```

</div>
استخدام Template Reference Variable مع ViewChild@
بدل ما نحدد النوع بتاع الكومبوننت، ممكن نستخدم Template Reference Variable.
يعني ندي اسم للعنصر في التيمبلت زي كده:

<div dir="auto" align="left">

```HTML
<child-component #childRef></child-component>
```

</div>
وبعدين نجيبه في الكود:
<div dir="auto" align="left">

```typescript
@ViewChild('childRef', { static: true }) child: ChildComponent;
```

</div>

### التعامل مع عناصر الـ HTML باستخدام ElementRef

لو عايز تجيب عنصر HTML زي p أو div، ممكن تستخدم ViewChild@ مع ElementRef.

### مثال:

<div dir="auto" align="left">

```HTML
<p #para>Some text</p>
```

</div>

<div dir="auto" align="left">

```typescript
import { Component, ElementRef, ViewChild, AfterViewInit } from "@angular/core";

@Component({
  selector: "htmlelement",
  template: `<p #para>Some text</p>`,
})
export class HTMLElementComponent implements AfterViewInit {
  @ViewChild("para", { static: false }) para: ElementRef;

  ngAfterViewInit() {
    console.log(this.para.nativeElement.innerHTML);
    this.para.nativeElement.innerHTML = "new text";
  }
}
```

</div>

### 🔴 لو عندك أكتر من عنصر بنفس النوع؟

لو عندك أكتر من عنصر زي ChildComponent في نفس التيمبلت، ViewChild@ هترجعلك أول واحد بس. لكن لو عايز كل العناصر، استخدم ViewChildren@

### مثال مع ViewChildren@

في المثال ده، عندنا أكتر من input:

<div dir="auto" align="left">

```HTML
<input name="firstName" [(ngModel)]="firstName">
<input name="middleName" [(ngModel)]="middleName">
<input name="lastName" [(ngModel)]="lastName">
```

</div>
نجيبهم باستخدام ViewChildren@ كالتالي:
<div dir="auto" align="left">

```typescript
import { Component, ViewChildren, QueryList, NgModel } from "@angular/core";

@Component({
  selector: "app-viewchildren-example",
  template: `
    <input name="firstName" [(ngModel)]="firstName" />
    <input name="middleName" [(ngModel)]="middleName" />
    <input name="lastName" [(ngModel)]="lastName" />
    <button (click)="show()">Show</button>
  `,
})
export class ViewChildrenExampleComponent {
  @ViewChildren(NgModel) modelRefList: QueryList<NgModel>;

  show() {
    this.modelRefList.forEach((element) => {
      console.log(element);
    });
  }
}
```

</div>
هنا ViewChildren@ بترجع كل input، وتقدر تلف عليهم باستخدام ()forEach

### 🔴 ملحوظلة

لما نستخدم ViewChild@ او ViewChildren@ في Angular، بنحتاج نستنى لحد ما العناصر في الـ DOM تكون اتعملها تحميل بالكامل قبل ما نقدر نستخدمها في الكود.

عشان كده، الـlifecycle hook المناسبة للتعامل مع ViewChild@ هي ngAfterViewInit مش ngOnInit.

</div>

## ContentChild and ContentChildren in Angular

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### إيه هما ContentChild و ContentChildren؟

الContentChild@ و `ContentChildren@` هما (Decorators) في Angular بنستخدمهم عشان نوصل لحاجة اسمها "Projected Content"، اللي هو المحتوى اللي بيجي للكومبوننت من كومبوننت الأب (Parent Component).

الProjected Content يعني محتوى جاي من الكومبوننت الأب عشان يتعرض في الكومبوننت الابن، وبنحدده عادةً باستخدام عنصر `ng-content` اللي بنضيفه في الكومبوننت الابن عشان يحجز مكان لعرض المحتوى اللي جاي من بره.

### الفرق بين `ViewChild@` و `ContentChild@`

🔴 الViewChild@ و ViewChildren@ بيقدروا يجيبوا أي عنصر موجود جوه الكومبوننت نفسه، سواء كان عنصر HTML، أو كومبوننت تاني، أو ديركتيف.

🔴 الContentChild@ و ContentChildren@ بقى بيستخدموا للوصول للمحتوى اللي جاي من الكومبوننت الأب عبر `ng-content`، يعني بيقدروا يجيبوا أي حاجة جاية من بره مش موجودة بشكل مباشر جوه الكومبوننت.

### إزاي بنستخدم ContentChild و ContentChildren؟

1. مثال بسيط على ContentChild
خلينا نقول عندنا كومبوننت (CardComponent) بيستخدم <ng-content> عشان ياخد محتوى من بره ويعرضه جواه.
مثلا الكارت فيه 3 أماكن: `header`, `content`, `وfooter`
<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "card",
  template: `
    <div class="card">
      <ng-content select="header"></ng-content>
      <ng-content select="content"></ng-content>
      <ng-content select="footer"></ng-content>
    </div>
  `,
  styles: [
    `
      .card {
        min-width: 280px;
        margin: 5px;
        float: left;
      }
    `,
  ],
})
export class CardComponent {}
```

</div>

الكود ده هيحجز 3 أماكن في الكارت: واحد لـ header، والتاني لـ content، والتالت لـ footer

2. استخدام ContentChild للوصول للعنصر المرسل من الكومبوننت الأب
   دلوقتي لو عندنا في الكومبوننت الأب كذا كارت وعايزين نضيف لكل كارت محتوى مختلف، نكتب الكود بالشكل ده:

<div dir="auto" align="left">

```HTML
<card>
  <header><h1 #header>Angular</h1></header>
  <content>One framework. Mobile & desktop.</content>
  <footer><b>Super-powered by Google</b></footer>
</card>
```

</div>

في المثال ده، إحنا ضفنا header, content, وfooter لكارت واحد، وحددنا `<h1 #header>` اللي موجود في header.

دلوقتي عايزين نوصل للـ h1 اللي في header جوه CardComponent باستخدام ContentChild@

<div dir="auto" align="left">

```typescript
import {
  Component,
  ContentChild,
  ElementRef,
  AfterContentInit,
  Renderer2,
} from "@angular/core";

@Component({
  selector: "card",
  template: `
    <div class="card">
      <ng-content select="header"></ng-content>
      <ng-content select="content"></ng-content>
      <ng-content select="footer"></ng-content>
    </div>
  `,
})
export class CardComponent implements AfterContentInit {
  @ContentChild("header") cardContentHeader: ElementRef;

  constructor(private renderer: Renderer2) {}

  ngAfterContentInit() {
    this.renderer.setStyle(
      this.cardContentHeader.nativeElement,
      "font-size",
      "20px"
    );
  }
}
```

</div>

### 🔴 النقطة المهمة هنا

ال`ContentChild('header')@` بيجيب أول عنصر اسمه header موجود في الـ Projected Content.

الngAfterContentInit هو الـ lifecycle hook المناسب عشان نضمن إن Angular حملت المحتوى الخارجي.

### ContentChildren@ عشان تجيب أكتر من عنصر

لو عندنا كذا عنصر بنفس الاسم (مثلا كذا عنصر header)، ممكن نستخدم ContentChildren@ عشان نجيبهم كلهم في شكل قائمة (QueryList) ونقدر نلف عليهم ونتعامل مع كل عنصر فيهم.

<div dir="auto" align="left">

```typescript
@ContentChildren('header') headers: QueryList<ElementRef>;
```

</div>

### الفرق بين ContentChild و ContentChildren

ال@ContentChild بيجيب أول عنصر بس يطابق الاسم.

ال@ContentChildren بيجيب كل العناصر اللي ليها نفس الاسم في شكل قائمة (QueryList)، وتقدر تستخدم forEach عشان تتعامل مع كل عنصر لوحده.

### ✅ الفرق بين ViewChild@ و ContentChild@

| #             | ViewChild و ViewChildren              | ContentChild و ContentChildren                      |
| ------------- | ------------------------------------- | --------------------------------------------------- |
| **الاستخدام** | بيدور على العناصر جوه الكومبوننت نفسه | بيدور على المحتوى اللي جاي من بره                   |
| **التوقيت**   | بيشتغل بعد تحميل التيمبلت             | بيشتغل بعد تحميل المحتوى الخارجي (AfterContentInit) |

</div>

## What are decorators in angular ?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

الـ Decorators في Angular هي عبارة عن وظيفة أو دالة بتدي معلومات إضافية عن الكلاس (class) أو (method) أو (property) أو (parameter).

بتدي معلومات لـ Angular عشان تفهم الكود وتعرف إزاي تتعامل معاه. يعني، الديكوريتور بيزود الكلاس بمعلومات تخليه (Component)، أو (Directive)، أو (Service)... وهكذا.

### طيب بنستخدم الـ Decorators ليه في Angular؟

الAngular بتستخدم الـ Decorators عشان تضيف Metadata (معلومات إضافية) للكود اللي بنكتبه.

المعلومات دي بتساعد Angular تفهم إزاي تتعامل مع الكلاس أو الميثودات اللي جواه.

مثلا، لو عندك كلاس وعايز تخليه Component، بنستخدم ديكوريتور اسمه Component@، ولو عايز تعمل Service بنستخدم Injectable@ وهكذا.

### أنواع الديكوريتورز في Angular

الAngular عندها كذا نوع من الـ Decorators، وهنقسمهم لأربع أنواع رئيسية:

#### Class Decorators: بتستخدم على الكلاسات (classes).

#### Property Decorators: بتستخدم على (properties).

#### Method Decorators: بتستخدم على (methods).

#### Parameter Decorators: بتستخدم على الباراميترز (parameters) بتاعة الـ Constructor.

### Class Decorators

#### 1- NgModule@

#### 2 -Component@

#### 3- Injectable@

#### 4- Directive@

#### 5- Pipe@

ديكوريتورز بتشتغل على الكلاسات، زي Component@ وDirective@ وInjectable@، ودي بتخلي Angular تتعامل مع الكلاس ده بطريقة معينة.

##### Component@

بنستخدمه عشان نقول لـ Angular إن الكلاس ده عبارة عن Component، وده بيخلي Angular تتعامل مع الكلاس ده ك component ممكن يتعرض في التيمبلت.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
})
export class AppComponent {}
```

</div>

##### Injectable@

ديكوريتور بيستخدم عشان نقول لـ Angular إن الكلاس ده محتاج يتعامل كـ Service. ده بيخلي Angular تعرف توفر الكلاس ده لما نحتاجه في component تاني عن طريق الـ Dependency Injection.

<div dir="auto" align="left">

```typescript
@Injectable({
  providedIn: "root",
})
export class MyService {}
```

</div>

### Property decorators

#### 1- Input@

#### 2- Output@

#### 3- HostBinding@

#### 4- ContentChild@

#### 5- ContentChildren@

#### 6- ViewChild@

#### 7- ViewChildren@

<div dir="auto" align="left">

```typescript
export class ChildComponent {
  @Input() childProperty: string;
}
```

</div>

### Method decorators

#### 1- HostListener@

<div dir="auto" align="left">

```typescript
@HostListener('click') onClick() {
  console.log(' cliked');
}
```

</div>

### Parameter decorators

#### 1- Inject@

#### 2- Self@

#### 3- SkipSelf@

#### 4- Optional@

#### 5- Host@

<div dir="auto" align="left">

```typescript
constructor(@Inject(SomeToken) private myValue) {

}
```

</div>
</div>

## AfterViewInit, AfterViewChecked, AfterContentInit and AfterContentChecked in Angular

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### إيه الفرق بين Content و View في Angular؟

قبل ما نشرح الـ Hooks اللي بنستخدمهم، محتاجين نفهم حاجة مهمة، وهي الفرق بين Content و View:

Content: ده المحتوى اللي بيوصل للكومبوننت كـ Projected Content، يعني محتوى بيجيله من الكومبوننت الأب عن طريق `<ng-content>`.

View: دي التيمبلت (Template) أو UI بتاع الكومبوننت نفسه، اللي بنكتبه جواه.

### الAngular بيستخدم 4 Lifecycle Hooks للتعامل مع الـ Content والـ View:

فيه أربع Hooks مهمين في Angular بيساعدونا نتحكم في التوقيت اللي بنشتغل فيه مع المحتوى اللي جاي من بره (اللي هو الـ Content) والعرض بتاع الكومبوننت (اللي هو الـ View).

#### 1. AfterContentInit

ده Hook بيشتغل أول ما يتعمل تحميل كامل للمحتوى (Content) اللي جاي من الأب.

الAngular كمان بيحدّث الخصائص اللي بنزودها بديكوريتور ContentChild@ أو ContentChildren@ قبل ما تنادي Hook دي.

بتشتغل مرة واحدة بس.

#### 2. AfterContentChecked

ده Hook بيشتغل كل مرة يحصل Change Detection في التطبيق.

يعني إيه؟ يعني كل مرة Angular بتفحص إذا فيه تغيير حصل، بتشغل الـ Hook ده وتتأكد من أي تغييرات حصلت في المحتوى.

بـالمختصر، ده بيشوف إذا حصل أي تعديل على المحتوى وبيشتغل كل مرة Angular تعمل عملية فحص للتغييرات (حتى لو بسيط زي الضغط على زرار).

#### 3. AfterViewInit

ده Hook بيشتغل بعد ما ينتهي تحميل الـ View الخاص بالكومبوننت وأي Child Components جواه.

الAngular بيحدّث الخصائص اللي بنزودها بديكوريتور ViewChild@ أو ViewChildren@ قبل ما تنادي Hook دي.

بتشتغل مرة واحدة بس.

#### 4. AfterViewChecked

ده Hook بيشتغل كل مرة يحصل Change Detection ويتأكد من أي تغييرات في (View).

يعني بعد ما Angular تخلص فحص التغييرات، هتشغل الـ Hook ده عشان تشوف إذا اتعدل ولا لأ.

بـالمختصر، ده زيه زي AfterContentChecked لكن بيركز على العرض بدل المحتوى، وبيشتغل في كل عملية فحص تغييرات.

#### ❌ ليه ماينفعش نعدل Bindings في الـ Checked Hooks زي ngAfterViewChecked؟

في Angular، الـ Checked Hooks زي ngAfterViewChecked بتشتغل بعد كل دورة فحص تغييرات (Change Detection Cycle). يعني، كل مرة Angular تشوف إذا فيه حاجة اتغيرت في الكومبوننت أو في الـ View، بيتم استدعاء الـ Hook دي.

المشكلة في تعديل الـ Bindings في الـ Checked Hooks
لما تعمل تعديل على Binding (زي تعديل قيمة متغيرة بتظهر في التيمبلت) في ngAfterViewChecked، ده بيعمل مشكلة لإن Angular هتضطر تدخل في دورة فحص جديدة عشان تتأكد من التغييرات، وهكذا تفضل في حلقة مفرغة (Infinite Loop) من دورات الفحص.

###### 🔴 المشكلة الكبيرة هنا إنك ممكن تواجه خطأ اسمه: ExpressionChangedAfterItHasBeenCheckedError

الخطأ ده معناه إن فيه قيمة اتغيرت بعد ما Angular انتهت من الفحص، وده بيعمل تعارض في الـ Change Detection.

### ✅ الحل

لو عايز تقرأ قيمة viewChild.message وتعرضها في التيمبلت من غير مشاكل، اعمل التعديل في Hook زي ngAfterViewInit أو في أماكن تانية مش بتتكرر زي ngOnInit.

### Init Vs Checked Hooks

الInit Hooks (AfterContentInit وAfterViewInit): بتشتغل مرة واحدة بس بعد ما ينتهي تحميل المحتوى أو العرض لأول مرة.

الChecked Hooks (AfterContentChecked وAfterViewChecked): بتشتغل في كل دورة Change Detection.

#### 🔴 لما بقول إن الـ Hook "بتشتغل مرة واحدة بس"، أقصد إن الـ Hook دي بتشتغل أول ما يحصل تحميل للكومبوننت بس ومش بتكرر تاني.

### ليه بتشتغل مرة واحدة بس؟

الفكرة إن الـ Hooks دي متخصصة إنك تستخدمها لإعدادات مبدئية. مثلا لو عايز تعمل حاجة في الكومبوننت بعد ما يخلص تحميله مباشرةً، بس مش محتاج تعملها كل مرة يحصل فيها تغيير في التطبيق. عشان كده Angular بتشغل الـ Hooks دي مرة واحدة بس بعد أول تحميل للكومبوننت أو المحتوى.

### طيب إيه اللي بيشتغل أكتر من مرة؟

في المقابل، فيه Hooks زي AfterContentChecked و AfterViewChecked. دول بيشتغلوا كل مرة يحصل فيها Change Detection في التطبيق.

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
