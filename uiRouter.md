UI-ROUTER in Angular 1.x
======================================================================


8 Steps for Simple Routing
----------------------------------------------------------------------
1. Run ```npm install --save @uirouter/angularjs``` to install the library.

2. Include the following scripts:
```
<script src="lib/angular.js"></script>
<script src="lib/angular-ui-router.js"></script>
```
You must load angular before loading the ui-router

3. Inject the ui-router into your module
```
var myApp = angular.module('blah', ['ui.router']);
```

4. Create a state
```
var blah = {
    name: 'bob',
    url: '/bob',
    template: '<h3>Hi Bob</h3>'
}
```

5. Register the state(s) with $stateProvider in an angular config block
```
myApp.config(function($stateProvider) {
    ...//state definition from step 4
    
    $stateProvider.state(blah);
});
```

6. Add a <ui-view> tag to the html to be the router target.
```
<body>
  <ui-view></ui-view>
</body>
```

7. Add some ui-sref links to activate the state when clicked
```
<a ui-sref="bob" ui-sref-active="active">Bob</a>
```

8. Define .active class for active links
```
.active { color: red; font-weight: bolder; }
```



Level 2 Routing
----------------------------------------------------------------------

### Routing to a Component
This one is easy-peasy. Just set the component property of your state definition object to the component you want to render in the router's <ui-view>.
```
var blah = {
  name: 'blah',
  url: '/blah',
  component: 'blahComponent'
}
```

### Resolving data with the Resolve Block
To fetch data from an api when the application state changes, use a resolve block. It matches the results of a function (use promises) to a key, and then binds the results to the component.
```
var blahState = {
  name: 'blah',
  url: '/blah',
  component: '/blahComponent',
  resolve: {
    awesomeMessages: function(MessageService) {
      return MessageService.getAwesomeQuotes();
    }
  }
}
```

and then...

```
angular.module('sayings').component('quotes, {
    bindings: { awesomeMessages: '<' },
    template: '<ul>' +
              '  <li ng-repeat="quote in $ctrl.quotes"> +
              '    {{quote.text}}' +
              '  </li>' +
              '</ul>'
})
```

### State Parameters
State parameters are the ui-router term for path variables. Note the use of the transition object to access them in the resolve function. It is auto-magically injected into the resolve function for you.
```
{
    name: 'person',
    url: '/people/{personID},
    component: 'person',
    resolve: {
      person: function(PeopleService, $transition$) {
        return PeopleService,getPerson($transition$.params().personId);
      }
    }
}
```

### Linking with Parameters with ui-sref
You might need to create links to each item in a collection using ui-sref. This example demonstrates that technique. Note the parenthesis after the target scope.

```
<li ng-repeat="person in $ctrl.people">
  <a ui-sref="person({ personId: person.id })">
    {{person.name}}
  </a>
</li>
```
