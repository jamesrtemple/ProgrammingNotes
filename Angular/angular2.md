# Components

``` TypeScript
import { Component } from '@angular/core'

@Component({
  selector: 'class-name',
  template: `
  template goes here
  `
  })
  export class ClassNameComponent {
    data1: string = 'data1';
    data2: any;

    method1(): void {
    //do stuff with no return value
    }
  }
```

## ViewMetaData
1. *selector*  
   *The selector for the component. It can be a new HTML 
   element name, attibute, class, etc. In most cases, the selector is
   set for a new HTML element name.
2. *template*  
   an HTML markup to be rendered when the component is set.
3. *templateUrl*  
   A URL points at an HTML file that contains the template.
4. *directives*  
   An array of types of other components or directives used by this
   component.
5. *pipes*  
   An array of pipes used by the component as pipes (See pipes later
   on in this chapter)
6. *Styles*  
   An array of strings where each string is a style rule
7. *styleUrlS*  
   A URL to an external CSS file 
8. *encapsulation*  
   The encapsulation type of the view
9. *providers*  
   An array of types of injectable services used by the
   components. When the component is instantiated, an instance of the
   provider is instantiated as well.
   
## ViewEncapsulation
An enumeration with 3 possible values for #8 above.
1. *Native*  
   Uses the brower's native encapsulation mechanism, using the Shadow DOM
   for the component and creating a Shadow Root on the component's host
   element.
2. *Emulated*  
   Emulates native encapsulation by adding surrugate IDs and
   preprocessing of the style rules. **Default**
3. *None*  
   No style is encapsulated for the component.

## Component Life Cycle Events
1. *OnInit*  
   occurs after the component is being initialized
2. *OnDestroy*  
   occurs before a component is destroyed
3. *OnChanges*  
   occurs on every change that occurs in the component data
4. *DoCheck*  
   extends the OnChanges handler, and when DoCkeck is implemented, it
   overrides the default change detection algorithm
5. *AfterContentInit*  
   occurs after content init

In order to hook one of these lifecycle events you should implement its corresponding interface (inerface names are listed above). Each interface has a method that will handle the lifecycle event.


# Attribute Directive
``` TypeScript
import {Directive, ElementRef} from '@angular/core'

@Directive({
	selector: '[edge-select]' 
})
export class SelectDirective {
    constructor(private _el: ElementRef) {
		_el.nativeElement.style.border = '2px solid #00897b';
	}
}
```

``` TypeScript
import {Directive, ElementRef} from '@angular/core'

@Directive({
	selector: '[edge-select]',
	host: {      '(dblclick)': 'onDoubleClick()'    }
})
export class SelectDirective {
	constructor(private _el: ElementRef) {}

	private selected: boolean = false;
	
	onDoubleClick() {
		if (!this.selected) {
			this._el.nativeElement.style.border = '2px solid #00897b';
			this.selected = true;
		}
		else {
			this._el.nativeElement.style.border = 'none';
			this.selected = false;
		}
	}
}
```

# Services

## 3 Steps to consuming a service

1. Import the service
2. Include it in the providers array of the module or component
3. Include it as a private parameter in the constructor

# Data Binding
There are 4 types of binding in Angular2:

## Interpolation

<h1>{{pageTitle}}</h1>

...where pageTitle is a property of our component class.

## Property Binding

<tag [target] = 'class.value'>

ex: <img [src]='product.imageUrl' [title]='product.title'>

## Event Binding

<tag (event)='handler()'>

ex: <button (click)='toggleProperty()'>Toggle It</button>
...where toggleProperty is a method on the component class.
(event) can be any valid DOM event.

## Two Way Binding

<tag [(ngModel)]='value'>

ex: <input [(ngModel)]='listFilter'>

ngModel is defined in the FormsModule in @angular/forms.
import {FormsModule} from '@angular/forms';
Add FormsModule to imports of AppModule

# Change Detection

List of things that can cause changes to the model
1. events: click, blur, submit, ...
2. timers: setinverval, settimeout, ...
3. xhrs: ajax(get, post, ...)

i.e. all asynchronous operations can cause changes

## Zones

a *zone* is a global object that intercepts and keeps track of
asynchronous work. angular uses zone.js for it's implementation of
this concept but customizes it with *ngzone*.

``` TypeScript
import {OnChanges} from `@angular/core`;

@Component({...})
class MyComponent implements OnChanges {
	@Input() prop;
	
	ngOnChanges(changes: {[propName: string]: SimpleChange}) {
		let newValue = changes['prop'].currentValue;
	}
}
```


ngOnChanges is called only when its property is changed by its
parent. So, you must never modify any input properties in your own
component. You should access those as read-only.

### OnPush Strategy

