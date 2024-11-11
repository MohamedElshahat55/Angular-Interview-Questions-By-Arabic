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

<!-- ## Angular Signals Component API input and output and model

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

في أنجولار، بقت في طريقة جديدة لكتابة الcomponents والdirectives والpipes، والطريقة دي اسمها Signal Components، وهي أبسط وأقوى من الطريقة التقليدية.


الSignal Components هي بديل كامل للdecorators زي ```Input``` و ```Output```. كمان بتوفر طريقة جديدة لعمل two-way binding (التواصل رايح جاي). والمفروض إن دي تبقى الطريقة المفضلة اللي تكتب بيها الcomponents الجديدة في أنجولار من دلوقتي، وبالمناسبة هي جاهزة للاستخدام حالياً.

الميزة الأساسية في Signal Components إنها مش محتاجة decorators، وكمان مفيش أغلب lifecycle hooks اللي متعودين عليها، لأنها متكاملة بشكل عميق مع الإشارات (signals).

لو عايز تستفيد من Signal Components، لازم تحدث لنسخة Angular 17.3 أو أعلى.

في الدليل ده، حاشرح إزاي تكتب components بطريقة Signal، وإزاي تستخدم الأدوات الأساسية زي input و output و model عشان تبني Signal Components في أنجولار.

<div dir="auto" align="left">

### Signal inputs with input()

</div>

الـinput() function بقت بديل للـInput() decorator، وده بيعتبر طريقة جديدة في Angular للتعامل مع الـinputs.

لكن مهم تعرف إن Input() decorator لسه شغال وهيفضل مدعوم لفترة جاية.

لما نستخدم input، القيمة اللي بنحطها للـinput property بتتحول لحاجة اسمها Signal. بمعنى إن الـSignal ده بيحتفظ دايمًا بأحدث قيمة متاحة للـinput اللي جاية من الجزء الأب أو الـparent.

مثال عملي: هنشوف إزاي نعمل input property اسمها book في BookComponent

<div dir="auto" align="left">

```typescript
import { Component, input } from "@angular/core";

@Component({...})
class BookComponent {
 book = input<Book>()
}
```

</div>

هنا استخدمنا input عشان نعمل input field اسمها book.

الفرق هنا إن input بيرجع قيمة نوعها ```InputSignal<Book>``` . وده معناه إن book مش مجرد object عادي زي الطريقة القديمة باستخدام @Input، لكنها بقت حاجة بتحافظ دايمًا على آخر قيمة جايه من الجزء الأب.

لكن بالرغم من استخدام الطريقة الجديدة، من ناحية الجزء الأب اللي بيبعت البيانات للـBookComponent، مفيش أي تغيير. تقدر تبعت بيانات بالطريقة المعتادة:
<div dir="auto" align="left">

```HTML
<book [book]="angularCoreDeepDiveBook" />
```

</div>
 <div dir="auto" align="left">

```typescript
angularCoreDeepDiveBook = {
  title: "Angular Core Deep Dive",
  synopsis: "A deep dive into Angular core concepts",
};
```

</div>
<div dir="auto" align="left">

### Reading input() values

</div>

من ناحية الـ Parent Component، كل حاجة بتفضل زي ما هي.

لكن بالنسبة للـ Component نفسه، إزاي نقدر نجيب قيمة الـ input؟

علشان نقرا القيمة، محتاجين نستدعي الـ Signal بتاع الـ book، زي أي Signal تاني في Angular:

<div dir="auto" align="left">

```typescript
book();
```

</div>

السطر ده لما نستدعيه، هيجيب لنا أحدث قيمة موجودة في book signal، اللي فيها قيمة angularBook object.

خلي بالك إن Signals دايمًا بيكون ليها قيمة، فـ ()book هترجع لنا يا إما undefined لو مفيش حاجة، أو قيمة book object.

دلوقتي هنعدل الـ Component بتاعنا علشان نعرض title وsynopsis بتوع الكتاب في template بتاعه:

<div dir="auto" align="left">

