 <!-- ## ElementRef in Angular

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

### ما هو ElementRef؟
 الElementRef هو Object بيتيح لنا الوصول المباشر للعنصر في الـDOM من داخل الكومبوننت أو الديركتيف.
 
  غالبًا، في أغلب حالات الـAngular، بنعتمد على  (Bindings) , (Directives) لتغيير الـDOM بشكل غير مباشر، لكن في حالات معينة، بنحتاج نوصل للعنصر نفسه عشان نعمل عمليات خاصة عليه، زي التفاعل مع مكتبات JavaScript خارجية أو إجراء تعديلات معينة على العنصر مباشرة.

  ### ليه نحتاج ElementRef؟
أحيانًا نحتاج نعدل حاجة محددة في العنصر مباشرة، مش كل حاجة بتكون ممكنة بالـAngular bindings. على سبيل المثال:

إضافة أو تعديل بعض الخصائص  (CSS Styles) بشكل ديناميكي.

التعامل مع مكتبات JavaScript خارجية محتاجة الـDOM Element مباشرة.

تنفيذ تعديلات أو تنقلات مباشرة على العنصر مش ممكنة بسهولة بالـAngular.

###  إزاي نستخدم ElementRef؟
##### أول خطوة: إنشاء Template Reference Variable
أول حاجة، عشان تقدر تستخدم ElementRef، لازم تنشئ حاجة اسمها Template Reference Variable في التيمبلت.

 ده بيكون متغير بيشير للعنصر اللي عاوز توصله، وبتكتبه بالشكل ده في الـHTML بتاعك:

<div dir="auto" align="left">

```HTML
<div #hello>Hello Angular</div>
```

</div> 
هنا، hello# ده هو Template Reference Variable للعنصر div

. بيدينا زي اسم داخلي نقدر نوصل بيه للعنصر ده من كود الكومبوننت.

#### الخطوة الثانية: الوصول لـ ElementRef باستخدام ViewChild
عشان نستخدم hello جوه كود الكومبوننت، بنستعمل ViewChild@، وده بيسمح لـAngular إنه يححقن لنا refrence للعنصر في الكومبوننت بشكل مباشر.

<div dir="auto" align="left">

```typescript
import { Component, ElementRef, ViewChild } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<div #hello>Hello Angular</div>`
})
export class AppComponent {
  @ViewChild('hello', { static: false }) divHello: ElementRef;

  ngAfterViewInit() {
    console.log(this.divHello.nativeElement.innerText); // هيطبع 'Hello Angular'
  }
}
```

</div>



هنا، ViewChild@ بيعمل ربط بين المتغير divHello والـElementRef للعنصر اللي عليه الـTemplate Reference Variable hello.

##### nativeElement
بداخل ElementRef، عندنا خاصية nativeElement اللي بترجع العنصر نفسه من الـDOM، وبالتالي تقدر تتعامل مع العنصر مباشرة زي ما بتعمل في JavaScript العادي.

#### استخدام الـRead Token لما يكون في ديركتيف تاني على العنصر
أحيانًا بيكون في ديركتيفات على نفس العنصر زي ngModel. لو عاوز توصل للعنصر نفسه كـElementRef بدل ما توصل للديركتيف ngModel، هنا بييجي دور الـread token. ده بيساعدنا نحدد نوع المرجع اللي محتاجينه (سواء ElementRef أو ديركتيف زي NgModel).

#### مثال مع ngModel
مثلاً عندنا input عليه ngModel كالتالي:
<div dir="auto" align="left">

```HTML
<input #nameInput [(ngModel)]="name">
```

</div> 
في المثال ده، عاوزين نوصل للعنصر نفسه كـElementRef أو نوصل للـngModel لو محتاجين نشتغل بيه. نقدر نحدد ده باستخدام read بالشكل التالي:

<div dir="auto" align="left">

```typescript
import { Component, ElementRef, ViewChild } from '@angular/core';
import { NgModel } from '@angular/forms';

@Component({
  selector: 'app-root',
  template: `<input #nameInput [(ngModel)]="name">`
})
export class AppComponent {
  name: string;

  // هنا بنطلب الـ ElementRef للعنصر input
  @ViewChild('nameInput', { static: false, read: ElementRef }) elRef: ElementRef;

  // هنا بنطلب ngModel المرتبط بالعنصر
  @ViewChild('nameInput', { static: false, read: NgModel }) inRef: NgModel;

  ngAfterViewInit() {
    console.log(this.elRef.nativeElement); // بيرجع العنصر `<input>`
    console.log(this.inRef.model);         // بيرجع القيمة المرتبطة بـ ngModel
  }
}
```

</div>

### ElementRef in Custom Directive
استخدام ElementRef في ديركتيف مخصص بيتيح لك تتعامل مع host element للديركتيف بشكل مباشر، زي ما بيظهر في مثال ttClass اللي عملنا فيه ديركتيف بيضيف كلاس معين للعنصر.

#### مثال: ديركتيف ttClass
في الكود اللي كتبناه، ttClass هو ديركتيف مخصص بيستخدم ElementRef للوصول للعنصر host element وإضافة كلاس معين عليه، زي كالتالي:
<div dir="auto" align="left">

```typescript
import { Directive, ElementRef, Input, OnInit } from '@angular/core';