Setting the value *changeDetection* in the component initialization
object to *ChangeDetectionStrategy.OnPush* will cause events raised by
the parent to stop bubbling up to children. This will optimize event
handling in situations where a change is broadcast from the root
module but change detection isn't needed for children of a component.

Note that changes only trigger change detection when the original
value is not equal to the new value. For references, this means that
you must create a new object because change detection is looking for
updates to the reference value itself, not that which is referenced.

# Forms

## There are 2 paradigms for form creating on ng2

1. Template-driven forms
2. Reactive forms

## Steps to create a form

1. Create the model class
   This should be a simple POJSO with fields to hold form data.
2. Create the component that controls the form
   Imports and uses the model class from step 1
3. Add the FormsModule and our new component from step 2 to the
   application module
   FormsModule is defined in @angular/forms and is included in the
   imports array
   The component from step 2 is included in the declarations array.
3. Create a template with the initial form layout
4. Bind data properties to each form input control with ngModel
   two-way data binding syntax.
5. Add the name attribute to each form input control.
6. Add custom CSS to provide visual feedback
7. Show and hide validation error messages
8. Handle form submission with ngSubmit.
9. Disable the form submit button until the form is valid.

## Review Template Reference Variables

Note the use of name and ngModel in the input tag below. Both are
necessary in order for the ng form to know about and monitor the input
field state. Also note that novalidate should be set on the form tag.

``` TypeScript
<form #form="ngForm" novalidate>
	<input type="text" placeholder="Name" name="name" ngModel>
	<button type="submit">OK</button>
</form>
```

## CSS Validation Classes

ng-touched, ng-untouched
ng-pristine, ng-dirty
ng-valid, ng-invalid

# Component Interaction
## Input Binding

Pass Data from parent to child with input binding in the component tag.

``` TypeScript
@Input() myvalue: string;
```

## Intercept input property changes with a setter

Pass data from parent to child where operations are required when the
value is explicity set in the component tag.

``` TypeScript
@Input()
set name(name: string) {
	this._name = name.trim();
}
```

## Intercept input property changes with ngOnChanges

In this method, ngOnChanges will be called when/if the parent changes
the value of myvalue.

``` TypeScript
export class MyClass implements OnChanges {
	@Input() myvalue: string;
	
	ngOnChanges(changes: {[propKey: string]: SimpleChange}) {
		//...
	}
}
```

## Parent listens for child event

Use this method to provide standard HTML like events on components.

``` TypeScript
@Output() onVoted = new EventEmitter<boolean>();
//...
this.onVoted.emit(isAgreed);
```

## Parent interacts with a child via a template local variable

Use this method if all access to the child can be done within the
template of the parent.

``` TypeScript
template: `
	<h3>Countdown via local var</h3>
	<button (click)="timer.start()">Start</button>
	<button (click)="timer.stop()">Stop</button>
	<div>{{timer.seconds}}</div>
	<countdown-timer #timer></countdown-timer>
`
```

## Parent calls a ViewChild

``` TypeScript
import { AfterViewInit, ViewChild } from '@angular/core';
import { Component } from '@angular/core';
import { MyChildComponent } from 'path/to/component';
//...
export class MyParentClass implements AfterViewInit {
	@ViewChild(MyChildComponent)
	private childComponent: MyChildComponent;
	
	value: string;
	
	ngAfterViewInit() {
		//Need the setTimeout here to avoid a
		unidirectional-data-flow-violation error!
		setTimeout(() => this.value = () => this.childComponent.value, 0);
	}
	
	someMethod() {
		//You can access methods of the child component too!
		this.childComponent.someMethod('Yay!');
	}
}
```

## Parent and children communicate via a service
# Custom Controls
# Notes from Pascal Precht
From his blog post at:
http://blog.thoughtram.io/angular/2016/07/27/custom-form-controls-in-angular-2.html

## Questions to ask before creating a custom control

1. Is there a native element that has the same semantics?
2. If yes, can we simply rely on that element and use CSS and/or progressive enhancement to change its appearance/behaviour to our needs?
3. If not, what will the custom control look like?
4. How can we make it accessible?
5. Does it behave differently on different platforms?
5. How does it validate?

## Things to make sure our control does

1. It properly propagates changes to the DOM/View
2. It properly progagates changes to the model
3. It comes with custom validation if needed
4. It adds validity state to the DOM so it can be styled
5. It is accessible
6. It works with template-driven forms
7. It works with model-driven forms
8. It needs to be responsive

## ControlValueAccessor

Defined in @angular/forms

A ControlValueAccessor is an interface that takes care of:
1. Writing a value from the form model into the view DOM
2. Informing other form directives and controls when the view/DOM
   changes
   
There is a ControlValueAccessor for every input type that knows how to
update its view.

The *DefaultValueAccessor* is for text inputs and textareas, and there
are many more.

