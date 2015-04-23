If you want this library to enter data into the database only under certain conditions, you can add filters.  For example: say you want to track user pageviews only for logged-in users.  You would use a filter to indicate that only logged-in users should be tracked.

Use the following syntax in the _application/config/usertracking\_config.php_ file to define filters:

```
$config['userTracking']['tracking_filter'][] = array($classType, //required -- enter "model", "helper", or "library"
    $className, //required -- the model, class, or helper name (e.g. site_helper.php would be 'site')
    $functionName, //required -- the function that actually returns the value
    $expectedResult, //required -- value that the function should return
    $arguments); //optional -- an array containing any arguments to send to the function
```

You can define as many filters as you like. By defualt, “OR” logic will be applied to the filters. You can change this by setting the line in the _application/config/usertracking\_config.php_ file:

```
$config['usertracking']['tracking_filter_logic'] = "AND"; //or "OR"
```

**Example:** If you have a function named “is\_logged\_in()” in one of your helpers that returns TRUE if the current user is logged in, then you would add a filter as such:

```
$config['userTracking']['tracking_filter'][] = array("helper", "authentication_helper", "is_logged_in", TRUE);
```