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
