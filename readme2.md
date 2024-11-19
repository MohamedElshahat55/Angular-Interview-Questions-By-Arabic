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

## Angular Signal Queries: viewChild, contentChild, viewChildren, contentChildren

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

مع ظهور الـ Signals في Angular، بقى عندنا دلوقتي طريقة جديدة تماماً لكتابة الـ Components في Angular باستخدام الـ Signal-based APIs، ومن غير الحاجة للـ Decorators.

جزء كبير من الطريقة الجديدة دي في كتابة الـ Components هو إدخال حاجة جديدة اسمها Signal-based Template Queries

<div dir="auto" align="left">

#### viewChild()

#### contentChild()

#### viewChildren()

#### contentChildren()

</div>

الـ APIs دي بقت بديل جديد عن الـ Decorator-based Template Queries التقليدية زي ViewChild@، ContentChild@، ViewChildren@، و ContentChildren@.

🔴 بيشتغلوا بنفس الطريقة بالظبط، لكن:

#### بقى نظامهم Signal-based

#### أسهل في الفهم والاستخدام

#### سهل تدمجهم مع أي Signals تانية

#### وفي العادي مش محتاجين تستخدم معاهم الـ Lifecycle Hooks

هنتعمق في التفاصيل بتاعت الـ Signal Queries دي، وهنستكشف الـ Syntax بتاعهم، طرق استخدامهم، والمميزات اللي بتخليهم أحسن من الـ Traditional Decorator-based Queries.

<div dir="auto" align="left">

### What is viewChild()?

</div>

الviewChild ده أسلوب بنستخدمه عشان نوصل لعناصر موجودة جوه تصميم (template) الكومبوننت بتاعنا.

العناصر دي ممكن تكون يا إما أجزاء (components) تانية معمولالها design في Angular أو عناصر HTML عادية زي `<div>` و `<button>`.

الـ viewChild بيعمل نفس وظيفة الـ ViewChild decorator، يعني الاتنين بيساعدونا نوصل للعناصر دي ونتعامل معاها.

هنبدأ الأول إزاي نوصل لعناصر الـ HTML العادية، وبعد كده هنشوف إزاي نوصل للكومبوننتات (components)

<div dir="auto" align="left">

### Querying plain HTML elements with viewChild()

</div>

عشان نجيب عنصر من الـtemplate، لازم نديله "template reference" باستخدام علامة #.

ده مثال على الطريقة:

<div dir="auto" align="left">

```typescript
@Component({
  selector: "book",
  template: `
    <div>
      <b #title>Title</b>
    </div>
  `,
})
class BookComponent {
  title = viewChild<ElementRef>("title");

  constructor() {
    effect(() => {
      console.log("Title: ", this.title()?.nativeElement);
    });
  }
}
```

</div>

زي ما انت شايف، استخدمنا title # كـ template reference عشان نوصل للعنصر الـ HTML نفسه.

وبعدين استخدمنا viewChild عشان نجيب العنصر اللي حطينا عليه الـ reference ده.

الـ viewChild بيرجع لنا "signal" بتحتوي على العنصر اللي جبناه، بس بيكون جوه ElementRef.

عشان نوصل للنتيجة اللي رجعته الـ query، كل اللي علينا إننا نتابع "الsignal" دي باستخدام أي API بيتعامل مع الإشارات زي ()effect أو ()computed.

<div dir="auto" align="left">

### What is the value returned by this signal?

</div>

لاحظ إن عشان نوصل للعنصر الـ HTML الفعلي، لازم نستخدم خاصية nativeElement من قيمة الـ signal.

ده لأن ElementRef هو مجرد غلاف حوالين عنصر الـ DOM الحقيقي، مش العنصر نفسه.

<div dir="auto" align="left">

### Why did we use a generic parameter ElementRef?

</div>

خد بالك كمان إننا استخدمنا الـ `<ElementRef>` في viewChild، عشان نحدد نوع القيم اللي الـ signal هترجعها.

لو ماعملناش كده، الـ signal هتتعامل على إنها بترجع قيم من نوع unknown، وده مش اللي احنا عايزينه.

وبكده تكون عرفت إزاي تعمل query لعناصر HTML العادية باستخدام `()viewChild` بكل بساطة!

<div dir="auto" align="left">

### What about AfterViewInit?

</div>