@Directive({
  selector: '[ttClass]',  
})
export class ttClassDirective implements OnInit {
  @Input() ttClass: string;  

  constructor(private el: ElementRef) { }

  ngOnInit() {
    this.el.nativeElement.classList.add(this.ttClass);
  }
}
```

</div>

### استخدامه في HTML:
لما تستخدم الديركتيف ttClass، هتكتب زي كده في الـHTML:
<div dir="auto" align="left">

```HTML
<div ttClass="highlight">Hello World!</div>
```

</div>
الكود ده هيضيف الكلاس highlight للعنصر div.

### 🔴 ملاحظات مهمة عند استخدام ElementRef


الElementRef بيسمح لك تتعامل مع العناصر مباشرةً، لكن Angular بتحذر من الاعتماد عليه كتير لأنه بيخلي التطبيق مرتبط جدًا بطريقة عرض العناصر، وده ممكن يسبب مشاكل في بعض الحالات، زي لما تتعامل مع Web Workers أو Server-side rendering. Renderer2 يعتبر بديل آمن لأنه بيسمح لك تتعامل مع العناصر بطريقة بتشتغل في بيئات مختلفة بدون الاعتماد المباشر على DOM.

### حماية ضد XSS Injection Attacks
استخدام ElementRef بطريقة غير صحيحة ممكن يعرض التطبيق لمشاكل أمنية زي هجمات XSS (Cross-Site Scripting). 

### بديل آمن: Renderer2
الRenderer2 هو API من Angular بيتيح لك التعامل مع الـDOM بشكل آمن ويتوافق مع بيئات مختلفة.

### ✨ الخلاصة
الElementRef مفيد في بعض الحالات لكنه يحتاج حذر لأنه مرتبط مباشرةً بالـDOM.

الRenderer2 هو الخيار الأفضل لو محتاج تضمن أمان أكتر في التعامل مع العناصر.
</div>


 ## What is Renderer2 ?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

الRenderer2 في Angular هو API بيتيح لك تتعامل مع عناصر الـ DOM بطريقة آمنة ومتوافقة مع بيئات مختلفة، وده بيكون أفضل من التعامل المباشر مع الـ DOM باستخدام ElementRef. 

الRenderer2 بيستخدم في حالات زي إضافة أو إزالة كلاس، تغيير ستايلات CSS، التعامل مع الأحداث، وإضافة أو حذف عناصر في الـ DOM.

### ليه نستخدم Renderer2 بدل ElementRef؟

لو استخدمت ElementRef للتعامل مع الـ DOM مباشرة، هيشتغل في المتصفح (Browser) بس. لكن لو عاوز تشغل التطبيق بتاعك في بيئات تانية زي:

الWeb Workers (لتشغيل الكود بعيدًا عن الواجهة الأساسية).

الServer-Side Rendering (لتحميل التطبيق من السيرفر زي Angular Universal).

تطبيقات الموبايل وسطح المكتب.

✅ الـ Renderer2 بيخلي الكود متوافق ويشتغل في كل البيئات دي، لأنه بيعمل كـ "طبقة وسطية" بين كودك وعناصر الـ DOM.

### استخدامات Renderer2
1. تغيير الخصائص (Properties) والستايلات (Styles)
بدل ما تستخدم ElementRef.nativeElement.style، تقدر تستخدم Renderer2 لإضافة أو إزالة ستايلات على العنصر. زي كده:

<div dir="auto" align="left">

```typescript
@ViewChild('myDiv') myDiv: ElementRef;

constructor(private renderer: Renderer2) {}

addStyle() {
  this.renderer.setStyle(this.myDiv.nativeElement, 'color', 'blue'); // يغير اللون للأزرق
}

removeStyle() {
  this.renderer.removeStyle(this.myDiv.nativeElement, 'color'); // يشيل اللون
}
```

</div>

### 2. إضافة أو إزالة كلاس
ممكن تضيف أو تشيل كلاس للعنصر زي addClass وremoveClass

<div dir="auto" align="left">

```typescript
addClass() {
  this.renderer.addClass(this.myDiv.nativeElement, 'highlight');
}

removeClass() {
  this.renderer.removeClass(this.myDiv.nativeElement, 'highlight');
}
```

</div>

### 3. التعامل مع events
ممكن كمان تستخدم Renderer2.listen عشان تتعامل مع الأحداث بطريقة آمنة ومتوافقة مع Angular

<div dir="auto" align="left">

```typescript
ngAfterViewInit() {
  this.clickListener = this.renderer.listen(this.myDiv.nativeElement, 'click', () => {
    console.log('Div clicked!');
  });
}

ngOnDestroy() {
  this.clickListener(); // تلغي الاشتراك في الحدث عشان ما يبقاش فيه تسريب للذاكرة
}
```

</div>

### 4. إنشاء عناصر جديدة وإضافتها
تقدر تنشئ عناصر جديدة وتضيفها للـ DOM باستخدام Renderer2

<div dir="auto" align="left">

```typescript
createElement() {
  const newDiv = this.renderer.createElement('div');
  const text = this.renderer.createText('Hello Angular');
  
  this.renderer.appendChild(newDiv, text); // تضيف النص للعنصر
  this.renderer.appendChild(this.myDiv.nativeElement, newDiv); // تضيف العنصر للـ DOM
}
```

</div>

</div> -->

 <!-- <hr/>
 ## How to Use Resolve Guard

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
