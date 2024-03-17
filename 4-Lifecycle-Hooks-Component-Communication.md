
## Lifecycle Hooks and Component Communication

- In Angular, lifecycle hooks are methods that provide visibility into key lifecycle events in the components and directives. These hooks allow you to perform actions at specific points in the component's lifecycle, such as initialization, change detection, and destruction. Lifecycle ends when the component is destroyed.
- These hooks allow you to perform actions at specific points in the component's lifecycle, such as initialization, change detection, and destruction. 
- Lifecycle ends when component is destroyed. 
- If you actually look at the component.ts file you will actually see an ngOnInit hook already exists on your newly created components. Every lifecycle hook has an interface i.e., `export class RoomsComponent implements OnInit {}`.
- Also in the same file, you can see a constructor() {}. In Angular, a constructor inside a component TypeScript file is used to initialize the component and its dependencies. It's a special method that is automatically called when a new instance of the component is created. Use constructor only for dependency injection and initialization. You can perform initialization tasks in the constructor, such as setting default property values or subscribing to observables. This allows you to set up the component's initial state before it's rendered.

Here are the lifecycle hooks available in Angular:

1. **ngOnChanges**: Called whenever one or more input properties of the component change. It receives a `SimpleChanges` object containing the previous and current values of the input properties.
   
2. **ngOnInit**: Called once after the first `ngOnChanges` and before any other lifecycle hooks. It's used for component initialization logic.
   
3. **ngDoCheck**: Called during every change detection run, immediately after `ngOnChanges` and `ngOnInit`. It allows you to implement custom change detection logic.
   
4. **ngAfterContentInit**: Called after Angular projects external content into the component's view, such as projected content (content children).
   
5. **ngAfterContentChecked**: Called after Angular checks the content projected into the component's view.
   
6. **ngAfterViewInit**: Called after Angular initializes the component's views and child views.
   
7. **ngAfterViewChecked**: Called after Angular checks the component's views and child views.
   
8. **ngOnDestroy**: Called just before Angular destroys the component or directive. It's used for cleanup logic such as unsubscribing from observables and detaching event handlers.

These hooks provide developers with a way to hook into specific moments of a component's lifecycle, enabling them to execute custom logic accordingly.

Component Communication: In Angular, there are several methods for component communication, allowing components to interact with each other, share data, and respond to events. Here are the common approaches:

- Input/Output Binding (Parent to Child):
  - Input Binding: Allows a parent component to pass data to a child component using property binding (`[property]="value"`).
  - Output Binding: Allows a child component to emit events to a parent component using event binding (`(event)="handler()"`).
- `@ViewChild` and `@ViewChildren`:
  - `@ViewChild`: Allows a parent component to access a child component's properties and methods directly.
  - `@ViewChildren`: Allows a parent component to access multiple child components of the same type.
- Service Communication:
  - Shared Service: Components can communicate via a shared service. The service acts as an intermediary, storing data or state that can be accessed by multiple components. Components can inject the service and use it to communicate with each other.
- Event Emitters:
  - Components can define custom events using Angular's EventEmitter class. Child components can emit events that parent components can listen to and respond to using event binding.
- RxJS Observables:
  - Components can use RxJS Observables to communicate asynchronously. Observables can be used for data streams, events, or state management. Components can subscribe to observables to receive data and notify other components about changes.
- `@Input()` and `@Output()` Decorators:
  - Components can use `@Input()` and `@Output()` decorators to define input and output properties, allowing parent and child components to communicate by passing data via these properties.
- NgRx (Redux Pattern):
  - For complex state management and communication between components, NgRx can be used. NgRx is a state management library for Angular that implements the Redux pattern. It provides a centralized store, actions, reducers, and selectors for managing application state.

### Parent and Child communication using @Input @Output:

child.component.ts
```
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <div>
      <p>Child Component</p>
      <p>Received message from parent: {{ message }}</p>
      <button (click)="sendMessageToParent()">Send Message to Parent</button>
    </div>
  `
})
export class ChildComponent {
  @Input() message: string;
  @Output() messageToParent = new EventEmitter<string>();

  sendMessageToParent() {
    this.messageToParent.emit("Message from child component");
  }
}
```

parent.component.ts

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <div>
      <p>Parent Component</p>
      <app-child [message]="parentMessage" (messageToParent)="receiveMessageFromChild($event)"></app-child>
    </div>
  `
})
export class ParentComponent {
  parentMessage = "Hello from parent";

  receiveMessageFromChild(message: string) {
    console.log("Received message from child:", message);
  }
}
```

In this example:

- The ChildComponent has an @Input property called message, which receives data from the parent component.
- It also has an @Output property called messageToParent, which emits events to the parent component.
- When the child component button is clicked, it emits a message to the parent component using the messageToParent event emitter.
- The ParentComponent passes data to the child component using property binding [message]="parentMessage", where parentMessage is a property defined in the parent component.
- The parent component also listens for events emitted by the child component using (messageToParent)="receiveMessageFromChild($event)".
- This setup allows for communication between parent and child components using @Input and @Output decorators in Angular.

### Change Detection:

- Change Detection in angular: Now by default each time theres a change like using a button or selecting something angular rerenders the view. Even if you change something in a parent component its children are also rerendered to overide this behavior you can use onPush change Detection

```
import { ChangeDetectionStrategy } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class ExampleComponent {
  // Component logic
}
```
OnPush Change Detection: This is a change detection strategy where Angular only checks for changes in the component's inputs (i.e., @Input properties) and not for changes in its internal state unless explicitly triggered. You can enable this strategy by setting the changeDetection property of the component to ChangeDetectionStrategy.OnPush. But for this to work you needto keep a fe wthings in mind 1. you should have @Input/@Output 2. you should have immutable data for an instance do not chnage the data by using .push instead use the spread operator like so (...arr, rooms). This creates an entirely new array instead of mutating the current one.

- Some other ways to avoid unnecessary actions use the below:
a. ure Pipes: If you have custom pipes, ensure they are pure pipes (@Pipe({ pure: true })). Pure pipes are only recalculated if their input parameters change, reducing unnecessary recalculations.
b. rackBy Function: When using *ngFor directive to iterate over a list, provide a track by function to help Angular identify which items have changed. This can significantly improve performance when dealing with lists.
```
<div *ngFor="let item of items; trackBy: trackByFn">
  {{ item }}
</div>
```
```
trackByFn(index: number, item: any): any {
  return item.id; // Use a unique identifier for the item
}
```
c. Detached Change Detection: In rare cases where you need fine-grained control over change detection, you can manually detach and reattach change detection using ChangeDetectorRef. This can be useful for optimizing specific parts of your application.

```
import { ChangeDetectorRef } from '@angular/core';

constructor(private cdr: ChangeDetectorRef) {}

ngAfterViewInit() {
  this.cdr.detach(); // Detach change detection
}

someMethod() {
  // Perform some operations
  this.cdr.detectChanges(); // Reattach and run change detection
}
```

- ngOnChanges can only be applied to those components or directives that have an @Input property

- ngDoCheck: It's important to use ngDoCheck judiciously, as it can impact the performance of your application if used incorrectly or excessively. It's typically used when you need to perform manual change detection for optimizations or when working with complex state management that Angular's default change detection mechanism might not handle efficiently.


