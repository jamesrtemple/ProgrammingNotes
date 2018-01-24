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
