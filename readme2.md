<!-- ## Uses of Angular Route Guards
[⬆️ Back to Top](#top7)

<div dir="auto" align="right">

#### To Confirm the navigational operation

لو عايز تسأل المستخدم "عايز تحفظ التعديلات قبل ما تسيب الصفحة؟

#### Allow access to certain parts of the application to specific users.

و عايز تتحكم مين يدخل على أجزاء معينة في التطبيق (زي صفحات الأدمن مثلاً)

#### Validating the route parameters before navigating to the route

لو محتاج تتأكد من باراميتر معين (زي ID بتاع المستخدم مثلاً) قبل ما تروح لصفحة معينة

#### Fetching some data before you display the component.

لو عندك بيانات محتاج تجيبها من السيرفر قبل ما تعرض الكومبوننت،

</div>

## Types of Route Guards

[⬆️ Back to Top](#top7)

### The Angular Router supports fifth different guards, which you can use to protect the route.

1- CanActivate
2- CanDeactivate
3- Resolve
4- CanLoad
5- CanActivateChild

## What is CanActivate Guard

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
الCanActivate Guard ده زي حارس بيمنع أو بيسمح للـ Route إنها تتفتح أو تتعرض للمستخدم بناءً على شرط معين. بنستخدمه لما نكون عايزين نتاكد من حاجة معينة قبل ما نخلي المستخدم يشوف الصفحة. يعني ممكن نقول للـ Guard ده “لو الشرط الفلاني موجود، اسمح للمستخدم يدخل”، ولو الشرط مش موجود، “امنع المستخدم”.

### أمتى بنستخدم CanActivate Guard؟

فيه أكتر من حالة ممكن تحتاج فيها CanActivate Guard

لو المستخدم مسجّل دخول: بنستخدمه عشان نتأكد إن المستخدم عامل تسجيل دخول في النظام. لو مش عامل تسجيل، نرجعه لصفحة تسجيل الدخول.

لو المستخدم ليه الصلاحية: بنشوف لو المستخدم عنده الصلاحية يدخل على صفحة معينة (زي صفحة الأدمن).

### إزاي نستخدم CanActivate Guard؟

عشان نستخدم CanActivate Guard، بنعمل Service في Angular.

### خطوات تنفيذه

إنشاء Service: بنعمل Service جديد في التطبيق يكون مسؤول عن الحماية دي.

ب Import CanActivate Interface: في الـ Service، بنستورد CanActivate Interface من @angular/router، ودي بتخلينا نحدد طريقة اسمها canActivate.

تنفيذ canActivate Method: الطريقة دي بتتأكد لو الشرط اتحقق وترجع true لو ممكن نكمل وندخل، أو false لو مش هينفع نكمل. كمان ممكن ترجع UrlTree (دي زي لينك) عشان تحول المستخدم على صفحة تانية لو الشرط مش موجود.

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import {
  Router,
  CanActivate,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
} from "@angular/router";

@Injectable()
export class AuthGuardService implements CanActivate {
  constructor(private _router: Router) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): boolean {
    //check some condition
    if (someCondition) {
      alert("You are not allowed to view this page");
      //redirect to login/home page etc
      //return false to cancel the navigation
      return false;
    }
    return true;
  }
}
```

Update the route definition with the canActivate guard as shown below. You can apply more than one guard to a route and a route can have more than one guard

</div>

<div dir="auto" align="left">

```typescript
{ path: 'product', component: ProductComponent, canActivate : [AuthGuardService] },
```

</div>

</div>

## What is CanActivateChild Guard

[⬆️ Back to Top](#top7)

<div dir="auto" align="right">

### يعني إيه CanActivateChild Guard؟

الCanActivateChild Guard ده زي CanActivate Guard، بس الفرق إنه بيتطبق على الأب اللي جواه Routes الفكرة هنا إنك لما تحط CanActivateChild Guard على أي Route أب، كل ما المستخدم يحاول يدخل على واحدة من الصفحات الفرعية (الـ Children)، الـ Guard ده بيشتغل ويتأكد لو مسموح له يدخل ولا لأ.

### الفرق بين CanActivate و CanActivateChild

الCanActivate: بتحطه على أي Route (سواء Route عادي أو Parent) وبيتحكم في دخول المستخدم للـ Route دي كلها.

الCanActivateChild: بتحطه على الـ Parent Route وبيشتغل على كل الـ Child Routes اللي جواه. يعني بدل ما تحط Guard على كل Route فرعية، ممكن تحط CanActivateChild مرة واحدة على الـ Parent وهو هيعمل الحماية المطلوبة لكل اللي جواه.

### مثال لتوضيح الفرق

لو عندك مثلاً صفحة Products (اللي هي الـ Parent)، وعندك جواها كذا Route فرعي (زي عرض منتج معين، تعديل منتج، إضافة منتج)

باستخدام CanActivate، لو حطيت Guard على Products، ده هيمنع الدخول على الـ Parent والـ Children كلها في حالة إن المستخدم مش عامل تسجيل دخول.

باستخدام CanActivateChild، ممكن تسمح لكل الناس تشوف صفحة Products، بس تمنع الدخول للـ Routes الفرعية (زي التعديل والإضافة) وتخليها بس للأدمن.

### إزاي نستخدم CanActivateChild Guard؟

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import {
  Router,
  CanActivateChild,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
} from "@angular/router";

@Injectable()
export class AdminGuardService implements CanActivateChild {
  constructor(private _router: Router) {}

  canActivateChild(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): boolean {
    // بنفترض إن في شرط معين زي إن المستخدم يكون أدمن
    const isAdmin = false; // حط الشرط المناسب هنا
    if (!isAdmin) {
      alert("مش مسموح ليك تدخل هنا!");
      this._router.navigate(["/login"]); // يرجع المستخدم لصفحة تانية لو مش أدمن
      return false;
    }
    return true;
  }
}
```

</div>
<div dir="auto" align="left">

```typescript
{ path: 'product', component: ProductComponent, canActivate : [AuthGuardService] ,
      canActivateChild : [AuthGuardService],
      children: [
      {  path: 'view/:id', component: ProductViewComponent  },
      {  path: 'edit/:id', component: ProductEditComponent  },
      {  path: 'add', component: ProductAddComponent }
      ]
  }
```

</div>

### 🔴 ملخص سريع

CanActivate: يمنع أو يسمح بالوصول للـ Route ككل (الـ Parent والـ Children).

CanActivateChild: بيتحط على الـ Parent وبيشتغل على كل Child جواه، وبيمنع الوصول للـ Routes الفرعية بناءً على الشرط.

</div>

## What is CanDeactivate Guard

[⬆️ Back to Top](#top7)

<div dir="auto" align="right">

### يعني إيه CanDeactivate Guard؟

الCanDeactivate Guard ده بيشتغل لما المستخدم يحاول يسيب الصفحة أو الـ Component الحالية وعايز يروح لصفحة تانية.

الهدف الأساسي منه إنه يمنع المستخدم من الخروج لو عنده بيانات لسه متسجلتش، زي لما يكون كاتب بيانات في فورم بس لسه ما حفظهاش.

### أفضل حالة نستخدم فيها CanDeactivate Guard

مثلاً في حالات زي ملء بيانات في فورم: لو المستخدم كتب بيانات بس لسه ما ضغطش على "حفظ" وحاول يسيب الصفحة، CanDeactivate Guard يقدر يوقفه ويسأله "هل انت متأكد إنك عايز تخرج من غير ما تحفظ؟". لو وافق، ينقله للصفحة الجديدة، ولو رفض، يخليه يكمل في نفس الصفحة.

### إزاي نستخدم CanDeactivate Guard؟

عشان تفعّل CanDeactivate Guard، محتاج تعمل Service خاصة بيه.

خطوات التنفيذ:
إنشاء Service: بنعمل Service جديد، والـ Service ده بيستورد CanDeactivate Interface من angular/router@

تنفيذ canDeactivate Method: الطريقة canDeactivate بتاخد الكومبوننت الحالي كـ argument، وبتاخد كمان معلومات عن الـ Route الحالي والـ Route اللي المستخدم رايحله. بناءً على الشرط اللي تحدده، بتحدد لو ممكن نسيب الصفحة أو لأ.

### مثال عملي

أول حاجة، بنعمل الكومبوننت اللي عايزين نحميه، وليكن اسمه RegisterComponent. جواه بنعمل طريقة اسمها canExit، والطريقة دي بتتحقق لو فيه بيانات غير محفوظة وتسأل المستخدم لو عايز يخرج أو يكمل.

<div dir="auto" align="left">

```typescript
import { Component } from "@angular/core";

@Component({
  templateUrl: "register.component.html",
})
export class RegisterComponent {
  // الطريقة دي بتتحقق لو فيه بيانات غير محفوظة وتسأل المستخدم
  canExit(): boolean {
    if (confirm("هل تريد فعلاً الخروج بدون حفظ التعديلات؟")) {
      return true; // يسمح بالخروج
    } else {
      return false; // يخلّي المستخدم في الصفحة
    }
  }
}
```

</div>
تفعيل الـ CanDeactivate Guard في Service
بنعمل Service عشان يتحقق من canExit لما المستخدم يحاول يسيب الصفحة.
<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import { CanDeactivate } from "@angular/router";
import { RegisterComponent } from "./register.component";

@Injectable({
  providedIn: "root",
})
export class CanDeactivateGuardService
  implements CanDeactivate<RegisterComponent>
{
  canDeactivate(component: RegisterComponent): boolean {
    return component.canExit(); // بيشغل canExit وبيتأكد لو المستخدم عايز يسيب الصفحة فعلاً
  }
}
```

</div>

### استخدام الـ Guard في الـ Routing

في ملف الـ Routing، بنضيف الـ Guard ده على الصفحة اللي عايزين نحميها، مثلاً على RegisterComponent

<div dir="auto" align="left">

```typescript
{ path: 'register', component: RegisterComponent, canDeactivate: [CanDeactivateGuardService] }
```

</div>

### 🔴 ملخص سريع

الCanDeactivate Guard بيمنع الخروج من الصفحة لو فيه بيانات غير محفوظة.

بيسأل المستخدم لو عايز يخرج بدون حفظ، ولو وافق، يكمل، ولو رفض، يفضل في نفس الصفحة.

بيساعدك تحمي بيانات المستخدم لو كان لسه ما حفظهاش قبل ما يخرج.

</div>

## How to Use Resolve Guard

[⬆️ Back to Top](#top7)

<div dir="auto" align="right">

### يعني إيه Resolve Guard؟

الResolve Guard في Angular بيعمل حاجة مهمة جداً وهي إنه يحمل البيانات من السيرفر قبل ما الصفحة تفتح أصلاً. بدل ما الكومبوننت يظهر فاضي وبعدين يستنى لحد ما البيانات توصله، Resolve Guard بيحمل البيانات الأول وبعدين يفتح الكومبوننت على طول والبيانات جاهزة.

### المشكلة اللي بيحلها Resolve Guard

عادةً في الكومبوننت العادية، لما بنستخدم ngOnInit لجلب البيانات، المستخدم ممكن يشوف صفحة فاضية لحد ما البيانات توصله. في الحالة دي، ممكن نستخدم loading spinner عشان نبين إن فيه حاجة بتحصل. لكن Resolve Guard بيخلّي البيانات موجودة من قبل ما الصفحة تفتح، فبيحسن التجربة ويخلي الصفحة تظهر كاملة للمستخدم.

### إزاي نستخدم Resolve Guard؟

إنشاء Service: بنعمل Service جديدة بتحمل البيانات المطلوبة. الـ Service دي هتطبق Resolve Interface

تنفيذ resolve method: جوه الـ Service، هنضيف method اسمها resolve بتجيب البيانات المطلوبة وترجعها. لازم ترجع Observable أو Promise عشان Angular تستنى البيانات دي قبل ما تفتح الكومبوننت.

### مثال عملي على الكود

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import {
  Resolve,
  ActivatedRouteSnapshot,
  RouterStateSnapshot,
} from "@angular/router";
import { ProductService } from "./product.service";
import { Observable } from "rxjs";

@Injectable({
  providedIn: "root",
})
export class ProductListResolveService implements Resolve<any> {
  constructor(private productService: ProductService) {}

  resolve(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<any> {
    return this.productService.getProducts();
  }
}
```

</div>

### إضافة الـ Resolve للـ Routing

عشان تفعّل الـ Resolve Guard ده، لازم تضيفه على Route بتاع الصفحة اللي عايز تفتحها بالبيانات الجاهزة.

<div dir="auto" align="left">

```typescript
{ path: 'product', component: ProductComponent, resolve: { products: ProductListResolveService } },
```

</div>
في الكود ده

الproducts هو اسم المتغير اللي هنستخدمه في الكومبوننت عشان نجيب البيانات.
ProductListResolveService هو الـ Service اللي جبنا منه البيانات.

### استخدام البيانات في الكومبوننت

جوه الكومبوننت، هنجيب البيانات الجاهزة من ActivatedRoute بدل ما نعمل طلب جديد.

<div dir="auto" align="left">

```typescript
import { Component, OnInit } from "@angular/core";
import { ActivatedRoute } from "@angular/router";

@Component({
  selector: "app-product",
  templateUrl: "./product.component.html",
})
export class ProductComponent implements OnInit {
  products: any;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    this.products = this.route.snapshot.data["products"]; // هنا بنجيب البيانات
  }
}
```

</div>

### ملاحظات إضافية

🔴 أولوية التنفيذ: Resolve Guard بيتنفذ بعد كل الـ Guards التانية.

🔴 إلغاء التنقل: لو الـ Resolver رجّع null أو حصل خطأ، Angular بتلغي التنقل ومش هتروح للـ Route.

🔴 استخدام أكتر من Resolver: تقدر تحط أكتر من Resolve على نفس الـ Route، يعني تقدر تجيب بيانات من مصادر مختلفة في نفس الوقت.

<div dir="auto" align="left">

```typescript
{ path: 'product', component: ProductComponent,
    resolve: {products: ProductListResolveService, , data:SomeOtherResolverService}  }
```

</div>
</div>

## How to use CanLoad Guard

[⬆️ Back to Top](#top7)

<div dir="auto" align="right">

### يعني إيه CanLoad Guard؟

الCanLoad Guard ده بيمنع تحميل الـ Lazy Loaded Modules لو المستخدم مالوش صلاحية.

بمعنى تاني، لو عندك Module مش عايز مستخدم معين يشوفه (زي صفحة الـ Admin)، الـ CanLoad بيمنع تحميل الـ Module ده بالكامل عشان المستخدم لا يقدر يشوف الصفحة ولا حتى يشوف كود الصفحة من المتصفح.

### الفرق بين CanActivate و CanLoad

الCanActivate: بيمنع المستخدم من الدخول للصفحة، لكن ما بيمنعش تحميل كود الصفحة، يعني ممكن المستخدم يشوف الكود من الـ Developer Tools.

الCanLoad: بيمنع تحميل كود الصفحة بالكامل. المستخدم مش هيشوف الكود ولا هيقدر يدخل على الصفحة.

### إزاي نستخدم CanLoad Guard؟

إنشاء Service جديدة: بنعمل Service بتطبق CanLoad Interface عشان نحدد الشروط اللي تمنع أو تسمح بالتحميل.

تنفيذ canLoad method: الطريقة دي بتتحقق من الـ Route اللي المستخدم عايز يدخل عليها، ولو الشروط متحققة بترجع true عشان يتم التحميل، أو false عشان تمنع التحميل.

#### مثال عملي

نبدأ بإنشاء Service جديدة، وليكن اسمها AuthGuardService، ونضيف فيها الشروط.

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import { CanLoad, Route, Router } from "@angular/router";

@Injectable()
export class AuthGuardService implements CanLoad {
  constructor(private router: Router) {}

  canLoad(route: Route): boolean {
    let url: string = route.path;
    console.log("Url:" + url);

    if (url === "admin") {
      // لو المستخدم حاول يدخل صفحة الأدمن
      alert("غير مسموح ليك تدخل الصفحة دي");
      return false; // تمنع تحميل الـ Module
    }
    return true; // تسمح بالتحميل للصفحات التانية
  }
}
```

</div>

### إضافة الـ CanLoad للـ Route

عشان تربط الـ Guard ده بالـ Routes، بتحط AuthGuardService في خاصية canLoad للـ Route اللي عايز تحميها.

<div dir="auto" align="left">

```typescript
const routes: Routes = [
  {
    path: "admin",
    loadChildren: "./admin/admin.module#AdminModule",
    canLoad: [AuthGuardService],
  },
  {
    path: "test",
    loadChildren: "./test/test.module#TestModule",
    canLoad: [AuthGuardService],
  },
];
```

</div>
تسجيل الـ Service في الـ AppModule
في الآخر، بنضيف الـ AuthGuardService في ملف AppModule كـ provider عشان Angular يقدر يستخدمه.

<div dir="auto" align="left">

```typescript
import { BrowserModule } from "@angular/platform-browser";
import { NgModule } from "@angular/core";
import { AppRoutingModule } from "./app-routing.module";
import { AppComponent } from "./app.component";
import { AuthGuardService } from "./auth-gaurd.service";

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, AppRoutingModule],
  providers: [AuthGuardService],
  bootstrap: [AppComponent],
})
export class AppModule {}
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