```typescript
import { Component, input } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
  </div> `,
})
class BookComponent {
  book = input<Book>();
}
```

</div>

لاحظ إننا في template استدعينا الـ Signal بتاع ()book، وبعد كده دخلنا على الـ title وsynopsis properties.

استخدمنا ?. (الـ Optional Chaining) علشان لو الـ book ممكن يبقى undefined.

الكود ده شغال، لكن ممكن يبقى متعب شوية.

طب إيه اللي هيحصل لو إحنا متأكدين وضامنين إن قيمة book عمرها ما هتكون undefined؟

هنا بقى يظهر لنا الفرق بين نوعين من Signal Inputs اللي ممكن نستخدمهم في Angular:

#### Optional Inputs
#### Required Inputs

<div dir="auto" align="left">

### Optional signal inputs

</div>

بشكل افتراضي، inputs اللي بنعملها باستخدام ()input بتعتبر optional.

ده معناه إننا مش مضطرين نحدد قيمة للـ input لما نستخدم component ده من جوه parent component.

المثال اللي استخدمناه فوق مع BookComponent كان optional input.

وده معناه حاجتين مهمين:

أول حاجة، ممكن نستخدم BookComponent من غير ما نحدد قيمة للـ book input:
<div dir="auto" align="left">

```HTML
<book />
```

</div>

تاني حاجة، في الحالة دي، الـ book signal هيبقى قيمته undefined.

لو مش عايزين تبقى القيمة الافتراضية هي undefined، ممكن كمان نحدد قيمة مبدئية للـ optional input كالتالي:
<div dir="auto" align="left">

```typescript
const age = input<number>(0);
```

</div>

كده، القيمة المبدئية للـ age input signal هتبقى 0 بدل undefined.

<div dir="auto" align="left">

### Making an input to be required

</div>

في بعض الحالات، بنحتاج إن input properties تكون required بدل ما تبقى optional. وده بيكون مفيد لما نكون عايزين نضمن إن قيمة معينة هتكون موجودة دايمًا.

إزاي نعمل ده؟ ببساطة، بنستخدم input.required بالشكل ده:

<div dir="auto" align="left">

```typescript
import { Component, input } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book().title }}</b>
    <div>{{ book().synopsis }}</div>
  </div> `,
  styles: ``,
})
class BookComponent {
  book = input.required<Book>();
}
```

</div>

فيه شوية حاجات مهمة لما بنستخدم input.required

🔴 مش ممكن نحدد قيمة مبدئية للـ input signal. القيمة الأولية هتبقى هي   القيمة اللي بنمررها للـ input من الـ parent component.

🔴 ماينفعش نهمل الـ book property في الـ parent component

<div dir="auto" align="left">

```HTML
<book />
```

</div>

لو عملنا كده، هيظهر خطأ في الـ compilation لأن الـ book input field مش optional دلوقتي!

علشان نحل المشكلة دي، لازم نمرر قيمة للـ book property لما نستخدم BookComponent:

<div dir="auto" align="left">

```HTML
<book [book]="angularBook" />
```

</div>
وبكده نكون غطينا أساسيات الفرق بين optional وrequired inputs.

<div dir="auto" align="left">

### Setting an input property alias

</div>

غالبًا، بنحب نخلي اسم input property هو نفسه اسم input signal.

لكن أحيانًا ممكن نحتاج ندي الـ input property اسم مختلف، وده نادرًا ما بيحصل، لكنه مفيد في بعض الحالات.

لو واجهت موقف زي ده، دي الطريقة اللي تقدر تعمل بيها input alias سواء للـ optional أو required inputs:

لعمل alias لـ optional input:

<div dir="auto" align="left">

```typescript
book = input<Book>(null, {
  alias: "bookInput",
});
```

</div>
لعمل alias لـ required input:

<div dir="auto" align="left">

```typescript
book = input.required<Book>({
  alias: "bookInput",
});
```

</div>

إزاي نستخدم الـ input alias في parent component:
لما نيجي نستخدم الـ alias في parent component، بيكون بالشكل ده:
<div dir="auto" align="left">

