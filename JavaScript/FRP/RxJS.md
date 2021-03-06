# RxJS

> Treating events as collections and manipulating sets of events with "operators"

Few applications are completely synchronous, and writing async code is necessary to keep applications responsive.

Imagine you have a normal array, you can `filter`, `map`, `reduce` all you can. But what happen if the array is asynchronous and streaming?

Application is all about "data flow".

* [ECMAScript Observable](https://github.com/zenparsing/es-observable)
* [Rx-book](http://xgrommx.github.io/rx-book/index.html)
* [Reactive course at Coursera](https://www.coursera.org/course/reactive)
* [How to debug RxJS code](http://staltz.com/how-to-debug-rxjs-code.html)
* [Thoughts on RxJS: It is overkill?](https://medium.com/@BrianDiPalma/thoughts-on-rxjs-cf3562e20d74#.euhg705ok)
* [RxJS vs Async.js](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/mapping/async/comparing.md)
* [Slide](https://github.com/npm/slide-flow-control)
* [Step](https://github.com/creationix/step)
* [rxjs-examples](https://github.com/annatomka/rxjs-examples)
* [React and RxJS](https://github.com/whiteinge/presentations/blob/master/react-rally_2015-08-24_react-rxjs/presentation.rst#rx-)

We have many PUSH APIs:

* DOM events
* WebSockets
* Node Streams
* Service Workers
* Server-Sent Events
* XHR (1 value, good for Promises)
* setInterval
* Animation (Cancellable)

Each has their own way of dealing with asynchronous data like:

* Callback functions - callback hell, poor concurrency
* Promises - only ever yield a single value, not good for recurring events. Can't be cancelled?
* Event emitters

> What does SQL, spreadsheet has in common with Reactive system?

## Thinking in Stream

You have to twist your mind and think in stream.

Imagine every variable is a stream. To get it, you need to figure out where it comes from. It could come from other variables, or it could come from an event. Figure out your side effects, these are the exit points for your data flow.

## Memory Cleaning

No need for external state tracking. No need to cleanup after yourself either.

## Observables

Note: Observables and Event Emitters are just different variations on the Observer design pattern.

* [Lifted Observable?](https://github.com/ReactiveX/RxJS/issues/60)

**Observable** == Stream of events from a data source like mouse events, network requests, array of strings, etc.

**Observer** == Handlers or listeners to do "your things" like combine or transformation, etc.

Observable is a datatype by Reactive Extensions (Rx). It abstracts away the concept of a data source that represent a stream of events. We treat mouse, click, network events as a "database" that we can query from.

It is being proposed for ES7. What does observable represents? It is a collection over time. Essentially, it is stream of events.

RxJS is push-based, so the source of events (Observable) will push new values to the consumer (Observer), without the consumer needing to request the next value.

```js
// Observable always start from a place, a source if you will, to get data from.
// In this case, the data is just a simple click event generated by the user.
var clicks = Rx.Observable.fromEvent(button, 'click');

// Filter out clicks that happen on the right side of the screen and logs only the first 10 clicks
Rx.Observable.fromEvent(document, 'click')
  .filter(c => c.clientX > window.innerWidth / 2)
  .take(10)
  .subscribeOnNext(c => console.log(c.clientX, c.clientY));
```

We are subscribed to sequences, not only to discrete values.

Observables don't do anything until at least one Observer subscribes to them.

> Observable is not a replacement for Enumerable. I would not recommend trying to take something that is naturally pull-based and force it to be push-based.

```js
// Autocomplete example
var q = document.querySelector('#q');
var resultList = document.querySelector('#result');

var Observable = Rx.Observable;

var keyups = Rx.Observable.fromEvent(q, 'keyup');

keyups.throttle(500)
  .map(() => q.value)
  .do(() => q.classList.add('spinner))
  .flatMapLatest(query => Rx.DOM.ajax({
    method: 'GET',
    url: '/autocomplete?q=' + query,
    responseType: 'json'  }))
  .do(() => q.classList.remove('spinner')) // Do side effect
  .map(r => r.response)
  .map(results => results.reduce((html, result) => `${html}<li>${result}</li>`))
  .subscribe(resultsHTML => resultList.innerHTML = resultsHTML);
```

## Observer

Observer is the handler.

```js
var observer = Observer.create(function next(x) {});

myObservable.subscribe(observer);
myObservable.subscribe(function next(x) {}); // Same

myObservable.subscribe(success, error, complete);
```

## Operators

* [Docs for Operators](https://github.com/Reactive-Extensions/RxJS/tree/master/doc/api/core/operators)

Operators are methods on `Observable` that allow you to compose new observables.

In RxJS, methods that transform (map) or query sequences are called operators.

`create` and `fromEvent` are all creation operators. They create Observables for common sources.

Observables are immutable, and every operator applied to them creates a new Observables.

* `map`
* `flatMap`
* `filter`
* `reduce`
* `catch`

## Schedulers

## RxJS with React

* [Why I'm tired of using and teaching flux](https://gist.github.com/justinwoo/08f9f8fcdcf865025f18)

```js
var Counter = React.createClass({
  componentWillMount() {
    this.onButtonClick = new Rx.Subject();
    
    this.subscription = (
      this.onButtonClick.start
      .startWith(0)
      .scan(acc => acc + 1)
      .subscribe(count => this.setState({count}))
    );
  },
  
  componentWillUnmount() {
    this.subscription.dispose();
  },
  
  render() {
    return (
      <div>
        {this.state.count}
        <button onClick={() => this.onButtonClick.onNext()}>Increment</button>
      </div>
    );
  }
});
```

# Videos

* [Ben Lesh Talks RxJS at Modern Web UI](https://www.youtube.com/watch?v=yk_6eU3Hcwo)
* [Channel 9 RxJS](https://channel9.msdn.com/Tags/rxjs)
* [What's new in RxJS 5.0 with Ben Lesh](https://www.youtube.com/watch?v=9on6u7pI3vY)
* [DevChat.tv - RxJS with Matthew Podwysocki](https://devchat.tv/js-jabber/182-jsj-rxjs-with-matthew-podwysocki)
* [**It was an Observation, I Promise**](https://www.youtube.com/watch?v=XhVyrAFed58)