لاحظ إننا مش محتاجين نستخدم الـ `AfterViewInit lifecycle hook` التقليدي زي ما كنا بنعمل مع الـ `ViewChild decorator`.

بدل كده، استخدمنا `()effect` كـ `signal` بسيطة عشان نستقبل إشعار لما عنصر `title` يبقى جاهز.

وكمان ممكن نستخدم `()computed` عشان نستخرج قيم من الـ `title signal`.

الـ `title signal` هي مجرد signal للقراءة فقط (read-only)، فده بيخليها سهلة في التعامل وبتندمج بشكل سلس مع باقي الأدوات المبنية على signals في الـ framework.

ده معناه إننا بشكل عام مش هنحتاج نستخدم AfterViewInit تاني لما نشتغل باستخدام query signals بدل الـ decorator التقليدي.

<div dir="auto" align="left">

### What happens if the value of a template variable occurs more than once?

</div>
<div dir="auto" align="left">

```HTML
<div>
  <b #title>First Title</b>
  <b #title>Second Title</b>
</div>

<p #title>Paragraph Title</p>
```

</div>

في الحالة دي، `viewChild` هيختار أول عنصر موجود فيه `title#`، ومش هيظهر أي خطأ.

ده يعني إنه لما يكون في أكتر من عنصر ليهم نفس الـ `template reference` (زي `title#` هنا)، `viewChild` دايمًا هياخد أول واحد بس ويهمله الباقي.

<div dir="auto" align="left">

### viewChild() and Component Queries

</div>

بجانب عناصر HTML العادية، نقدر كمان نجيب الـ component instances باستخدام ميزة `viewChild`.

ممكن نعمل query للـ components إما باستخدام template references زي ما عملنا قبل كده، أو باستخدام كلاس الـ component نفسه.

خلينا نبدأ بعمل query للـ components باستخدام template references:

<div dir="auto" align="left">

```typescript
@Component({
  template: `
    <div>
      <book #book></book>
    </div>
  `,
})
class BookListComponent {
  bookComponent = viewChild<BookComponent>("book");
}
```

</div>

زي ما شايف، إحنا هنا بنستخدم <book/> component في الـ template، وحطينا ليه template reference باسم book.

لو مررنا الـ reference ده لـ viewChild، الـ query signal هترجع لنا الـ instance بتاع الـ BookComponent نفسه، مش عنصر الـ HTML المرتبط بيه.

✨ده معناه إننا نقدر نتعامل مع الـ component instance مباشرة، زي كده:

 <div dir="auto" align="left">

```typescript
this.bookComponent().title;
this.bookComponent().hello();
```

</div>

خد بالك من استخدام الـ generic parameter BookComponent . البراميتر ده مهم عشان يعرف viewChild نوع الـ component اللي متوقعه من الـ query دي.

وبكده تكون عرفت إزاي تستخدم viewChild عشان تجيب الـ component instances بشكل مباشر، بكل بساطة!

<div dir="auto" align="left">

### How does viewChild() work if the template changes?

</div>

الـ viewChild signal query بيعمل الـ query أول مرة لما الـ view بيتم تهيئته (initialize).

لو في أي وقت العنصر اللي جبناه اتحذف أو اتعمله إعادة عرض (re-rendered) أو اتحدّث في شجرة الكومبوننت، الـ signal query هتعيد الـ query عشان تحدث نفسها بالحالة الحالية للعنصر.

لو العنصر اتحذف، قيمة الـ signal query هتبقى undefined.

لكن لما العنصر يتخلق تاني، الـ signal query هترجع تجيب العنصر من الـ template view مرة تانية.

يعني زي ما شايف، الـ signal query بتحدّث نفسها تلقائيًا في كل مرة يحصل فيها تغيير في الـ detection run.

<div dir="auto" align="left">

### Setting "read" on viewChild()

</div>

الـ `viewChild` بتشتغل بشكل افتراضي إنها بترجع:

العنصر HTML عادي مغلف في `ElementRef` لو اللي بنسأل عنه هو عنصر HTML.
الكومبوننت نفسه لو العنصر ده هو كومبوننت.

لكن في بعض الحالات ممكن نحتاج نغير السلوك ده عشان نرجع حاجة معينة مرتبطة بالعنصر ده، سواء كانت الكومبوننت نفسه أو حاجات مرتبطة بيه.

