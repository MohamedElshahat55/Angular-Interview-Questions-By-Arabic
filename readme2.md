 <!-- ## What is View Encapsulation in Angular?

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

### يعني إيه View Encapsulation؟
الـ View Encapsulation في Angular بيساعدنا نتحكم في الاستايلات الخاصة بكل كومبوننت بحيث تكون معزولة وماتأثرش على باقي الكومبوننتات في التطبيق.

 يعني لو عندك استايلات معينة في كومبوننت واحد، مش عايزينها تأثر على استايلات الكومبوننتات التانية.

 ### الAngular بيدعم 3 طرق أو استراتيجيات للتحكم في الاستايلات:

###### الViewEncapsulation.None: بدون عزل للاستايلات (يعني الاستايلات تكون global).
###### الViewEncapsulation.Emulated: عزل وهمي (Emulated Encapsulation).
###### الViewEncapsulation.ShadowDOM: عزل حقيقي باستخدام الـ Shadow DOM.

###  ViewEncapsulation.None
يعني إيه ViewEncapsulation.None؟

لو استخدمت ViewEncapsulation.None، يبقى كده مفيش عزل. الاستايلات اللي بتعملها في الكومبوننت ده هتكون  (Global)، يعني ممكن تأثر على كل العناصر في التطبيق.
<div dir="auto" align="left">

```typescript
import { Component,ViewEncapsulation } from '@angular/core';
 
@Component({
  selector: 'app-none',
  template: `<p>I am not encapsulated and in blue 
             (ViewEncapsulation.None) </p>`,
  styles: ['p { color:blue}'],
  encapsulation: ViewEncapsulation.None
})
export class ViewNoneComponent {
}
```

</div>

#### لو أضفنا الكومبوننت ده في التطبيق، الاستايل color: blue هيأثر على كل ```<p>``` في التطبيق، مش بس جوا الكومبوننت ده.


### 2. ViewEncapsulation.Emulated
يعني إيه ViewEncapsulation.Emulated؟

دي تعتبر الاستراتيجية الافتراضية في . Emulated Encapsulation يعني  الAngular هتضيف حاجة زي أكواد HTML Attributes فريدة للكومبوننت والاستايلات الخاصة به، بحيث تضمن إن الاستايلات دي ماتأثرش على باقي الكومبوننتات.

يعني Angular بتضيف حاجات زي _ngcontent لكل عنصر جوا الكومبوننت عشان تربط الاستايلات الخاصة بيه بيه بس، بحيث تضمن إن الاستايلات ماتخرجش لباقي التطبيق.

<div dir="auto" align="left">

```typescript
import { Component,ViewEncapsulation } from '@angular/core';
 
@Component({
  selector: 'app-emulated',
  template: `<p>Using Emulator</p>`,
  styles: ['p { color:red}'],
  encapsulation: ViewEncapsulation.Emulated
})
export class ViewEmulatedComponent {
}
```

</div>

### إيه اللي بيحصل هنا؟
لما تفتح   (Developer Tools)، هتلاقي Angular ضافت Attribute فريد زي ```_ngcontent-c2``` على عنصر ```<p>``` والاستايلات الخاصة به. ده بيخلي الاستايلات دي تنطبق بس على العناصر اللي جوا الكومبوننت ده، وماتأثرش على باقي التطبيق.

### ViewEncapsulation.ShadowDOM
يعني إيه ViewEncapsulation.ShadowDOM؟

الـ Shadow DOM هو جزء من Web Components وبيوفر عزل حقيقي للاستايلات.

 لما تستخدمه، الاستايلات الخاصة بالكومبوننت ده مش هتخرج بره الكومبوننت، ومش هتأثر على أي عناصر تانية بره الكومبوننت.

ملاحظة: مش كل المتصفحات بتدعم الـ Shadow DOM، فالأفضل تشغل التطبيق على متصفح زي جوجل كروم.

<div dir="auto" align="left">

```typescript
import { Component,ViewEncapsulation } from '@angular/core';
 
@Component({
  selector: 'app-shadowdom',
  template: `<p>I am encapsulated inside a Shadow DOM ViewEncapsulation.ShadowDom</p>`,
  styles: ['p { color:brown}'],
  encapsulation: ViewEncapsulation.ShadowDom
})
export class ViewShadowdomComponent {
 
}
```

</div>

### إيه اللي بيحصل هنا؟
الAngular بترندر الكومبوننت ده جوا عنصر اسمه shadow-root#.

 العنصر ده بيعزل الاستايلات الخاصة بالكومبوننت عن باقي التطبيق، وده بيحقق عزل حقيقي.

### مزايا وعيوب Shadow DOM
مزايا: عزل حقيقي للاستايلات، وبكده تضمن إن الاستايلات ماتأثرش على أي حاجة بره الكومبوننت.

عيوب: مش كل المتصفحات بتدعمه، وبعض الاستايلات المشتركة بين الكومبوننتات ممكن ماتشتغلش زي ما تتوقع.

### 🚀 الخلاصة
الViewEncapsulation.None: استخدامه لما تكون عايز الاستايلات تأثر على التطبيق كله.

