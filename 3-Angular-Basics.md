## Angular Basics

1. **Binding Syntax:**
   - Interpolation: Create a variable in the `component.ts` file and then use it in the `component.html` using `{{variableName}}`.
   - Property Binding: Angular also allows you to use native HTML attribute properties. For example, if you have `noOfRooms = 10` in your `component.ts` file, then in your `.html` file, you need to have this `<div [innerText]="noOfRooms"></div>`.
   - Event Binding: We use this for interaction with the app. For example, if you need to have a click event, you would use banana syntax `<button (click)="toToggle()"></button>`.

2. **Directives:**
   - Directives are used to change the behavior and appearance of DOM elements.
   - Directives can implement all lifecycle hooks. Directive cannot have a template.
   - **Types of Directives:**
     - *Structural Directives:* In Angular, structural directives are used to manipulate the DOM layout by adding, removing, or altering elements based on certain conditions.
       - `<div *ngIf="isVisible">Content to show when isVisible is true</div>`
       - `<div *ngFor="let key of objectKeys(myObject)">{{ myObject[key] }}</div>`
       - ```
         <div [ngSwitch]="condition">
          <div *ngSwitchCase="'case1'">Content for case1</div>
          <div *ngSwitchCase="'case2'">Content for case2</div>
          <div *ngSwitchDefault>Default content</div>
        </div>
        ```
     - *Attribute Directives:* In Angular, attribute directives are used to modify the behavior or appearance of DOM elements by manipulating their attributes. Attribute directives are applied to elements as attributes in HTML markup.
       - `ngClass`: Allows you to conditionally apply CSS classes to elements based on expression evaluation.
         - `<div [ngClass]="{'active': isActive, 'disabled': isDisabled}">...</div>`
       - `ngStyle`: Allows you to conditionally apply inline styles to elements based on expression evaluation.
         - `<div [ngStyle]="{'font-size.px': fontSize, 'color': fontColor}">...</div>`
       - `ngModel`: Provides two-way data binding for form inputs, syncing the value of the input field with a property on the component.
         - `<input type="text" [(ngModel)]="name">`

3. **Pipes:**
   - Pipes are used for data transformation.
   - Pipes do not change the actual object.
   - **Common Pipes:**
     - `DatePipe`: Formats a date value according to locale rules.
     - `UpperCasePipe`: Transforms text to all upper case.
     - `LowerCasePipe`: Transforms text to all lower case.
     - `CurrencyPipe`: Transforms a number to a currency string, formatted according to locale rules.
     - `DecimalPipe`: Transforms a number into a string with a decimal point, formatted according to locale rules.
     - `PercentPipe`: Transforms a number to a percentage string, formatted according to locale rules.
     - `AsyncPipe`: Subscribe and unsubscribe to an asynchronous source such as an observable.
     - `JsonPipe`: Display a component object property to the screen as JSON for debugging.

4. **Adding Bootstrap to Our Project:**
   - Stop the `ng serve` and then use `ng add ngx-bootstrap`.
   - Also, make sure to update styles and scripts in `angular.json`.