```HTML
<book [bookInput]="angularBook" />
```

</div>

### 🔴 ملاحظة:
لو حاولت تستخدم اسم الـ input property الأصلي بدل alias، زي كده:
<div dir="auto" align="left">

```HTML
<book [book]="angularBook" />
```

</div>

####  ❌ الكود مش هيشتغل، وهيطلع لك خطأ

<div dir="auto" align="left">

### Input value transformation: the transform function

</div>

في بعض الحالات النادرة، ممكن نحتاج نعدل قيمة الـ input قبل ما تتخزن في input signal.

بنعمل كده عن طريق استخدام input transform، اللي بيخلينا نغير البيانات اللي جاية من parent component قبل ما تتخزن.

دي الطريقة اللي نقدر نحدد بيها input transforms سواء للـ optional أو required inputs:

للـ optional input:

<div dir="auto" align="left">

```typescript
book = input(null, {
  transform: (value: Book | null) => {
    if (!value) return null;

    value.title += " :TRANSFORMED";

    return value;
  },
});
```

</div>

للـ required input:

<div dir="auto" align="left">

```typescript
book = input.required({
  transform: (value: Book | null) => {
    if (!value) return null;

    value.title += " :TRANSFORMED";

    return value;
  },
});
```

</div>

####  🔴ملاحظة:
قيمة خاصية transform لازم تكون pure function، يعني دالة بتشتغل بدون side effects (تأثيرات جانبية).

في الدالة دي بنكتب منطق تحويل القيمة اللي محتاجينه، ومهم جدًا إننا نرجع قيمة من الدالة علشان الـ transform يشتغل صح.

<div dir="auto" align="left">

### Deriving values from signal inputs

</div>

بما إن input في الأساس هو مجرد signal، نقدر نعمل بيه كل اللي بنعمله مع أي signal تاني، وده بيشمل حساب derived signal منه.

إزاي نقدر نعمل derived signal من input signal باستخدام computed:

<div dir="auto" align="left">

```typescript
import { Component, input, computed } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
    <div>{{ bookLength() }}</div>
  </div> `,
  styles: ``,
})
class BookComponent {
  book = input.required<Book>();

  bookLength = computed(() => this.book().title.length);
}
```

</div>

في الكود ده، bookLength هو derived signal ناتج من book signal.

بمعنى، في أي وقت تتغير فيه قيمة book input signal، الـ bookLength signal هيتم حسابه من جديد.

كمان ممكن نستخدم effect علشان نراقب أي تغييرات بتحصل في book signal لو حابين.

خلوا في بالكم، input signal هو مجرد read-only signal، يعني مفيش حاجة خاصة بيه، تقدروا تعملوا عليه كل العمليات اللي ممكن تعملوها مع أي signal تاني.

<div dir="auto" align="left">

### No more need for the OnChanges lifecycle hook

</div>

استخدام signal inputs بدلًا من Input() decorator بيدينا فائدة مخفية وهي تبسيط عملية متابعة التغييرات في الـ input بدون الحاجة لاستخدام OnChanges lifecycle hook.

خلينا نوضح ده بمثال:

الطريقة التقليدية باستخدام Input@ و OnChanges:
في الطريقة القديمة، لو عايزين نتابع تغييرات الـ input بنستخدم OnChanges بالشكل ده:

<div dir="auto" align="left">

```typescript
import { Component, Input, OnChanges, SimpleChanges } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book?.title }}</b>
    <div>{{ book?.synopsis }}</div>
  </div> `,
})
class BookComponent implements OnChanges {
  @Input() book: Book;

  ngOnChanges(changes: SimpleChanges) {
    if (changes["book"]) {
      console.log("Book changed: ", changes.book.currentValue);
    }
  }
}
```

</div>

الطريقة الجديدة باستخدام signals وeffect

دلوقتي، مع نظام signal-based الجديد، مابقيناش محتاجين OnChanges lifecycle hook. بدل كده، بنستخدم effect لمتابعة أي تغيير يحصل في input signal بشكل مباشر:
<div dir="auto" align="left">

