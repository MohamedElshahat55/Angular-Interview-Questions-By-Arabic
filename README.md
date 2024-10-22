<a name="top"></a>

# Angular RxJS Interview Questions

| No. | Questions                                                                                                                          |
| --- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 1   | [Explain RxJS Observable?](#explain-rxjs-observable)                                                                               |
| 2   | [What are RxJS operators?](#what-are-rxjs-operators)                                                                               |
| 3   | [What is Observable.pipe() and how to use it?](#what-is-observablepipe-and-how-to-use-it)                                          |
| 4   | [What is the difference between RxJS of and from?](#what-is-the-difference-between-rxjs-of-and-from)                               |
| 5   | [Explain RxJS map operator?](#explain-rxjs-map-operator)                                                                           |
| 6   | [Explain RxJS switchMap operator?](#explain-rxjs-switchmap-operator)                                                               |
| 7   | [Explain RxJS mergeMap operator?](#explain-rxjs-mergemap-operator)                                                                 |
| 8   | [Explain RxJS concatMap operator?](#explain-rxjs-concatmap-operator)                                                               |
| 9   | [Explain RxJS exhaustMap operator?](#explain-rxjs-exhaustmap-operator)                                                             |
| 10  | [How will you handle errors on observable using RxJS throwError?](#how-will-you-handle-errors-on-observable-using-rxjs-throwerror) |
| 11  | [How will you handle errors on observable using RxJS catchError?](#how-will-you-handle-errors-on-observable-using-rxjs-catcherror) |
| 12  | [Explain RxJS retry operator?](#explain-rxjs-retry-operator)                                                                       |
| 13  | [Explain RxJS filter operator?](#explain-rxjs-filter-operator)                                                                     |
| 14  | [Explain RxJS tap operator?](#explain-rxjs-tap-operator)                                                                           |
| 15  | [Explain RxJS takeUntil operator?](#explain-rxjs-takeuntil-operator)                                                               |
| 16  | [Explain RxJS takeWhile operator?](#explain-rxjs-takewhile-operator)                                                               |
| 17  | [Explain RxJS takeLast operator?](#explain-rxjs-takelast-operator)                                                                 |
| 18  | [Explain RxJS take operator?](#explain-rxjs-take-operator)                                                                         |
| 19  | [Explain RxJS debounce operator?](#explain-rxjs-debounce-operator)                                                                 |
| 20  | [Explain RxJS debounceTime operator?](#explain-rxjs-debouncetime-operator)                                                         |
| 21  | [Explain RxJS combineLatestWith operator?](#explain-rxjs-combinelatestwith-operator)                                               |
| 22  | [Explain RxJS fromEvent operator?](#explain-rxjs-fromevent-operator)                                                               |

## Explain RxJS Observable

Observable في RxJS هو طريقة لتبادل البيانات بين اللي بينتجها ( producer) واللي بيستخدمها ( consumer). تخيل إن فيه حد بيبعث لك بيانات، بس مش هتبعت لك غير لما تطلبها (ده نظام pull)، أو ممكن البيانات تتبعت لك من غير ما تطلبها (ده نظام push).

في JavaScript العادي، أنت اللي بتطلب البيانات (ده زي pull). لكن في RxJS Observable، البيانات بتتبعت لك تلقائيًا أول ما تعمل subscribe للـ Observable (ده نظام push).

في Angular، Observable بتبدأ تشتغل لما تعملها subscribe، وبتقدر تعمل كده إما باستخدام subscribe مباشرةً أو باستخدام async pipe.

وأي دالة في HttpClient في Angular، زي اللي بتعمل طلبات HTTP، بترجع Observable، يعني البيانات بتتبعت لك أول ما تعمل subscribe ليها.

[⬆️ Back to Top](#top)
