<!-- ## What is ng-content?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ ng-content في Angular بنستخدمه عشان نعمل حاجة اسمها content projection، وهي إننا نقدر نمرر HTML من الـ Parent Component للـ Child Component بحيث الـ Child Component يعرض المحتوى ده في مكان معين جوة UI بتاعته.

🔴 لو فكرت فيها، الـ Input@ بيسمح للـ Parent إنه يمرر بيانات للـ Child Component، بس لو حبينا نمرر حاجة زي HTML elements أو محتوى فيه CSS معين، الـ Input@ مش حينفع. وده هنا بييجي دور ng-content.

### مثال توضيحي بسيط

لو عندك Button Component بسيط، هيعرض زراير، وعايز مثلاً تخلي النص اللي جواه "Click Me"، تقدر تعمل كده بإنك تضيف <button>Click Me</button> جوة الكومبوننت.

لكن لو عايز تخلي الـ Parent هو اللي يقرر يكتب إيه جوة الزرار أو يضيف HTML مختلف، بنستخدم ng-content.

### إزاي نعمل ده؟

في المثال ده، بدل ما تحط "Click Me" جوة <button>Click Me</button>، هنحط <ng-content></ng-content> مكانه. وده معناه إن المحتوى اللي بين <app-fancybtn></app-fancybtn> في الـ Parent Component حيتعرض جوة الزرار.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "app-fancybtn",
  template: `<button><ng-content></ng-content></button>`,
})
export class FancyBtnComponent {}
```

</div>
وفي الـ Parent Component هنكتب مثلاً:
<div dir="auto" align="left">

```HTML
<app-fancybtn>Click Me</app-fancybtn>
<app-fancybtn><b>Submit</b></app-fancybtn>

```

</div>
كده النص اللي بين app-fancybtn  هيظهر جوة الزرار في المكان اللي محطوط فيه ng-content. الجميل هنا إنك ممكن تمرر أي محتوى HTML وحيظهر.

### الـ Multiple Projections والـ select attribute

لو عندك كومبوننت زي Card Component وفيه أجزاء زي header وcontent وfooter، تقدر تدي لكل جزء ng-content خاص بيه باستخدام select attribute. بالشكل ده تقدر تمرر محتويات مختلفة للـ Parent والـ Child هيعرضهم في الأماكن الصح.

<div dir="auto" align="left">

```typescript
@Component({
  selector: "app-card",
  template: `
    <div class="card">
      <div class="header"><ng-content select="header"></ng-content></div>
      <div class="content"><ng-content select="content"></ng-content></div>
      <div class="footer"><ng-content select="footer"></ng-content></div>
    </div>
  `,
})
export class CardComponent {}
```

</div>
وفي الـ Parent

<div dir="auto" align="left">

```HTML
<app-card>
  <header><h1>Angular</h1></header>
  <content>One framework. Mobile & desktop.</content>
  <footer><b>Super-powered by Google</b></footer>
</app-card>
```

</div>

### ✨ ng-content without selector catches all

</div>
<hr/>


## what is Angular input and output and EventEmitter?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
أول حاجة، خلينا نبدأ بـ Input@
لو عندك Input@ في الـ child component، ده معناه إنك ممكن تستقبل بيانات من الـ parent component. يعني مثلا لو عندك component اسمه CustomerDetailComponent وعاوز تستقبل بيانات عميل معين من الـ parent component، هتعمل حاجة زي كده:


<div dir="auto" align="left">

```typescript
export class CustomerDetailComponent implements OnInit {
  @Input() customer: Customer;
}
```

</div>
هنا احنا عاملين Input@ فوق الخاصية customer. ده معناه إن الـ parent component هيقدر يبعت قيمة للخاصية دي، زي كده مثلا:

<div dir="auto" align="left">

```HTML
<app-customer-detail [customer]="selectedCustomer"></app-customer-detail>
```

</div>

### ثاني حاجة، الـ Output@ و EventEmitter
لما تيجي تتعامل مع Output@، ده معناه إنك بتبعت أحداث للـ parent component. يعني مثلا لو الـ child component عايز يقول للـ parent component إن العميل اتعدل، هنعمل كالتالي:

<div dir="auto" align="left">

```typescript
@Output() customerChange: EventEmitter<Customer> = new EventEmitter<Customer>();