مثال 1: الوصول للعنصر الـ HTML بدل الكومبوننت

لو إحنا عندنا كومبوننت اسمه `<book/>` في الـ template، ومش عايزين نوصل للكومبوننت نفسه، لكن عايزين نوصل للعنصر الـ HTML اللي بيحتويه.

<div dir="auto" align="left">

```typescript
@Component({
  template: `
    <div>
      <book #book></book>
    </div>
  `,
})
class BookListComponent {
  bookComponent = viewChild("book", {
    read: ElementRef,
  });
}
```

</div>

هنا استخدمنا read: ElementRef مع viewChild. ده بيقول لـ viewChild إنها ترجع ElementRef اللي بيحتوي على العنصر HTML نفسه، مش الـ BookComponent.

مثال 2: الوصول لDirective معينة مرتبطة بالعنصر

ممكن يكون عندنا Directive معينة مضافة للعنصر، زي matTooltip اللي بتضيف tooltip على العنصر.

<div dir="auto" align="left">

```typescript
@Component({
  template: `
    <div>
      <book #book matTooltip="I'm a tooltip!"> </book>
    </div>
  `,
  imports: [MatTooltip],
})
class BookListComponent {
  bookComponent = viewChild("book", {
    read: MatTooltip,
  });

  constructor() {
    effect(() => {
      console.log("Tooltip: ", this.bookComponent()?.message);
    });
  }
}
```

</div>

لو عايزين نوصل لحاجة معينة مرتبطة بالعنصر (زي الـ HTML element نفسه أو Directive معينة)، ممكن نحدد النوع اللي محتاجينه باستخدام read مع viewChild.

<div dir="auto" align="left">

### Making viewChild() to be required

</div>

بشكل افتراضي، `()viewChild` هترجع `undefined` لو العنصر اللي بنسأل عنه مش موجود في الـ template view.

لكن ممكن نخلي `()viewChild` تعمل query تكون "إجبارية"، بمعنى إنها لازم تلاقي حاجة تطابق الـ query في الـ template. لو مفيش حاجة تطابق، هيظهر خطأ.

<div dir="auto" align="left">

```HTML
<div>
  <b #title>Title</b>
</div>

```

</div>
<div dir="auto" align="left">

```typescript
titleRef = viewChild.required("bold");
```

</div>

في المثال ده، الـ query بتدور على عنصر بالـ reference bold، لكن مفيش عنصر بالـ reference ده، وبالتالي هيظهر الخطأ التالي:

`ERROR Error: NG0951: Child query result is required but no value is available`

</div>

<!-- ## What is Resource API?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

في Angular v19 حيكون فيه طريقة جديدة تقدر من خلالها تجيب بيانات من سيرفر، وتعرف إذا كانت العملية شغالة أو خلصت، وكمان تقدر تغير البيانات اللي عندك بشكل مباشر لما تحتاج. الطريقة دي بتسهل عليك متابعة الحالة، يعني لو البيانات لسه ما وصلتش، أو حصلت مشكلة، أو حتى لو وصلت وعايز تعدل عليها، كله حيكون واضح وأسهل في التعامل. الفكرة إنها بتنظم العملية كلها وتخليك تركز على شغلك من غير تعقيد.

🔴 الـ Resource API الجديدة في Angular فكرتها بسيطة جدًا. خلينا نبص على أبسط مثال لاستخدامها.

<div dir="auto" align="left">

```typescript
import { resource } from "@angular/core";

@Component({})
export class MyComponent {
  todoResource = resource({
    loader: () => {
      return Promise.resolve({ id: 1, title: "Hello World", completed: false });
    },
  });

  constructor() {
    effect(() => {
      console.log("Value: ", this.todoResource.value());
      console.log("Status: ", this.todoResource.status());
      console.log("Error: ", this.todoResource.error());
    });
  }
}
```

</div>

### 🔴 إيه اللي بيحصل هنا؟

إحنا بنستخدم `resource` عشان نجيب بيانات، وهنا بنستعمل Promise بسيط جدًا كـ مثال.

الـ `resource` بيرجع حاجة اسمها `WritableResource`. ده نوع بيساعدنا إننا نحدث البيانات لو احتجنا.

المميز في النوع ده إنه مش بس بيخلينا نقرأ البيانات (زي القيمة الحالية أو الحالة)، لكن كمان بنقدر نعدل عليها يدويًا لو احتجنا، من غير ما نستنى الـ loader يشتغل من جديد.

