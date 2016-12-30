# Input Binding
Pass Data from parent to child with input binding in the component tag.
```
@Input() myvalue: string;
```

# Intercept input property changes with a setter
Pass data from parent to child where operations are required when the
value is explicity set in the component tag.
```
@Input()
set name(name: string) {
	this._name = name.trim();
}
```

# Intercept input property changes with ngOnChanges
In this method, ngOnChanges will be called when/if the parent changes
the value of myvalue.

```
export class MyClass implements OnChanges {
	@Input() myvalue: string;
	
	ngOnChanges(changes: {[propKey: string]: SimpleChange}) {
		//...
	}
}
```

# Parent listens for child event
Use this method to provide standard HTML like events on components.
```
@Output() onVoted = new EventEmitter<boolean>();
//...
this.onVoted.emit(isAgreed);
```


# Parent interacts with a child via a template local variable
Use this method if all access to the child can be done within the
template of the parent.
```
template: `
	<h3>Countdown via local var</h3>
	<button (click)="timer.start()">Start</button>
	<button (click)="timer.stop()">Stop</button>
	<div>{{timer.seconds}}</div>
	<countdown-timer #timer></countdown-timer>
`
```


# Parent calls a ViewChild

```
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


# Parent and children communicate via a service