update() {
  this.customerChange.emit(this.customer);
}
```

</div>
هنا إحنا بنستخدم Output@ فوق الخاصية customerChange اللي من نوع EventEmitter<Customer>. لما نعمل emit للحدث ده عن طريق update function، الـ parent component هيقدر يلتقط الحدث ده ويشوف القيمة اللي بعتها customer.

🔴 في الـ parent component، نقدر نسمع الحدث ده باستخدام كود زي ده

<div dir="auto" align="left">

```HTML
<app-customer-detail [customer]="selectedCustomer" (customerChange)="update($event)"></app-customer-detail>
```

</div>
هنا في <app-customer-detail> إحنا بنحط customerChange بين أقواس دائرية عشان نقدر نمسك الحدث، وده هيشغل الـ update function اللي في الـ parent component لما يتغير الـ customer.

### ملاحظات إضافية على Input@ و Output@ في Angular

#### 1. إمكانية تمرير اسم اختياري مع Input@
Input@ بتسمح لك بإنك تحدد اسم اختياري، وده بيبقى مفيد لما تحب تسمي الخاصية حاجة في الكود واسم تاني للـ binding في الـ HTML.
<div dir="auto" align="left">

```typescript
@Input('customerData') customer: Customer;
```

</div>
✨ هنا بنستخدم customerData كاسم خاص بالـ binding في الـ Parent، لكن في الكود بنستخدم customer.

#### 2. التعامل مع تغييرات باستخدام Setter
تقدر تعمل setter للخاصية اللي عليها Input@ عشان تضيف أي منطق إضافي أو تتحكم في التغيير قبل ما يتم تعيين القيمة.


<div dir="auto" align="left">

```typescript
private _customerData: Customer;

@Input()
set customer(customer: Customer) {
  this._customerData = customer;
  console.log("Updated customer data:", this._customerData);
}

get customer(): Customer {
  return this._customerData;
}

```

</div>
هنا، كل مرة يتغير فيها customer، هنقدر نشغل كود معين أو نضيف منطق إضافي قبل ما نعطي القيمة للخاصية.

#### 3. الاشتراك في تغييرات Input@ باستخدام ngOnChanges

الAngular بيوفر ngOnChanges كـ lifecycle hook، وده بيسمح لنا نراقب أي تغيير في الخصائص اللي عليها Input@ في أي وقت.


<div dir="auto" align="left">

```typescript
import { OnChanges, SimpleChanges } from '@angular/core';

export class CustomerDetailComponent implements OnChanges {
  @Input() customer: Customer;

  ngOnChanges(changes: SimpleChanges) {
    if (changes['customer']) {
      console.log("Customer changed:", changes['customer'].currentValue);
    }
  }
}
```

</div>
هنا ngOnChanges هيتم تنفيذه كل مرة يحصل فيها تغيير في الخاصية customer.

#### 4. الEventEmitters تعتبر Observable

الEventEmitters في Angular هي Observable زي RxJS Subjects، وده بيسمح باستخدام مشغلين RxJS عشان تتلاعب بالأحداث، مثلا تقدر تعمل debounceTime، filter، وغيره على الأحداث اللي بتنبعث.

#### 5. تمرير البيانات حسب المرجع (Pass by Reference)
لبيانات من نوع Object وArray بتنتقل حسب Reference يعني أي تغيير فيها بيعدل النسخة الأصلية. عشان كده لما تبعت بيانات من الـ Parent للـ Child، لو عدلتها في الـ Child، هتتغير تلقائيًا في الـ Parent.
البيانات من نوع Primitive زي number و string بتتنقل حسب القيمة، فالتغيير على القيمة مش بيأثر على النسخة الأصلية في الـ Parent.
</div>
<hr/>

## Template Reference Variable in Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
الTemplate Reference Variable هي متغيرات بننشئها في  (Template) عشان نقدر نوصل لأي عنصر HTML، أو  (Component)، أو  (Directive) في الTemplate

#### كيفية تعريف Template Reference Variable
نقدر نعرّفها باستخدام علامة # متبوعة باسم المتغير.

#### أمثلة

عنصر HTML

<div dir="auto" align="left">

```HTML
<input type="text" #firstName>
```

</div>
component or directive
<div dir="auto" align="left">

```HTML
<app-customer #customerList="customer"></app-customer>
```

</div>

#### إظهار القيم باستخدام Template Reference Variables

في المثال ده، بنعرف متغيرات firstName# و#lastName

<div dir="auto" align="left">

```HTML
<h1>Welcome</h1>

