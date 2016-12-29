# Notes from Pascal Precht

From his blog post at:
http://blog.thoughtram.io/angular/2016/07/27/custom-form-controls-in-angular-2.html

*Questions to ask before creating a custom control*
1. Is there a native element that has the same semantics?
2. If yes, can we simply rely on that element and use CSS and/or progressive enhancement to change its appearance/behaviour to our needs?
3. If not, what will the custom control look like?
4. How can we make it accessible?
5. Does it behave differently on different platforms?
5. How does it validate?

*Things to make sure our control does*
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
```
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
```
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
```
import { NG_VALIDATORS, FormControl } from '@angular/forms';

@Component({
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


