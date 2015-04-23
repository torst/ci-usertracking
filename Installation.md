# System Requirements #

  * CodeIgniter version 1.6.3 or 1.7.1 or newer _(1.7.0 has a bug that prevents this from working correctly)_
  * PHP v5.1 or newer
  * A database connection already setup in your CodeIgniter application


# Installation Procedure #

  1. Verify that you are running CodeIgniter 1.6.3, 1.7.1, or newer.  You can do this by inserting _echo CI\_VERSION;_ into one of your views.
  1. Download and extract the latest version of UserTracking for CI.
  1. Upload the usertracking.php file to your application/libraries folder.

# Manual Database Setup #

This plugin automatically creates the database table it needs to keep track of users.  However, if you want to set the database table up manually, you can use the following code SQL code:

_note: if you are using a database prefix, append that to the beginning of the table name_

```
CREATE TABLE /*!32312 IF NOT EXISTS*/ "usertracking" (
"id" int(11) NOT NULL AUTO_INCREMENT,
"session_id" varchar(100) DEFAULT NULL,
"user_identifier" varchar(255) DEFAULT NULL,
"request_uri" text,
"timestamp" varchar(20) DEFAULT NULL,
"client_ip" varchar(50) DEFAULT NULL,
"client_user_agent" text,
"referer_page" text,
PRIMARY KEY ("id")) /*!40100 DEFAULT CHARSET=utf8*/;
```

# Usage #

See the usage wiki page for details