<input type="text" #firstName placeholder="First Name" (keyup)="0">
<input type="text" #lastName placeholder="Last Name" (keyup)="0">

<b>Welcome {{ firstName.value }} {{ lastName.value }}</b>
```

</div>
1- عند الكتابة داخل   (input)، بيتم تفعيل الحدث keyup.
بسبب "0"=(keyup), الAngular بيقوم بتشغيل الChange Detection لتحديث القيم اللي في الTemplate.

2- Change Detection بيحدث  (view) مباشرة ويعرض القيمة الجديدة اللي كتبتها في الinput

#### لماذا نحتاج "0"=(keyup)"؟
لو شيلنا (keyup) من الكود، ممكن ما يتم تحديث جملة الترحيب بالسرعة اللي بنتوقعها لأن Angular يعتمد على الكشف عن التغييرات فقط عند وقوع حدث غير متزامن أو عند أي حدث متعلق بالكشف عن التغييرات.
</div>
<hr/>

 ## What is ng-container in Angular?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ ng-container ده عبارة عن طريقة بنستخدمها في أنجولر عشان نعمل تقسيم أو جزء معين في  (template) من غير ما نضيف عنصر HTML فعلي في الصفحة. يعني الـ ng-container نفسه مش بيظهر في الكود النهائي للـ HTML، لكن المحتوى اللي جواه بيظهر.

### ليه بنستخدم ng-container؟
الميزة الرئيسية للـ ng-container إنه بيخلينا نضيف حاجات معينة زي شروط أو تكرارات (زي *ngIf أو *ngFor) من غير ما نضطر نضيف عنصر إضافي في DOM، واللي ممكن يكون ليه تأثير سلبي على الأداء، أو حتى يكون مزعج لو بتعدل في الـ CSS.

#### مثال بسيط

<div dir="auto" align="left">

```HTML
<h1> ng-Container</h1>
<p>Hello  world!</p>
<ng-container>
  المحتوى بتاع الكونتينر.
</ng-container>
```

</div>
الكود ده لما بيتحول لـ HTML النهائي هيكون كالتالي:
<div dir="auto" align="left">

```HTML
<h1> ng-Container</h1>
<p>Hello  world!</p>
المحتوى بتاع الكونتينر.
```

</div>
✨ زي ما انت شايف، الـ ng-container نفسه اختفى، لكن المحتوى اللي جواه ظهر في الصفحة.

### استخدامات ng-container
#### مثال مع ngFor و ngIf
تخيل إن عندك قائمة فيها مجموعة من العناصر وعايز تعرض بس العناصر النشطة (اللي Active)، فهتستخدم *ngFor عشان تعمل لوب على العناصر، و*ngIf عشان تتحقق إذا كان العنصر نشط ولا لأ.

لو استخدمت عنصر زي span مثلا عشان تحط الـ *ngFor هتلاقي إنه بيضيف عنصر span جديد في DOM لكل عنصر، وده ممكن يخلي الكود أطول وممكن يأثر على الـ CSS.
لكن لو استخدمت ng-container، هتتجنب الحكاية دي

بدون ng-container
<div dir="auto" align="left">

```HTML
<ul>
  <span *ngFor="let item of items;">
    <li *ngIf="item.active">
      {{item.name}}
    </li>
  </span>
</ul>

```

</div>
باستخدام ng-container
<div dir="auto" align="left">

```HTML
<ul>
  <ng-container *ngFor="let item of items;">
    <li *ngIf="item.active">
      {{item.name}}
    </li>
  </ng-container>
</ul>
```

</div>
مثال تاني مع ngIf
لو عندك شرط *ngIf عشان تتحقق من وجود عنصر معين، مفيش داعي تستخدم div أو أي عنصر عشان تحط فيه الشرط ده؛ ممكن تستبدله بـ ng-container

بدون ng-container

<div dir="auto" align="left">

```HTML
<div *ngIf="items1">
  <div *ngFor="let item of items1;">
    {{item.name}}
  </div>
</div>
```

</div>
باستخدام ng-container

<div dir="auto" align="left">

```HTML
<ng-container *ngIf="items1">
  <div *ngFor="let item of items1;">
    {{item.name}}
  </div>
