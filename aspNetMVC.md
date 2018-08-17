ASP.Net MVC
=======================

Routing
----------
Configure routing in the class RouteConfig public static RegisterRoutes method.

```
routes.MapRoute(
    name: "Default",
    url: "{controller}/{action}/{id}",
    defaults: new { controller = "Home", 
                    action = "Index", 
                    id = UrlParameter.Optional }  //Note the optional spec
);

routes.MapRoute("MyRoute", "{controller}/{action}");
```

The second call sets up matches to /ControllerName/ActionName. Any URL
in the form /X/Y will attempt to find a controller named X with action
Y to handle the request. It won't match '/' or '/X', as defaults are
not specified, but the first call would match both of those patterns.

The *controller* and *action* segment variables above are reserved
segment names. Additional segment variables are available by calling
`RouteData.Values["segmentName"]` in the controller, or by specifying
a method parameter with the segment name in the controller method.

```
public ActionResult MyController(string id) {...}
```


### Route Constraints
**I'm not getting this from the book. Look up online***


### Attribute Routing
`[Route("RouteName")]` is an option too. Just place that above an
action method to have it handle /RouteName.

Use RoutePrefix to handle routes like /X/Y
```
[RoutePrefix("X")]
public class XController : Controller {
    [Route("Y/{user}/{password}")]
    public ActionResult Z(string user, string password) {
        return View();
    }
}
```


Controllers
---------------
The following controller handles requests for '/' and '/Page2', return
views named by convention from the project Views folder. You can pass
a model and/or view name into View().
```
using System.Web.Mvc;

public class NameController : Controller {
    public ActionResult Index() {
        return View();
    }
    
    public ActionResult Page2() {
        Page2Model p2m = new Page2Model();
        return View(p2m);
    }
}
```


Layouts
----------
