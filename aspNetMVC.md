ASP.Net MVC
=======================

Routing
----------

### Core Routing

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


### Attribute Based Routing

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

### Commonly Used Context Objects and Properties
Request.QueryString
Request.Form
Request.Cookies
Request.HttpMethod
Request.Headers
Request.Url
Request.UserHostAddress
RouteData.Route
RouteData.Values
HttpContect.Application
HttpContext.Cache
HttpContext.Items
HttpContext.Session
User
TempData

### Action Method Parameters
MVC will search through **value providers** and **model binders** for
keys that match provided parameter names. If a match is found it will
pass the associated value in for that parameter.

The list includes: *Request.Form*, *Request.QueryString*, *Request.Files*
and *RouteData.Values*.

**Caution**
If a parameter name is matched but can't be converted to the required
type, .Net will instead use the default value! This could be a little
dangerous! You need to check the ModelState's validation errors to
detect that this happened.

### Action Results
The base class `ActionResult` implements the command pattern to
respond to requests. You can implement your own derivation or just use
the built in implementations.


You can instantiate a sub-class of ActionResult to return, or you can
use one of the controller's helper methods to do it for you.
| ActionResult           | Helper Method                 | Description            |
|------------------------|-------------------------------|------------------------|
| ViewResult             | View                          |                        |
| PartialViewResult      | PartialView                   |                        |
| RedirectToRouteResult  | RedirectToAction, etc...      |                        |
| RedirectResult         | Redirect or RedirectPermanent |                        |
| ContentResult          | Content                       | For plain text         |
| FileResult             | File                          | Really any binary data |
| JsonResult             | Json                          |                        |
| JavaScriptResult       | JavaScript                    |                        |
| HttpUnauthorizedResult | --                            |                        |
| HttpNotFoundResult     | HttpNotFound                  |                        |
| HttpStatusCodeResult   | --                            |                        |
| EmptyResult            | --                            |                        |


### Passing a Model to the View
Easy peasy!!!

    `return View(modelObject);` and `@model ModelObjectType`
    
You could also use the ViewBag, but why?


### Doing a Redirect
Several ways and helper methods associated with this, depending on the
level of control you need.

**Redirect** is the simplest, taking a simple url.
**RedirectToRoute** gives you more control and takes an object with a
controller, action and parameters.
**RedirectToAction** is a simpler version of the above that doesn't
require you to new up a configuration object.

To save data in a POST method to be read in a GET after a redirect,
put it in the **TempData** dictionary. It will be available in the GET
and deleted after it is read. TempData also has a Peek and Keep
function to help control when data is marked for deletion.

Layouts
----------