</ng-container>
```

</div>
</div>
<hr/>


 ## How to use ng-template and TemplateRef in Angular


 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
الـ ng-template ده عنصر في Angular بيستخدم عشان تحط فيه template معين، لكن من غير ما يتعرض في الصفحة (الـ DOM) بشكل مباشر. يعني هو كأنك بتجهز حاجة وتخليها جاهزة عالرف، ومش بتظهر غير لما تقوله يظهر.

### مثال بسيط

<div dir="auto" align="left">

```HTML

<h2>Defining a Template using ng-Template</h2>

<ng-template>
  <p> Say Hello</p>
</ng-template>
```

</div>
مش هتلاقي "Say Hello" ظهرت في الصفحة. السبب إن الـ ng-template لوحده مش هيعرض أي حاجة، هو بس بيحطها على جنب لحد ما تيجي أنت تقوله يعرضها فين وإمتى.

### إزاي نعرض الـ template؟
#### فيه كذا طريقة علشان تعرض اللي جوه ng-template

ال ngTemplateOutlet: دي Directive بتخليك تعرض الـ template في مكان معين.

#### مثال باستخدام ngTemplateOutlet
الأول بنعمل الـ template ونحط عليه اسم علشان نقدر نرجعله:

<div dir="auto" align="left">

```HTML
<ng-template #sayHelloTemplate>
  <p>Say Hello/p>