الViewEncapsulation.Emulated: الاختيار الافتراضي، بيعزل الاستايلات باستخدام ng-content.

الViewEncapsulation.ShadowDOM: بيعزل الاستايلات بشكل كامل لكن ممكن مايشتغلش على كل المتصفحات.
</div>

 ## What are Host and hostContext in angular? 

 [⬆️ Back to Top](#top)

<div dir="auto" align="right">

### أولاً: إيه هو host:؟
الhost هو CSS Selector بنستخدمه في Angular عشان نستهدف العنصر الأساسي بتاع الكومبوننت نفسه.

 لما بتستخدمه، هو بيخليك تضيف استايلات على العنصر الرئيسي للكومبوننت من غير ما تتعرض للعناصر اللي جواه أو من غير ما تضطر تضيف كلاس معين عليه.

 ### ليه بنستخدم :host في Angular
 
  كل كومبوننت بيبقى ليه استايلات خاصة بيه، ولو عايز تضيف استايل للعنصر الأساسي بتاع الكومبوننت من غير ما تأثر على باقي الكومبوننتات أو محتوى الصفحة، هنا :host بيبقى مفيد.

  ### مثال عملي:
خلينا نقول عندك كومبوننت اسمه app-card وعايز تخلي العنصر الأساسي  يظهر بحدود (border) ولون خلفية (background color) محددين.
<div dir="auto" align="left">

```typescript
@Component({
  selector: 'app-card',
  template: `
    <div class="content">
      <p>this is a content</p>
    </div>
  `,
  styles: [`
    :host {
      display: block;
      border: 2px solid #333;
      background-color: #f9f9f9;
      padding: 16px;
      border-radius: 8px;
    }
  `]
})
export class CardComponent { }
```

</div>

الـ :host هنا بيخلي الاستايلات تطبق على العنصر الأساسي بتاع app-card نفسه.

مش محتاج تضيف كلاس أو تعمل حاجة مخصوص للعنصر الرئيسي، لأن :host بيفهم لوحده إن ده هو العنصر الحاوي للكومبوننت، وبيطبق عليه الاستايلات مباشرة.

### ثانياً: إيه هو :host-context؟
الhost-context هو CSS Selector بيستخدم في Angular عشان تتحكم في الاستايلات بناءً على السياق الخارجي للكومبوننت. يعني بيشوف الكومبوننت موجود فين أو جواه إيه، ويطبق الاستايلات بناءً على ده.

تخيل :host-context زي شرط بيقول: "لو الكومبوننت موجود في سياق معين أو محاط بعنصر معين، يبقى طبق الاستايل ده".


### مثال

افترض إن عندك كومبوننت في Angular فيه عنصر ```<input>```، وعايز هذا الكومبوننت يظهر بشكل مختلف بناءً على المكان اللي بيتواجد فيه. يعني مثلًا:

لو الكومبوننت ده موجود جوا Dropdown، عايز عرض الـ ```<input>``` يكون 50%.

لو الكومبوننت ده موجود جوا Table، عايز عرض الـ ```<input>``` يكون 100%.

### إزاي نستخدم :host-context في المثال بتاعنا؟
لو عندنا كومبوننت MyInputComponent اللي فيه ```<input>```، عايزين نخليه يغير عرضه بناءً على المكان اللي هو فيه.

الكومبوننت MyInputComponent هيظهر في أماكن مختلفة، زي my-dropdown و my-table.

لو الكومبوننت ده جوه ```<my-dropdown>```، العرض يكون 50%.
لو الكومبوننت ده جوه ```<my-table>```، العرض يكون 100%.
<div dir="auto" align="left">

```CSS
:host-context(my-dropdown) input {
  width: 50%; /* العرض لما يكون جوا dropdown */
}

:host-context(my-table) input {
  width: 100%; /* العرض لما يكون جوا table */
}
```

</div>

ال:host-context(my-dropdown) input: ده بيقول إنه لو الكومبوننت MyInputComponent موجود جوا عنصر ```<my-dropdown>```، يخلي عرض ```<input>``` في الكومبوننت ده 50%.

ال:host-context(my-table) input: ده بيقول إنه لو الكومبوننت MyInputComponent موجود جوا ```<my-table>```، يخلي عرض ```<input>``` في الكومبوننت ده 100%.

دلوقتي لو حطيت MyInputComponent جوا <my-dropdown> أو <my-table>، هيتم تطبيق الاستايل اللي يناسب السياق بشكل تلقائي.

<div dir="auto" align="left">

```HTML
<my-dropdown>
  <my-input></my-input> <!-- العرض 50% هنا عشان موجود في dropdown -->
</my-dropdown>

<my-table>
  <my-input></my-input> <!-- العرض 100% هنا عشان موجود في table -->
</my-table>
```

</div>

### ليه host-context مفيد في الحالة دي؟

بدل ما تكتب كود إضافي في كل مكان أو تضيف كلاس جديد للتحكم في الاستايل، host-context بيسهل عليك التحكم في استايلات الكومبوننت بناءً على السياق الخارجي اللي الكومبوننت موجود فيه، من غير ما تعدل على الكومبوننت نفسه كل مرة.

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