```typescript
import { Component, input, effect } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
  </div> `,
  styles: ``,
})
class BookComponent {
  book = input.required<Book>();

  constructor() {
    effect(() => {
      console.log("Book changed: ", this.book());
    });
  }
}
```

</div>

### الفكرة الأساسية:
بدون الحاجة لأي lifecycle hook خاص، مجرد استدعاء effect بيكون كافي علشان يتابع أي تغييرات تحصل في input signal.

<div dir="auto" align="left">

### Angular component outputs with output()

</div>

الـ output() API هو بديل مباشر للـ Output() decorator التقليدي في Angular.

رغم إن Output مش هيتم إيقافه، لكن استخدام output بيخلي كتابة الكود أكثر تناسقًا، خاصة لو كنا بنستخدم input، وبيقدم طريقة أكثر type-safe وأفضل تكاملًا مع RxJs مقارنة بالطريقة القديمة اللي بتستخدم EventEmitter.

إزاي نستخدم output لتحديد component output في Angular:

<div dir="auto" align="left">

```typescript
import { Component, output } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
    <button (click)="onDelete()">Delete Book</button>
  </div>`,
})
class BookComponent {
  deleteBook = output<Book>();

  onDelete() {
    this.deleteBook.emit({
      title: "Angular Deep Dive",
      synopsis: "A deep dive into Angular core concepts",
    });
  }
}
```

</div>

من وجهة نظر parent component

بنفس طريقة event handling المعتادة، الـ parent component ممكن يستمع لحدث
deleteBook بالشكل ده:
<div dir="auto" align="left">

```HTML
<book (deleteBook)="deleteBookEvent($event)" />
```

</div>
وفي  deleteBookEvent، هنستقبل قيمة book اللي تم إرسالها ونقدر نستخدمها في الكود:
<div dir="auto" align="left">

```typescript
deleteBookEvent(book: Book) {
  console.log(book);
}
```

</div>

<div dir="auto" align="left">

### Setting an alias on an output()

</div>

زي ما قدرنا نحدد alias للـ signal inputs، كمان ممكن نحدد alias للـ output بالطريقة دي

<div dir="auto" align="left">

```typescript
deleteBook = output<Book>({
  alias: "deleteBookOutput",
});
```

</div>
إزاي parent component يستخدم الـ alias:
لما نحدد alias، الـ parent component هيستخدم الاسم الجديد deleteBookOutput للاستماع للحدث:
<div dir="auto" align="left">

```HTML
<book (deleteBookOutput)="deleteBookEvent($event)" />
```

</div>

<div dir="auto" align="left">

### output() RxJs Interoperability using outputFromObservable()

</div>

زي ما وضحنا، الـ ()output مش مبني على signals، لكنه أكتر type-safe من الـ Output@ التقليدي، وبيوفر تكامل أفضل مع RxJs.

واحدة من الميزات القوية هي إننا نقدر بسهولة نعمل output signal بيصدر القيم من Observable.

علشان نعمل ده، بنستخدم outputFromObservable، ودي الطريقة:

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";
import { outputFromObservable } from "@angular/core/rxjs-interop";
import { of } from "rxjs";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
  </div>`,
})
class BookComponent {
  deleteBook = outputFromObservable<Book>(
    of({
      title: "Angular Core Deep Dive",
      synopsis: "A deep dive into the core features of Angular.",
    })
  );
}
```

</div>

🚀 الميزة هنا هي إننا نقدر نربط بين Observables وoutputs في Angular بشكل مباشر، وده بيسهل الشغل مع streams وتكامل RxJs، خصوصًا لو بنعتمد على reactive programming.

<div dir="auto" align="left">

### output() RxJs interoperability with outputToObservable()

</div>

زي ما قدرنا نحول Observable لـ output باستخدام outputFromObservable، ممكن كمان نحول output إلى Observable باستخدام outputToObservable.

