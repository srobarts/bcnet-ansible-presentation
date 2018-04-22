## Templates

Ansible uses the Jinja2 templating engine to allow users to create templates, for use in playbooks.

For example, here is a template for a Wordpress wp-config.php file.

(I have truncated this down to show functionality. Some stuff is missing).
```
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', '{{ wp_db_name }}');

/** MySQL database username */
define('DB_USER', '{{ wp_db_user }}');

/** MySQL database password */
define('DB_PASSWORD', '{{ wp_db_password }}');

/** MySQL hostname */;
define('DB_HOST', '{{ wp_db_host }}');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');

/** Disable automatic updating **/
define( 'AUTOMATIC_UPDATER_DISABLED', {{ auto_up_disable }} );

/** Define automatic updates for components **/
define( 'WP_AUTO_UPDATE_CORE', {{ core_update_level }} );

/* That's all, stop editing! Happy blogging. */

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
	define('ABSPATH', dirname(__FILE__) . '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH . 'wp-settings.php');
```
As can be seen, variables are being used to replace values.

This template can then be used for writing the wp-config.php file in the playbook.  This is illustrated in this section from the playbook:
```
- name: Copy Wordpress config file from template
  template: src=wp-config.php dest=/var/www/html/
```
The variables (the parts within the {{ }} brackets) will be replaced by values defined in the vars folder.