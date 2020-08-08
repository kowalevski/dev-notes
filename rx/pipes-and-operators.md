## Pipe and Operators

```javascript
import { interval } from "rxjs";
import { map, filter, take } from "rxjs/operators";

// interval(N): Observable<number> - creates and return Observable that emits incremental numbers every N milliseconds

/**
 * pipe() is just function whose work can be imagined like tube
 * that tube just takes some stream of values and give that values
 * values in pipe can be modified by operators like filter, map and others
 */

// filter and map are operators. they take every value that "flows" in pipe and give that value back
// returned value can be modified or filtered by operators

// take(N) is operator that emits only the first N values.
// When count of values will be more than N - Observable will stop;

interval(1000)
  .pipe(
    filter(number => number % 2 === 0),
    map(number => number * 2),
    take(4)
  )
  .subscribe(finalVal => console.log(finalVal));

// result: 0, 4, 8, 12
```
