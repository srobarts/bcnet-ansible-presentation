## WP-CLI

### Basic Commands

**Get current Wordpress version:**
```
wp core version
```
Output:
```
WordPress version: 4.9.2
```
**Get list of sites in multisite installation:**
```
wp site list
```
Output:
```
+---------+------------------------------------------------+---------------------+---------------------+
| blog_id | url                                            | last_updated        | registered          |
+---------+------------------------------------------------+---------------------+---------------------+
| 1       | http://eportfoliostest.capilanou.ca/           | 0000-00-00 00:00:00 | 2018-03-02 23:54:10 |
| 4       | http://eportfoliostest.capilanou.ca/scotttest/ | 2018-03-03 00:49:40 | 2018-03-03 00:05:06 |
+---------+------------------------------------------------+---------------------+---------------------+
```

**Get list of all active themes:**
```
wp theme list --status=inactive
```
Output:
```
+---------------+----------+--------+---------+---------+
| name          | status   | update | version | enabled |
+---------------+----------+--------+---------+---------+
| twentyfifteen | inactive | none   | 1.9     | no      |
| twentysixteen | inactive | none   | 1.4     | no      |
+---------------+----------+--------+---------+---------+
```

**Get a list of active plugins:**
```
wp plugin list --status=active
```
Output:
```
+----------------+----------------+--------+---------+
| name           | status         | update | version |
+----------------+----------------+--------+---------+
| akismet        | active         | none   | 4.0.3   |
| user-switching | active-network | none   | 1.3.0   |
+----------------+----------------+--------+---------+
```

### Install a plugin
```
 wp plugin install user-switching --activate
```
Output:
```
Installing User Switching (1.3.0)
Downloading installation package from https://downloads.wordpress.org/plugin/user-switching.1.3.0.zip...
Unpacking the package...
Installing the plugin...
Plugin installed successfully.
Activating 'user-switching'...
Plugin 'user-switching' network activated.
Success: Installed 1 of 1 plugins.
```

If you can find the plugin in this list:

http://svn.wp-plugins.org/

Then you can install it using the above method. Just get the exact name of the plugin, and WP-CLI will take care of the rest.

Un-install a plugin:
```
wp plugin uninstall hello
```
Output:
```
Uninstalled and deleted 'hello' plugin.
Success: Uninstalled 1 of 1 plugins.
```

### Install a Theme
```
wp theme install cubic --activate
```
The output will be similar to the plugin install.

Like with the plugins, if you can find a theme in the below list, you can install the theme with this method.

https://wpcom-themes.svn.automattic.com/

### Installing themes and plugins from zip with WP-CLI



## Demonstration

Use https://eportfoliostest.capilanou.ca


Plugin install example:
```
wp plugin install contact-form-7 --activate
```
Theme install example
```
wp theme install davis --activate
```
Check for a Wordpress update
```
 wp core check-update
```
Update Wordpress
```
wp core update
```