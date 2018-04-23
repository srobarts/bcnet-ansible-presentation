## WP-CLI

### Basic Commands

Get current Wordpress version:
```
wp core version
```
Output:
```
WordPress version: 4.9.2
```
Get list of sites in multisite installation:
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

Get list of all active themes:
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
Install a plugin:
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