عشان نعرف القيمة اللي جت من الـ Resource

بنستخدم `()value` عشان نجيب البيانات الحالية.
بنستخدم `()status` عشان نعرف حالة البيانات (مثلاً: بتتحمل ولا خلصت).
بنستخدم `()error `لو حصلت مشكلة.

```
Value: undefined
Status: 'loading'
Error: undefined

Value: { id: 1, title: "Hello World", completed: false }
Status: 'resolved'
Error: undefined
```

### في الأول

الValue: undefined (لإن البيانات لسه ما وصلتش).
الStatus: 'loading' (معناها إن البيانات لسه في مرحلة التحميل).
الError: undefined (لإن مفيش أي مشاكل).

### بعد ما البيانات توصل

الValue: { id: 1, title: "Hello World", completed: false } (البيانات اللي رجعت).

الStatus: 'resolved' (معناها إن التحميل خلص).

الError: undefined (برضه مفيش مشاكل).

### Updating the data locally

توضيح فكرة تحديث البيانات محليًا

لما نتكلم عن تحديث البيانات محليًا باستخدام الـ `WritableResource`، إحنا بنقصد إننا نغير البيانات اللي عندنا من غير ما نعمل طلب جديد للسيرفر. دي طريقة ممتازة لو عايز الـ UI يتحدث بسرعة بناءً على تغييرات المستخدم، بدل ما تستنى رد من السيرفر.

<div dir="auto" align="left">

```typescript
import { resource } from "@angular/core";

@Component({
  template: ` <button (click)="updateTodo()">Update</button> `,
})
export class MyComponent {
  todoResource = resource({
    loader: () => {
      return Promise.resolve({ id: 1, title: "Hello World", completed: false });
    },
  });

  updateTodo() {
    this.todoResource.value.update((value) => {
      if (!value) return undefined;

      return { ...value, title: "updated" };
    });
  }
}
```

</div>
<div dir="auto" align="left">
We can update the data locally by using the update method of the value signal.

This will print the following:

```typescript
Value: { id: 1, title: "updated", completed: false }
Status: 'local'
Error: undefined
```

</div>

### ليه الstatus مهمة؟

الlocal: بتوضح إن التعديل ده حصل محليًا.

ده بيساعدك لو عايز تفرق بين البيانات اللي جت من السيرفر وبين اللي تم تعديلها يدويًا.

### Loading the data

تحميل البيانات من السيرفر

دلوقتي هنشوف إزاي نستخدم الـ `resource` عشان نجيب بيانات من السيرفر باستخدام API حقيقي زي JSONPlaceholder.

<div dir="auto" align="left">

```typescript
interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

@Component()
export class MyComponent {
  todosResource = resource({
    loader: () => {
      return fetch(`https://jsonplaceholder.typicode.com/todos?_limit=10`).then(
        (res) => res.json() as Promise<Todo[]>
      );
    },
  });
}
```

</div>

### شرح الكود

تعريف واجهة (Interface)

عرّفنا الـ Todo عشان نحدد شكل البيانات اللي راجعة (id, title, completed).

### إنشاء resource

استخدمنا loader لكتابة دالة بتحمل البيانات من السيرفر باستخدام fetch.
الطلب بيسحب 10 عناصر من قائمة todos.

### بداية العمل

أول ما يتم إنشاء todosResource، بيبدأ الطلب على طول.
أثناء ما الطلب شغال، القيمة (value) بتكون undefined، والحالة (status) بتكون 'loading'.

### لما الطلب يخلص

القيمة (value) هتتحول للبيانات اللي جت من السيرفر.
الحالة (status) هتكون 'resolved'.

### ✨ النتيجة

أثناء التحميل

<div dir="auto" align="left">

```typescript
Value: undefined;
Status: "loading";
Error: undefined;
```

</div>

بعد انتهاء التحميل

<div dir="auto" align="left">

```typescript
Value: [
  { id: 1, title: "Hello World", completed: false },
  { id: 2, title: "Hello World", completed: false },
  ...
]
Status: 'resolved'
Error: undefined
```

</div>

### ملاحظات:

الحالة (status)

ال'loading': الطلب شغال.

ال'resolved': البيانات وصلت بنجاح.

ال'error': لو حصلت مشكلة أثناء التحميل.

### مرونة الـ resource:

بمجرد ما البيانات توصل، تقدر تعرضها مباشرة في الـ UI.
لو حصلت مشكلة، الـ error هتوضح لك السبب.

### Refreshing the data

في بعض الأحيان، ممكن تحتاج تعيد تحميل البيانات (refresh) بناءً على تفاعل المستخدم، زي لما يضغط على زرار.

<div dir="auto" align="left">

```typescript
import { resource } from "@angular/core";