</ng-template>
```

</div>
وبعدين في أي مكان عاوزين نعرض فيه الـ template ده، بنستخدم ng-container بالطريقة دي
<div dir="auto" align="left">

```HTML
<ng-container *ngTemplateOutlet="sayHelloTemplate">
This text is not displayed
</ng-container>
```

</div>
فالنتيجة اللي هتطلع هي
<div dir="auto" align="left">

```HTML
Say Hello
```

</div>
✨ يعني Angular بياخد اللي جوه sayHelloTemplate ويعرضه مكان الـ ng-container

### طب لو عاوز أتحكم فيه أكتر من TS؟
لو محتاج تتحكم في عرض الـ template من جوه TS؟ بتاع الـ Component، ممكن تستخدم حاجة اسمها TemplateRef و ViewContainerRef.

الTemplateRef: ده عبارة عن object بيحتوي على الـ template نفسه (اللي موجود جوه ng-template). بنستخدمه عشان نمسك الـ template ونتحكم فيه من الكود.

الViewContainerRef: ده عبارة عن مكان في الـ DOM (الصفحة) تقدر تعرض فيه الـ template في أي وقت. هو بيحدد المكان اللي الـ template هيظهر فيه، وده بيبقى مفيد لما تكون عاوز تضيف أو تحذف أجزاء من الـ DOM بشكل ديناميكي.

 #### مثال باستخدام TemplateRef و ViewContainerRef

 <div dir="auto" align="left">

```typescript
@ViewChild('sayHelloTemplate', { read: TemplateRef }) sayHelloTemplate: TemplateRef<any>;
```

</div>
وبعدين ممكن تستخدمه في الكود علشان تعرضه كده
<div dir="auto" align="left">

```typescript
this.vref.createEmbeddedView(this.sayHelloTemplate);
```

</div>
<div dir="auto" align="left">

```typescript
import { Component, ViewChild, TemplateRef, ViewContainerRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements AfterViewInit {

  @ViewChild('sayHelloTemplate', { read: TemplateRef }) sayHelloTemplate: TemplateRef<any>;

  constructor(private vref: ViewContainerRef) {}

  ngAfterViewInit() {
    this.vref.createEmbeddedView(this.sayHelloTemplate);
  }
}
```

</div>


### ليه استخدمنا AfterViewInit؟
علشان نتاكد إن الـ template بقى جاهز واتحمل في الصفحة، لأن لو جربنا نستخدمه مباشرة في ngOnInit ممكن ميكنش اتحمل بالكامل.

## الng-template مع ngIf
لما تستخدم ngIf، الAngular بيحولها تلقائيًا لـ ng-template   (behind the scenes). يعني بدل ما تكتب الكود بالشكل المعتاد

<div dir="auto" align="left">

```HTML
<div *ngIf="selected">
  <p>You are selected</p>
</div>
```

</div>
تقدر تكتبها باستخدام <ng-template> بالشكل ده:
<div dir="auto" align="left">

```HTML
<ng-template [ngIf]="selected">
  <div>
    <p>You are selected</p>
  </div>
</ng-template>
```

</div>

### طيب إيه اللي بيحصل هنا؟
الAngular لما بيشوف *ngIf بيترجمها تلقائيًا لـ ng-template بحيث لما الشرط يكون true، يعرض اللي جواه، ولو الشرط false، مش هيعرض أي حاجة. فبكده ng-template بيدي مرونة أكبر للتحكم في أماكن العرض وشروطه.

### ليه ممكن تستخدم ng-template بشكل مباشر مع ngIf؟
في حالات ممكن تحتاج تتحكم في طريقة العرض بشكل أوسع من مجرد *ngIf. مثلاً، لو عاوز تعمل أجزاء تانية تظهر لو الشرط كان false، زي استخدام الـ then و else.

#### مثال مع then و else
لو عندك سيناريو فيه محتوى عاوز تعرضه لما الشرط يكون true، ومحتوى تاني لما الشرط يكون false، تقدر تعملها كده
<div dir="auto" align="left">

```HTML
<div *ngIf="selected; then thenBlock else elseBlock"></div>

<ng-template #thenBlock>
  <p> You are selected</p>
</ng-template>

<ng-template #elseBlock>
  <p> You are selected </p>
</ng-template>
```

</div>
</div>
<hr/>


 ## How to Use ngTemplateOutlet in Angular?


 [⬆️ Back to Top](#top)

<div dir="auto" align="right">
في Angular، الـ ngTemplateOutlet هو Directive بيستخدم لعرض Template معين في مكان محدد داخل الـ DOM باستخدام Reference للـ Template ده، وكمان ممكن تمرر معاه بيانات. دي أداة قوية بتسمحلك تستخدم نفس الـ Template أكتر من مرة في أماكن مختلفة وتتحكم في محتواه بناءً على اللي انت محتاجه.

### إزاي نستخدم ngTemplateOutlet
تحديد Template: بنبدأ بكتابة Template باستخدام ng-template، وده بيكون مجرد تصميم مش بيظهر لوحده. لازم نحدد Reference للـ Template ده زي #template1.
<div dir="auto" align="left">

```HTML
<ng-template #template1>
   <p> Template </p>
</ng-template>

```

</div>
استخدام ngTemplateOutlet: عشان نعرض الـ Template ده في مكان معين، بنستخدم ngTemplateOutlet ونعينه للـ Reference اللي حددناه.
<div dir="auto" align="left">

```HTML
<ng-container *ngTemplateOutlet="template1"></ng-container>
```

</div>
تمرير بيانات للـ Template: ممكن نستخدم خاصية ngTemplateOutletContext عشان نمرر بيانات للـ Template كمان. يعني لو عندنا قيمة اسمها value، نقدر نمررها كالتالي:

<div dir="auto" align="left">

```HTML
<ng-template let-value="value" #messageTemplate>
   <p>القيمة اللي وصلت من الـ Parent هي {{value}}</p>
</ng-template>

<ng-container [ngTemplateOutlet]="messageTemplate" [ngTemplateOutletContext]="{value:'1000'}"></ng-container>
```

</div>

### استخدام $implicit
في Angular، استخدام implicit بيسمحلك تمرر قيمة افتراضية لأي متغير محلي (local variable) في ng-template من غير ما تعينها مباشرة للمتغير ده. ببساطة، لو عينت قيمة للـ implicit في ngTemplateOutletContext، المتغيرات اللي ملهاش قيمة صريحة هتاخد القيمة اللي عينتها لـ $implicit.

<div dir="auto" align="left">

```HTML
<ng-template let-name let-message="messageText" #welcomeTemplate>
  <p>hello {{name}}، {{message}}</p>
</ng-template>

<ng-container
    [ngTemplateOutlet]="welcomeTemplate"
    [ngTemplateOutletContext]="{$implicit: 'mohamed', messageText: 'welcome'}">
</ng-container>

<ng-container
    [ngTemplateOutlet]="welcomeTemplate"
    [ngTemplateOutletContext]="{$implicit: 'hassan', messageText: 'welcome'}">
</ng-container>

```

</div>
الlet-name: هنا إحنا بنعرّف متغير محلي اسمه name داخل الـ ng-template. المتغير ده هياخد قيمته من  implicit اللي بنحدده في كل مرة نستخدم فيها الـ Template.

let-message="messageText": هنا بنعرّف متغير محلي تاني اسمه message داخل نفس الـ Template، والمتغير ده هياخد قيمته من  messageText اللي بنمرره في ngTemplateOutletContext.

</div> -->

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
