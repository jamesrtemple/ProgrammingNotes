# Forms

## There are 2 paradigms for form creating on ng2
1. Template-driven forms
2. Reactive forms


## Steps to create a form
1. *Create the model class*  
   This should be a simple POJSO with fields to hold form data.
2. *Create the component that controls the form*  
   Imports and uses the model class from step 1.
3. *Add the FormsModule and our new component from step 2 to the
   application module*
   FormsModule is defined in @angular/forms and is included in the
   imports array.
   The component from step 2 is included in the declarations array.
3. *Create a template with the initial form layout*  
4. *Bind data properties to each form input control with ngModel
   two-way data binding syntax.*
5. *Add the name attribute to each form input control.*
6. *Add custom CSS to provide visual feedback*
7. *Show and hide validation error messages*
8. *Handle form submission with ngSubmit.*
9. *Disable the form submit button until the form is valid.*


## Review Template Reference Variables


Note the use of name and ngModel in the input tag below. Both are
necessary in order for the ng form to know about and monitor the input
field state. Also note that novalidate should be set on the form tag.

```
<form #form="ngForm" novalidate>
	<input type="text" placeholder="Name" name="name" ngModel>
	<button type="submit">OK</button>
</form>
```

## CSS Validation Classes
ng-touched, ng-untouched
ng-pristine, ng-dirty
ng-valid, ng-invalid