@Component({
  template: ` <button (click)="refresh()">Refresh</button> `,
})
export class MyComponent {
  todosResource = resource({
    loader: () => {
      return fetch(`https://jsonplaceholder.typicode.com/todos?_limit=10`).then(
        (res) => res.json() as Promise<Todo[]>
      );
    },
  });

  refresh() {
    this.todosResource.refresh();
  }
}
```

</div>

الميثود `()refresh` اللي موجودة في الـ resource بتشتغل على إعادة تشغيل الـ loader مرة تانية لتحميل البيانات من جديد.

### ملاحظة مهمة

لو استدعيت `()refresh` أكتر من مرة في نفس الوقت

مش هيبدأ طلب جديد إلا بعد انتهاء الطلب الحالي.

ده معناه إن الطلبات مش هتتكرر أو تتداخل، وده نفس السلوك اللي بنشوفه مع exhaustMap في RxJS.

### Loading specific date based on other signals

تحميل البيانات بناءً على Signals

لما نحتاج نحمل بيانات بناءً على Signal زي todoId، الميثود loader لوحدها مش بتتتبع تغييرات الـ Signal بشكل تلقائي. يعني لو todoId اتغيرت، الـ load مش هيتم استدعاؤه مرة تانية تلقائيًا.

<div dir="auto" align="left">

```typescript
import { resource } from "@angular/core";

@Component()
export class MyComponent {
  todoId = signal(1); // Signal لتحديد ID المطلوب

  todoResource = resource({
    loader: () => {
      return fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId()}`
      ).then((res) => res.json() as Promise<Todo>);
    },
  });
}
```

This will work fine, but one this to notice is that `loader` is `untracked` and that means, that if the todoId signal changes, the load won't be called again. Let's make it more reactive!

</div>

### ❌المشكلة

رغم إن todoId عبارة عن Signal، الـ loader هنا مش بيتتبع التغييرات اللي بتحصل في todoId.
لو غيرت قيمة todoId، البيانات مش هتتحدث تلقائيًا.

### Separate the request and the loader

عند الحاجة إلى جعل البيانات تتحدث تلقائيًا عند تغيير Signal مثل `todoId`، يمكننا استخدام خاصية `request` داخل الـ `resource`. الـ `request` تتيح تمرير Signal أو مجموعة من Signals ليتم تتبعها تلقائيًا.

<div dir="auto" align="left">

```typescript
todoResource = resource({
  request: this.todoId,
  loader: ({ request: todoId }) => {
    return fetch(`https://jsonplaceholder.typicode.com/todos/${todoId}`).then(
      (res) => res.json() as Promise<Todo>
    );
  },
});
```

</div>

تم تمرير this.todoId كـ Signal.

لما تتغير قيمة todoId، الـ loader يتم استدعاؤه تلقائيًا لتحميل البيانات الجديدة.

الloader يستقبل القيمة الحالية لـ todoId عبر الخاصية request.
يقوم بعمل طلب البيانات بناءً على هذه القيمة.

### التعامل مع الطلبات غير المكتملة (Unfinished Requests)

إذا تغيرت قيمة todoId أثناء وجود طلب سابق قيد التنفيذ، يمكن إلغاء الطلب القديم باستخدام خاصية `abortSignal`.

<div dir="auto" align="left">

```typescript
todoResource = resource({
  request: this.todoId,
  loader: ({ request: todoId, abortSignal }) => {
    return fetch(`https://jsonplaceholder.typicode.com/todos/${todoId}`, {
      signal: abortSignal,
    }).then((res) => res.json() as Promise<Todo>);
  },
});
```

</div>

### استخدام طلب يعتمد على إشارات متعددة (Multiple Signals)

<div dir="auto" align="left">

```typescript
limit = signal(10);
query = signal("");