*ControlValueAccessor Definition*
``` TypeScript
export interface ControlValueAccessor {
	
	//Writes a new value from the form model into the view
	writeValue(obj: any) : void
	
	//Registers a handler that should be called when something in the
	//view has changed
	registerOnChange(fn: any) : void
	
	//Used to register handler for touch events (e.g. when an input
	//element blurs)
	registerOnTouched(fn: any) : void
}
```

## Registering our ControlValueAccessor

``` TypeScript
import { Component, Input, forwardRef } from '@angular/core';
import { ControlValueAccessor, NG_VALUE_ACCESSOR } from '@angular/forms';

@Component({
  ...
  providers: [
    { 
      provide: NG_VALUE_ACCESSOR,
      useExisting: forwardRef(() => CounterInputComponent),
      multi: true
    }
  ]
})
class CounterInputComponent {
  ...
}
```

## Validation for the ControlValueAccessor

``` TypeScript
import { NG_VALIDATORS, FormControl } from '@angular/forms';

@Cmponent({
  ...
  providers: [
    { 
      provide: NG_VALIDATORS,
      useValue: (c: FormControl) => {
        let err = {
          rangeError: {
            given: c.value,
            max: 10,
            min: 0
          }
        };

        return (c.value > 10 || c.value < 0) ? err : null;
      },
      multi: true
    }
  ]
})
class CounterInputComponent implements ControlValueAccessor {
  ...
}
```

# Zones and RxJS

## Zones
a *zone* is a global object that intercepts and keeps track of
asynchronous work. angular uses zone.js for it's implementation of
this concept but customizes it with *ngzone*.

Zones have the following responsibilities:
1. Intercept asynchronous task scheduling.
2. Wrap callbacks for error-handling and zone tracking across async
   operations.
3. Provide a way to attach data to zones.
4. Provide a context specific last from error handling.
5. Intercept blocking methods.

An application is a tree of components.
Each component has its own change detector.
=> An application is a tree of change detectors.

Change detection always begins at the root component and then its
children. When changes of input properties in a child component are
detected, an event is caused.


```
import {OnChanges} from `@angular/core`;

@Component({...})
class MyComponent implements OnChanges {
	@Input() prop;
	
	ngOnChanges(changes: {[propName: string]: SimpleChange}) {
		let newValue = changes['prop'].currentValue;
	}
}
```

**Very Important**
ngOnChanges is called only when its property is changed by its
parent. So, you must *never* modify any input properties in your own
component. You should access those as read-only.


## OnPush Strategy
Setting the value *changeDetection* in the component initialization
object to *ChangeDetectionStrategy.OnPush* will cause events raised by
the parent to stop bubbling up to children. This will optimize event
handling in situations where a change is broadcast from the root
module but change detection isn't needed for children of a component.

Note that changes only trigger change detection when the original
value is not equal to the new value. For references, this means that
you must create a new object because *change detection is looking for
updates to the reference value itself*, not that which is referenced.


## Using Observable with ChangeDetectorRef
ChangeDetectorRef is a reference to the component's change
detector. Obtain a reference by importing it from core and injecting
it into the component's constructor.
```
import { ChangeDetectorRef } from '@angular/core';

@Component({})
class MyComponent {
	constructor(private cdRef: ChangeDetectorRef) {}
}
```

markForCheck() is the most useful method of ChangeDetectorRef. It
marks a component to be checked, allowing you to manually trigger
change detection when changes are not picked up due to changes
occurring from the parent. You can call detach() and reattach() to
turn change detection on or off for a component as well.


## Creating Zones
Zones are created by forking a preexisting zone.
```
let rootZone = Zone.current;
let zoneA = rootZone.fork({name: 'zoneA'});
```

To execute code in a zone, use the run method.
```
zoneA.run(function() {
	//Do stuff here
});
```
Child zones, those forked from a parent, have a reference back to the
parent zone.
```
zoneA.parent === rootZone
```

## Stack Frames
A given stack frame can only be associated with one zone. When
asynchronous work is scheduled within a zone's run function, that work
will execute in that zone.
```
zoneA.run(function() {
	setTimeout(function() {
		expect(Zone.current).toEqual(zoneA);
	}, 0);
});
```

## Context Propagation
You can add and retrieve data to/from a zone thusly:
```
let zoneA = rootZone.fork({name: 'zoneA', properties: {a: 1, b:1}});
let zone - zoneA.fork({name: 'zoneB', properties: {a:2}});

expect(zoneA.get('a')).toEqual(1);
expect(zoneB.get('a')).toEqual(2);
```
	
*Important*: Child zones inherit parent zone properties. Data attached
to a zone can't be change once the zone is forked.


## Interception
The benefits of zones are:
1. Composability with parent zones
2. Observability of task execution
3. Centralized error handling



