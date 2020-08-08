## Observable, Subscription, Observers

- **Observable** - collection of future values or events;
- **Observer** - collection of callback functions that knows how to listen values from Observable
- **Subscription** - execution of Observable

Example of simple using Observable with Subscriber and Observer

```javascript
import { Observable } from "rxjs";

const observer = {
  next: console.log,
  error: console.log,
  complete: () => {
    console.log("there are no more values!");
  }
};

const observable = new Observable(subscriber => {
  subscriber.next("*****Hello from Observable class*****");
  subscriber.error("***Error***");
  subscriber.complete("***Complete***");
});

observable.subscribe(observer);
```


