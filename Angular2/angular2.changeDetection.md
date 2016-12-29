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

*ngOnChanges* is called only when its property is changed by its
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

