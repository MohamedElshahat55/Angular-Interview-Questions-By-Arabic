## What is angular Http interceptor

[⬆️ Back to Top](#top8)

<div dir="auto" align="right">

### يعني إيه Angular HTTP Interceptor؟

الHTTP Interceptor في Angular ده بيشتغل كوسيط ما بين التطبيق بتاعنا والسيرفر.

لما التطبيق يبعت طلب للسيرفر (زي GET أو POST)، الـ Interceptor بيقدر يمسك الطلب ده قبل ما يتبعت ويقدر يعدل عليه.

كمان لما السيرفر يرد علينا، الـ Interceptor يقدر يمسك الرد ويعدّل فيه لو محتاج.

### فوايد HTTP Interceptor

واحدة من أهم الفوايد هي إنك تقدر تضيف Authorization Header (زي توكن بتاع تسجيل الدخول) على كل طلب.

يعني بدل ما تحط التوكن بشكل يدوي في كل مكان، الـ Interceptor بيضيفه تلقائي لكل طلب، وده بيوفر مجهود ويقلل الأخطاء.

كمان تقدر تستخدمه عشان تمسك الأخطاء اللي بترجع من السيرفر، زي لو في مشكلة في الاتصال أو السيرفر رد بحاجة غلط. ممكن تخليه يسجل الأخطاء دي في اللوج أو يعرض للمستخدم رسالة.

### مثال على الاستخدامات

إضافة Headers: تقدر تضيف Headers مخصصة (زي Authorization) لكل طلب خارج.

التعامل مع الأخطاء: تقدر تمسك الأخطاء اللي بترجع من السيرفر وتتعامل معاها قبل ما توصل للتطبيق.

### إزاي نعمل Http Interceptor؟

إنشاء Service جديدة: الأول بنعمل Service جديدة، ودي لازم تطبّق HttpInterceptor Interface من Angular.

<div dir="auto" align="left">

```typescript
import { Injectable } from "@angular/core";
import {
  HttpInterceptor,
  HttpRequest,
  HttpHandler,
  HttpEvent,
} from "@angular/common/http";
import { Observable } from "rxjs";

@Injectable()
export class AppHttpInterceptor implements HttpInterceptor {
  intercept(
    req: HttpRequest<any>,
    next: HttpHandler
  ): Observable<HttpEvent<any>> {
    // هنا تقدر تعمل أي تعديل على الطلب
    console.log("Interceptor شغال!");

    // بترجع الطلب عشان يكمل ويعمله send
    return next.handle(req);
  }
}
```

</div>

الintercept هي الطريقة الأساسية اللي بتشتغل على كل طلب. بتاخد req اللي هو الطلب
الحالي وnext اللي هو المسؤول عن تمرير الطلب للخطوة اللي بعدها.

الnext.handle(req) بيكمل إرسال الطلب بعد التعديلات اللي انت عملتها.
تسجيل الـ Interceptor في الـ Root Module: عشان Angular تستخدم الـ Interceptor، لازم تضيفه في providers في AppModule وتستخدم الـ HTTP_INTERCEPTORS عشان تسجله كـ Multi Provider.

<div dir="auto" align="left">

```typescript
import { HTTP_INTERCEPTORS } from "@angular/common/http";

@NgModule({
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AppHttpInterceptor,
      multi: true,
    },
  ],
})
export class AppModule {}
```

</div>

هنا بنضيف AppHttpInterceptor كـ provider في التطبيق، وmulti: true معناها إنه يقدر يستخدم أكتر من Interceptor في نفس الوقت لو عندك أكتر من واحد.

### Setting the new headers

#### ايه هي الفكرة الأساسية؟

لما بنبعت طلب HTTP من Angular للسيرفر (زي لما نجيب بيانات أو نبعت بيانات)، الطلب ده بيتبعت ومعاه Headers (زي بطاقة تعريف بتحط شوية معلومات عن الطلب، زي نوع البيانات اللي بنبعتها أو إن كان المستخدم مسجّل دخول).

فيه حالات بنحتاج نضيف أو نعدل أو حتى نحذف Headers قبل ما الطلب يتبعت للسيرفر.

هنا بنستخدم حاجة اسمها HTTP Interceptor، ودي بتخلينا "نعترض" الطلب ونعدل عليه قبل ما يتبعت.

 <div dir="auto" align="left">

```typescript
req = req.clone({
  headers: req.headers.set("Content-Type", "application/json"),
});
```

</div>

### ليه بنستخدم clone؟

في Angular، الطلبات (requests) والأجزاء بتاعتها زي الـ Headers بتكون ثابتة (Immutable)، يعني ماينفعش نعدل عليها مباشرةً. علشان كده، لما نحتاج نغير حاجة في الطلب، لازم نعمل نسخة (Clone) منه.

### ليه بنضيف Content-Type؟

لما نبعت بيانات للسيرفر، بنحط نوع البيانات اللي بنبعتها في الهيدر Content-Type. مثلاً لو البيانات بصيغة JSON، بنضيف الهيدر بالشكل ده

هنا set بتعمل نسخة جديدة من الهيدر وبتضيف Content-Type لو مش موجود أو بتعدله لو كان موجود.

### طيب لو عايز تضيف الهيدر بدون ما تغير الموجود؟

ممكن تستخدم append بدل set، ودي بتضيف Header جديد حتى لو كان نفس الهيدر موجود قبل كده:

<div dir="auto" align="left">

```typescript
req = req.clone({
  headers: req.headers.append("Content-Type", "application/json"),
});
```

</div>

### تأكد لو Header موجود قبل ما تضيفه

لو مش عايز تضيف نفس Header مرتين، ممكن تتأكد قبل بإستخدام:

<div dir="auto" align="left">

```typescript
if (!req.headers.has("Content-Type")) {
  req = req.clone({
    headers: req.headers.set("Content-Type", "application/json"),
  });
}
```

</div>

### إضافة Authorization Token

#### 🔴 ايه هو الـ Token؟

الـ Token هو زي كود سري بيستخدمه المستخدم لما يكون عامل تسجيل دخول.

بنضيفه في الهيدر Authorization عشان نقول للسيرفر "المستخدم ده معاه صلاحيات".

### إزاي تضيف التوكن للطلب؟

بنستخدم طريقة زي دي، نفترض إن التوكن متخزن في Service بتاعتك:

<div dir="auto" align="left">

```typescript
const token: string = authService.Token; // بنجيب التوكن من الـ Service
if (token) {
  req = req.clone({
    headers: req.headers.set("Authorization", "Bearer " + token),
  });
}
```

</div>

في الكود ده بنضيف "Bearer" قبل التوكن، وده أسلوب متعارف عليه في الـ Authorization Headers.

### Intercepting the Response

لما نبعت طلب للسيرفر، بنستنى رد (Response) يوصلنا.

الـ Interceptor بيخلينا "نعترض" الرد ده، نعدله أو نسجل أي حاجة محتاجينها قبل ما يوصل للتطبيق نفسه.

في الحالة دي، بنستخدم RxJS Operators زي map, tap catchError, و retry عشان نتحكم أكتر في الرد.

### تسجيل requests باستخدام tap

#### ليه بنستخدم tap؟

الtap بيخلينا نقدر نسجل أحداث معينة، زي الوقت اللي أخده الطلب عشان يخلص.

دي طريقة كويسة لو عايز تعرف الوقت اللي الطلب استغرقه، أو تسجل أي معلومات إضافية عن الطلب أو الرد.

### مثال عملي

في الكود ده، tap بيتنفذ مرتين: مرة لما الطلب يبعت، ومرة تانية لما الرد يوصل.

<div dir="auto" align="left">

```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  req = req.clone({ headers: req.headers.append('Content-Type', 'application/json') });
  const started = Date.now();

  return next.handle(req).pipe(
    tap(event => {
      const elapsed = Date.now() - started;
      console.log(`Request for ${req.urlWithParams} took ${elapsed} ms.`);
      if (event instanceof HttpResponse) {
        console.log('Response Received');
      }
    })
  );
}
```

</div>

✨الكود ده بيحسب الزمن اللي أخده الطلب عشان يوصل الرد، وبيسجل رسالة لما الاستجابة توصل.

### تعديل الرد باستخدام map

#### ليه بنستخدم map؟

الmap بنستخدمه عشان نعدل محتوى الرد قبل ما يوصل للتطبيق. لو فيه بيانات محتاجين نغيرها أو نبدّلها، بنقدر نستخدم map عشان نعمل ده.

#### مثال عملي

في المثال ده، بنستخدم map عشان نغير محتوى الرد بالكامل، ونحط بيانات جديدة في (body) بتاع الرد:

<div dir="auto" align="left">

```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  return next.handle(req).pipe(
    map(resp => {
      const myBody = [{ 'id': '1', 'name': 'TekTutorialsHub', 'html_url': 'www.tektutorialshub.com', 'description': 'description' }];
      if (resp instanceof HttpResponse) {
        resp = resp.clone<any>({ body: myBody });
        return resp;
      }
      return resp;
    })
  );
}
```

</div>

### التعامل مع الأخطاء باستخدام catchError

#### ليه بنستخدم catchError؟

الcatchError بنستخدمه عشان نمسك أي خطأ حصل أثناء الطلب ونتعامل معاه، زي مثلاً لو الطلب رجّع 401 Unauthorized، نعرف نوجّه المستخدم لصفحة تسجيل الدخول.

#### مثال عملي

في الكود ده، catchError بيمسك الأخطاء ويعرض التفاصيل الخاصة بيها، ولو كان الخطأ 401، ممكن نوجه المستخدم للصفحة المناسبة:

<div dir="auto" align="left">

```typescript
intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  const token: string = 'invalid token';
  req = req.clone({ headers: req.headers.set('Authorization', 'Bearer ' + token) });

  return next.handle(req).pipe(
    catchError(err => {
      console.error(err);
      if (err instanceof HttpErrorResponse) {
        console.log(err.status, err.statusText);
        if (err.status === 401) {
          // توجيه المستخدم لصفحة تسجيل الدخول
        }
      }
      return of(err); // بترجع الخطأ كـ Observable
    })
  );
}
```

</div>

### إلغاء الطلب باستخدام EMPTY

#### ليه ممكن نحتاج نلغي الrequest

لو المستخدم مش مسجّل دخول مثلاً، ممكن نلغي الطلب عشان ما يتبعتش للسيرفر، وده بنعمله بإرجاع EMPTY (اللي هو Observable فاضي).

<div dir="auto" align="left">

```typescript
import { EMPTY } from 'rxjs';

intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
  if (NotLoggedIn) {
    return EMPTY; // الطلب مش هيتبعت
  }

  return next.handle(req);
}
```

</div>

</div>

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
