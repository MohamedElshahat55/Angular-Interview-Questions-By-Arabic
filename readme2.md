<!-- # Error Handling in Angular Applications -->

<!-- ## Why Handle Errors?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في Angular، التعامل مع errors جزء مهم من تصميم التطبيق لأن JavaScript ممكن ترمي errors في أي وقت يحصل فيه حاجة غلط. مثلاً

1 - لو استخدمنا متغير مش موجود.
2- لو القيمة اللي قدمناها خارج scope المسموح بيه.
3- أو لو فيه مشكلة في الكود نفسه زي إن الكتابة غير صحيحة.
4- أو لو القيمة مش من النوع اللي المفروض تكون عليه.

بجانب الحاجات دي، ممكن يحصل errors غير متوقعة زي انقطاع الاتصال، مفيش إنترنت، أو HTTP errors زي المستخدم غير مصرح له أو إن (Session) انتهت.

### التعامل مع HTTP Errors

الـ HTTP Errors بتحصل لما نبعت request باستخدام HttpClient في Angular. الـ errors دي ممكن تكون إما من السيرفر (زي مستخدم غير مسموح أو انتهاء الجلسة)، أو من عند العميل (زي فشل الاتصال). الفكرة إن HttpClient بيقدر يتعامل مع الـ HTTP responses، والـ errors بتتقسم لنوعين رئيسيين:

1- الErrors من السيرفر: زي ما يكون المستخدم غير مصرح له (401 Unauthorized) أو انتهت Session أو السيرفر واقع.
2- الErrors من العميل: زي حصول مشكلة في الاتصال بالشبكة أو عدم القدرة على ارسال الـ request بشكل صحيح.

### Client-Side Errors

الأخطاء اللي بتحصل في الكود مباشرة بتتسمى Client-Side Errors، ودي بيتم التعامل معاها عن طريق ErrorHandler وهو الـ default error handler اللي Angular بيستخدمه عشان يمسك أي exception غير متوقع.

### Global Error Handler

بشكل افتراضي، ErrorHandler في Angular بيمسك كل errors اللي بتحصل في التطبيق، لكن دوره بيقتصر على طباعتها في الـ console. لكن في التطبيقات الكبيرة، لازم يكون عندنا Global Error Handler مخصص عشان نقدر نعرض رسائل واضحة للمستخدم أو نبعت التقارير دي للسيرفر لمتابعة errors.

### خطوات عمل Global Error Handler

1- بنعمل سيرفس جديد بتimplements من ErrorHandler.
2- نستخدم الـ handleError

### مثال بسيط

<div dir="auto" align="left">

```typescript
import { ErrorHandler, Injectable } from "@angular/core";

@Injectable()
export class GlobalErrorHandlerService implements ErrorHandler {
  handleError(error) {
    console.error("An error occurred:", error.message);
    alert("An error occurred, please try again later!");
  }
}
```

</div>


### inject another service in Global Error Handler

ممكن تحتاج إنك تستخدم service زي Router عشان تعمل توجيه للمستخدم لصفحة مخصصة للخطأ. بس Angular بتعمل الـ Error Handler قبل ما باقي الـ services تبقى جاهزة، عشان كده بنستخدم حاجة اسمها Injector عشان نحقن الservice يدويًا.

<div dir="auto" align="left">

```typescript
import { ErrorHandler, Injectable, Injector } from "@angular/core";
import { Router } from "@angular/router";

@Injectable()
export class GlobalErrorHandlerService implements ErrorHandler {
  constructor(private injector: Injector) {}

  handleError(error) {
    let router = this.injector.get(Router);
    console.log("Navigating to error page");
    router.navigate(["/error"]);
  }
}
```

</div>
</div>
<hr/>

## What is a HttpErrorResponse?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">
في Angular، التعامل مع HTTP Errors حاجة أساسية عشان تخلي التطبيق بتاعك أكتر استقرارًا. لما يحصل error أثناء عملية الـ HTTP، Angular بيغلف الـ error ده في object اسمه HttpErrorResponse، وبعد كده بيرجعه للتطبيق بتاعك.

ال object ده فيه معلومات مهمة عن الـ error زي سبب المشكلة والـ status code (زي 401 Unauthorized أو 404 Not Found). الـ HttpErrorResponse بيحتوي على الـ error اللي حصل سواء من السيرفر أو من الكود بتاع العميل.

</div>
<hr/>

## How Can Catching Errors in HTTP Request?