دي الطريقة:

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";
import { output, outputToObservable } from "@angular/core/rxjs-interop";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <b>{{ book()?.title }}</b>
    <div>{{ book()?.synopsis }}</div>
    <button (click)="onDelete()">Delete Book</button>
  </div>`,
})
class BookComponent {
  deleteBook = output<Book>();

  deleteBookObservable$ = outputToObservable(this.deleteBook);

  constructor() {
    this.deleteBookObservable$.subscribe((book: Book) => {
      console.log("Book emitted: ", book);
    });
  }

  onDelete() {
    this.deleteBook.emit({
      title: "Angular Core Deep Dive",
      synopsis: "A deep dive into Angular core concepts",
    });
  }
}
```

</div>

استخدمنا outputToObservable لتحويل deleteBook output إلى Observable اسمه deleteBookObservable$.

دلوقتي أي قيمة بيصدرها deleteBook output، هيتم استقبالها برضه في deleteBookObservable$.

استخدمنا subscribe لمتابعة القيم الصادرة وطباعة أي book object جديد في الكونسول.

🚀 الميزة هنا هي إننا نقدر نشتغل مع outputs كـ Observables، وده بيسهل التكامل مع RxJs وreactive programming.

<div dir="auto" align="left">

### What is the model() API?

</div>

بالإضافة إلى ```()input``` و ```()output```، أضافت Angular API جديدة اسمها ```()model```، واللي بنستخدمها لإنشاء model inputs.

#### ما هو Model Input؟
الModel Input هو نوع خاص من inputs بيكون writeable، يعني قابل للقراءة والكتابة! وده معناه إننا بنقدر نعمل two-way data binding بين الـ parent component والـ child component.

ببساطة،  بيسمح للـ parent component إنه يمرر بيانات للـ child component، وفي نفس الوقت، child component يقدر يرجع بيانات للـ parent component.

مثال على استخدام ```()model```
خلينا نشوف مثال يوضح استخدام ```()model``` في two-way binding:

<div dir="auto" align="left">

```typescript
import { Component, model } from "@angular/core";

@Component({
  selector: "book",
  standalone: true,
  template: `<div class="book-card">
    <input [(ngModel)]="bookModel().title" />
    <div>{{ bookModel().synopsis }}</div>
    <button (click)="updateBook()">Update Book</button>
  </div>`,
})
class BookComponent {
  bookModel = model<Book>();

  updateBook() {
    const updatedBook = {
      ...this.bookModel(),
      title: "Updated Title",
    };
    this.bookModel.set(updatedBook); // Emit updated data to the parent
  }
}
```

</div>

الـ parent component ممكن يمرر قيمة للـ model باستخدام [(bookModel)] بالطريقة المعتادة.
child component يقدر يقرأ أو يعدل قيمة الـ model input، ولما يعمل تعديل باستخدام ()set, البيانات الجديدة بتترجع للـ parent component مباشرة.

من منظور parent component:
<div dir="auto" align="left">

```HTML
<book [(bookModel)]="parentBook"></book>
```

</div>
الـ parentBook هتتحدث تلقائيًا لما child component يغير قيمة الـ model.

<div dir="auto" align="left">

### When to use model()?

</div>

في بعض الحالات، مثلًا لو عندنا date picker component بيحتوي على قيمة رئيسية (زي قيمة date نفسها)، ```()model```ممكن يكون مفيد جدًا. في المثال ده:

الparent component هيحدد initial value للتاريخ.

الchild component يقدر يرجع القيم المحدثة للـ parent لما المستخدم يغيرها.

 ✨ومع ذلك، في الغالب:

يفضل استخدام inputs وoutputs العادية لأنها أكثر وضوحًا وأسهل في الفهم.

ال```()model``` لو تم استخدامها بدون سبب قوي، ممكن تؤدي لكتابة كود صعب الفهم وصعب تتبعه أثناء الـ debugging.

تخيل إنك بتستخدم model input عبر عدة مستويات من components متداخلة، هيبقى صعب تعرف مصدر قيمة معينة أثناء تتبع الأخطاء.

</div> -->

<!-- <div dir="auto" align="left">

```typescript

```

</div>
<div dir="auto" align="left">

```HTML

```

</div> -->