todosResource = resource({
  request: () => ({ limit: this.limit(), query: this.query() }),
  loader: ({ request, abortSignal }) => {
    const { limit, query } = request as { limit: number; query: string };
    return fetch(
      `https://jsonplaceholder.typicode.com/todos?_limit=${limit}&query=${query}`,
      { signal: abortSignal }
    ).then((res) => res.json() as Promise<Todo[]>);
  },
});
```

</div>

### فايدة الـ abortSignal
الـ abortSignal بتستخدم لإلغاء الطلبات اللي لسه شغالة (Unfinished Requests) لما يحصل تغيير يستدعي طلب جديد. وده بيحسن الأداء ويمنع التداخل بين الطلبات.

### الموقف اللي محتاج فيه abortSignal

لو المستخدم غيّر القيم بسرعة:

مثلاً: المستخدم زوّد limit من 10 لـ 20 لـ 30 في وقت قليل.
كل قيمة جديدة بتحتاج طلب جديد للبيانات.

بدون abortSignal: الطلبات القديمة هتكمل لحد ما تخلص، وده هيستهلك موارد السيرفر

مع abortSignal: الطلب القديم يتلغي أول ما يبدأ طلب جديد.
لو حصل تغيير في أكثر من Signal مع بعض:

زي تغيير limit وquery في نفس الوقت.
abortSignal يضمن إن الطلبات القديمة تُلغى بسرعة.

### What happens when we have a request in progress and update data locally?
عندك طلب بيانات شغال (جاري تحميل البيانات من السيرفر).

في نفس الوقت، قررت إنك تعدّل البيانات محليًا (من غير ما تستنى الرد من السيرفر).

#### اللي بيحصل:
البيانات المحلية تتحدث فورًا:

أول ما تعدّل البيانات، Angular Resource API بتقوم بتحديث البيانات اللي عندك مباشرة في الواجهة (Local Update).

يعني المستخدم هيشوف التحديث الجديد بدون انتظار.

إلغاء الطلب الجاري:

الطلب اللي كان شغال من السيرفر (request in progress) يتم إلغاؤه تلقائيًا.
السبب: البيانات اللي كان هيجيبها الطلب مبقتش لازمة لأنك بالفعل عدّلتها محليًا.

### Create more reusable resources

عن طريق فصل القيم التفاعلية (reactive values) عن الـ loader
ممكن ننقل loader logic إلى function مستقلة ونستخدمها في أماكن مختلفة بسهولة.

الكود قبل التعديل:

<div dir="auto" align="left">

```typescript
todoResource = resource({
    request: this.todoId,
    loader: ({ request: todoId, abortSignal }) => {
        return fetch(
          `https://jsonplaceholder.typicode.com/todos/${todoId}`,
          { signal: abortSignal }
        ).then((res) => res.json() as Promise<Todo>);
    },
});
```

</div>

الكود بعد التعديل:
<div dir="auto" align="left">

```typescript
import { ResourceLoaderParams } from "@angular/core";

function todoLoader({ request: todoId, abortSignal }: ResourceLoaderParams<number>): Promise<Todo> {
    return fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId}`,
      { signal: abortSignal }
    ).then((res) => res.json() as Promise<Todo>);
}

todoResource = resource({ request: this.todoId, loader: todoLoader });
```

</div>

الـ function دي بتنقل loader logic الخارجي بعيدًا عن الـ resource.

بتعتمد على النوع ResourceLoaderParams عشان تحصل على المعلومات اللي محتاجة زي request و abortSignal.

### RxResource -> The Observable based resource API

في Angular، الاعتماد على Observables لعمليات تحميل البيانات هو أمر شائع. باستخدام rxResource، يمكننا استخدام Observables بدلاً من Signals وPromises لتحميل البيانات بشكل أكثر تفاعلية ومرونة.

<div dir="auto" align="left">

```typescript
import { rxResource } from "@angular/core/rxjs-interop";

@Component()
export class MyComponent {
  limit = signal(10);

  todosResource = rxResource({
    request: this.limit,
    loader: (limit) => {
      return this.http.get<Todo[]>(
        `https://jsonplaceholder.typicode.com/todos?_limit=${limit}`
      );
    },
  });
}
```

</div>


</div> -->

<!-- <div dir="auto" align="left">

```typescript

```

</div>
<div dir="auto" align="left">

```HTML

```

</div> -->