[⬆️ Back to Top](#top)

<div dir="auto" align="right">

### في Angular، ممكن تمسك الـ HTTP errors في 3 أماكن مختلفة:

1- في الـ Component
2 -في الـ Service
3- على المستوى العام باستخدام HTTP Interceptor

### التعامل مع Errors في الـ Component

أنت ممكن تمسك الـ HTTP errors في الكومبوننت بعد ما تعمل request. على سبيل المثال، لو أنت عامل GitHubService عشان تجيب البيانات من API زي الـ Repositories الخاصة بمستخدم، هتكتب subscribe للـ HTTP request في الكومبوننت عشان تتعامل مع الـ response والـ error.

#### في الكومبوننت، الـ subscribe بياخد 3 callbacks:

##### success: لما الـ request ينجح.

##### error: لو حصل error في الـ request.

##### completed: لما الـ observable ينتهي بدون مشاكل.

<div dir="auto" align="left">

```typescript
public getRepos() {
  this.loading = true;
  this.errorMessage = "";
  this.githubService.getRepos(this.userName)
    .subscribe(
      (response) => { // Next callback
        console.log('response received');
        this.repos = response;
      },
      (error) => { // Error callback
        console.error('error caught in component');
        this.errorMessage = error;
        this.loading = false;
      }
    );
}
```

</div>
✨ هنا لو حصل error زي URL غلط، الـ error هيتخزن في الـ errorMessage وتقدر تتعامل معاه في الـ UI، وتظهر رسالة للمستخدم.

### التعامل مع Errors في الـ Service

أنت كمان ممكن تمسك الـ HTTP errors في الـ service اللي بيعمل الـ request باستخدام الـ catchError من مكتبة RxJS.

<div dir="auto" align="left">

```typescript
getRepos(userName: string): Observable<any> {
  return this.http.get<repos[]>(this.baseURL + 'usersY/' + userName + '/repos')
    .pipe(
      catchError((err) => {
        console.log('error caught in service');
        console.error(err);
        return throwError(err); // رمي الـ error تاني عشان الكومبوننت يتعامل معاه
      })
    );
}

```

</div>
 ✨هنا بنمسك الـ error في الـ service نفسه، وممكن نعمل معاه حاجة زي طباعة رسالة أو إرسالها لملف لوج، وبعد كده بنرميه تاني عشان الكومبوننت يعرف يتعامل معاه.

 ### التعامل مع Errors على المستوى العام باستخدام Interceptor

 لما تيجي تتعامل مع HTTP errors اللي بتحصل كتير (زي Unauthorized 401 أو Not Found 404)، مش منطقي إنك تمسك كل error في كل component أو service. هنا بييجي دور الـ HTTP Interceptor. الـ interceptor هو سيرفس بيشتغل في الخلفية وبيمسك كل request وresponse وبيعمل interception للـ errors عشان يتعامل معاها.

 #### مثال لإنشاء HTTP Interceptor
 <div dir="auto" align="left">

```typescript
@Injectable()
export class GlobalHttpInterceptorService implements HttpInterceptor {

  constructor(public router: Router) { }

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(req).pipe(
      catchError((error) => {
        if (error instanceof HttpErrorResponse) {
            switch (error.status) {
                case 401:
                    this.router.navigateByUrl("/login");
                    break;
                case 403:
                    this.router.navigateByUrl("/unauthorized");
                    break;
            }
        }
        return throwError(error);
      })
    );
  }
}
```

</div>
لما السيرفر يبعت error response، بيبقى فيه HTTP Status Code بيوضح نوع الـ error، زي 401 (Unauthorized) أو 404 (Not Found). على حسب الكود ده، ممكن نعمل خطوات معينة:

Error 401 (Unauthorized): هنا ممكن نعمل redirect لصفحة تسجيل الدخول.
Error 403 (Forbidden): نقدر نوجه المستخدم لصفحة غير مصرح له بالدخول ليها.
#### 🧨 بعد كده لازم تسجل الـ Interceptor في الـ AppModule

<div dir="auto" align="left">

```typescript
providers: [
  { provide: HTTP_INTERCEPTORS, useClass: GlobalHttpInterceptorService, multi: true }
]
```

</div>

#### 🚀 الـ Interceptor ده هيمسك كل الـ HTTP requests اللي بتمر في التطبيق، ويتعامل مع الأخطاء العامة زي الأخطاء اللي جاية من السيرفر أو مشاكل الشبكة.
</div> -->

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
