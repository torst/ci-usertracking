## Basic Usage ##

After installing, you can track any pageview into the usertracking table by inserting the following two lines of code into any controller method:

```
$this->load->library('usertracking');
$this->usertracking->track_this();
```

I recommend that you place this code into the constructor of any controller that you would like to track.  This way, all pageviews instantiated by that controller will be tracked.  I also recommend that you enable [autoloading](http://codeigniter.com/user_guide/general/autoloader.html) for the usertracking library.


## Auto-tracking ##

A much more efficient way to use this library is to enable auto-tracking.  This will automatically track pageviews without you having to clutter up your controllers with tracking code.  To enable autotracking, follow these steps:

  1. Ensure that the `$config['enable_hooks] = TRUE;` is indeed set to TRUE in your _application/config/config.php_.
  1. Copy the following code into your _application/config/hooks.php_ file:
```
/* ----------------------------------------------------------------- */
/*
|
| Added as part of the usertracking library by Casey McLaughlin. Please ensure
| that you have the Usertracking.php file installed in your application/library folder!
*/
$hook['post_controller_constructor'][] = array('class' => 'Usertracking',
'function' => 'auto_track',
'filename' => 'Usertracking.php',
'filepath' => 'libraries');
```
  1. Set `$config['usertracking']['auto_track']` to `TRUE` in the _application/config/usertracking\_config.php_ file.


## Tracking by User IDs ##

You can assign a unique user identifier to each usertracking record from your own authentication/user management system.  This allows you to track user across multiple visits, which can be extremely useful for security/behavioral tracking purposes.

To enable user tracking by User ID, oepn the _application/config/usertracking\_config.php_ file and find the line:
```
$config['usertracking']['user_identifier'] = NULL;
```

You are going to tell the Usertracking library what already-existing function in your code returns a unique ID for the currently logged-in user.  If you use an authentication system, you probably have a function that does this already.

The function can be in a library, model, or helper, and there is only one real requirement: it must return a value that can be inserted into a varchar(255) database field whether a user is logged-in or not.

```
$config['usertracking']['user_identifier'] = array($classType, //required -- enter "model", "helper", or "library"
    $className, //required -- the model, class, or helper name (e.g. site_helper.php would be 'site')
    $functionName, //required -- the function that actually returns the value
    $arguments); //optional -- an array containing any arguments to send to the function
```

**Example:** To use a model with a classname of “Users\_model” and a function named “get\_user\_info” that accepts an arugment named “fieldname”, you would use the following syntax:

```
$config['userTracking']['user_identifier'] = array('model', 'users_model', 'get_user_info', array('id));
```