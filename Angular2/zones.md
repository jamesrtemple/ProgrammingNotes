# Zones
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
*ngOnChanges* is called only when its property is changed by its
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



