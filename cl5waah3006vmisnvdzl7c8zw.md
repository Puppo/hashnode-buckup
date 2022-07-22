## RxJS - Marble Diagrams

Hi guy,
before continuing with the operators, today I want to explain the _Marble Diagrams_.
The Marble Diagrams is a timeline where you can illustrate the state of your observable during its execution.
The actors in this diagram are timeline and values(circle).
The timeline is used to represent the time during the execution of the observable though the circles indicate the values emitted.
But let me show you an example:
![map marble diagram](https://cdn.hashnode.com/res/hashnode/image/upload/v1658483264637/cEu1DeUbo.jpeg)

This example is based on this code
```ts
import { Observable } from "rxjs";
import { map } from "rxjs/operators";

const source$ = new Observable<number>(observer => {
  let count = 0;
  const id = setInterval(() => {
    if (count++ < 3) {
      observer.next(count);
    } else {
      clearInterval(id);
      observer.complete();
    }
  }, 1000);
});

source$.pipe(map(value => value * 2)).subscribe({
  next: console.log,
});
```
As you can notice, in the diagram there are two timelines, one for the source and the other for the map operator.
In the first timeline you can see when the source emits the value, in the second timeline you can see the result of the transformation after the execution of the map operator.

To build a Marble diagram you need to keep in mind some easy rules: there is always a timeline that represents the source observable, there are N timelines as many operators as you need to display, every timeline illustrates the state of the values after the execution of the operator indicated in the timeline and finally, you need to use a circle to represent the values.

This tool is very convenient to illustrate the transformation of the observable during its execution and it helps us to have an image of the state of the observable execution.

In addition to the Marble Diagram you can use the Marble Testing to test the execution of you Observable.
The Marble testing uses a special format to represent the timeline and the value during the execution, but I will speak about it in the future.

To reinforce the Marble Diagram concept let me show you another example

```ts
import { Observable } from "rxjs";
import { delay, map } from "rxjs/operators";

const source$ = new Observable<number>(observer => {
  let count = 0;
  const id = setInterval(() => {
    if (count++ < 3) {
      observer.next(count);
    } else {
      clearInterval(id);
      observer.complete();
    }
  }, 1000);
});

source$
  .pipe(
    map(value => value * 2),
    delay(1500)
  )
  .subscribe({
    next: console.log,
  });
```
![Marble Diagram Map+Delay](https://cdn.hashnode.com/res/hashnode/image/upload/v1658483265991/edWSriUOEx.jpeg)

In this example you can see how the observable in the first operator doubles the value and then it waits 1.5 seconds before emitting the result.
To represent this case the marble diagram has 3 timelines, one with the source, one with the map operator and one with the delay operator. Every timeline indicates the value during the execution of its operator so you can see the behaviour of this implementation.

It's all from the marble diagram.

See you soon guys!
