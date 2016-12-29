# Components
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
