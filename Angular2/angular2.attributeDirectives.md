# Attribute Directives

```
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

```
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


