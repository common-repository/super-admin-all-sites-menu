=== Super Admin All Sites Menu ===
Stable tag: 1.6.7
Requires at least: 5.6  
Tested up to: 6.4  
Requires PHP: 7.3  
License: GPL v2 or later  
Tags: superadmin, multisite, management  
Contributors: PerS  
Donate link: https://www.paypal.com/paypalme/PerSoderlind

For the super admin, replace WP Admin Bar My Sites menu with an All Sites menu.

== Description ==

* Doesn't use `switch_to_blog()`, i.e. Super Admin All Sites Menu is faster and uses less resources than the WP Admin Bar My Sites menu.
* Subsite menu data are stored locally in IndexedDB (did I say it's fast?). The local storage is updated when;
  * the plugin is activated.
  * a site is added or deleted.
  * you change a blog name.
  * IndexedDB is out of sync with site changes.
  * [Restricted Site Access](https://github.com/10up/restricted-site-access) is activated or deactivated.
* When subsite menu data is updated, AJAX is used and it's done in increments (100 sites per increment).
* List all subsites. WP Admin Bar My Sites only list sites you're a local admin on.
* Mark sites that has [restricted site access](https://github.com/10up/restricted-site-access) with a red icon.
* Sites menu is sorted alphabetically.
* Search filter.
* Add more menu choices:
     * Under "Network Admin"
         * Add New Site
     * Per subsite.
         * 'New Page'
         * 'Users'
         * 'Plugins'
         * 'Settings'

= Prerequisite =

* WordPress Multisite
* A modern browser, IE 11 isn't supported.

= Filters =

You can use the following filters to override the defaults:

* `all_sites_menu_order_by`
  * Sort menu by. Default value is `name`, accepts `id`, `url` or `name`
    `
    add_filter( 'all_sites_menu_order_by', function( string $order_by ) : string {
    	return 'url';
    } );
    `
* `all_sites_menu_load_increments`
  * AJAX load increments. Default value is 100.
    `
    add_filter( 'all_sites_menu_load_increments', function( int $increments ) : int {
  		return 300;
  	} );
  	`
* `all_sites_menu_plugin_trigger`
  * Trigger an update of local storage (IndexedDB) when a plugin is (de)activated. Default is `[ 'restricted-site-access/restricted_site_access.php' ]`.
    > Note: Must be an array and each element in the array must point to the main plugin file. Syntax `'plugin-dir/plugin-file.php'`
  	`
   	add_filter( 'all_sites_menu_plugin_trigger', function( array $plugins ) : array {
  		return [
  			'restricted-site-access/restricted_site_access.php',
  			'myplugin/myplugin.php',
  		];
  	} );
  	`
* `all_sites_menu_search_threshold`
  * Don't display search field if there's less than N subsites. Default value is 20.
  	`
  	add_filter( 'all_sites_menu_search_threshold', function( int $increments ) : int {
  		return 40;
  	} );
  	`
* `all_sites_menu_search_threshold`
  * Don't display search field if there's less than N subsites. Default value is 20.
  	`
  	add_filter( 'all_sites_menu_search_threshold', function( int $increments ) : int {
  		return 40;
  	} );
  	`
* `all_sites_menu_force_refresh_expiration`
  * How often a forced refresh should be taken. Default value is `3600`. Set the value to `0` to disable forced refresh.
  	`
  	add_filter( 'all_sites_menu_force_refresh_expiration', function( int $seconds ) : int {
  		return 3600;
  	} );
  	`

= Development = 

* Active development of this plugin is handled [on GitHub](https://github.com/soderlind/super-admin-all-sites-menu).

== Screenshots ==

1. Demo
2. Menu data are stored locally in IndexedDB.

== Changelog ==

= 1.6.7 =

- Update dependencies

= 1.6.6 =

- Tested with WordPress 6.4

= 1.6.5 =

- Tested with WordPress 6.3

= 1.6.4 =

- Fix bug in handling the REST API.

= 1.6.2 =

- Tested with WordPress 6.0

= 1.6.1 =

* Await for the promise `populateDB()` to resolve before continuing.

= 1.6.0 =

* Use `@wordpress/api-fetch` to fetch subsite data.

= 1.5.0 =

* Use REST instead of AJAX.

= 1.4.28 = 

* Housekeeping

= 1.4.27 =

* Add missing textdomain to translations.
* Update uninstall.php

= 1.4.26 =

* Bundle Dexie using wp-scripts

= 1.4.25 =

* Housekeeping

= 1.4.24 =

* Use @wordpress/i18n to translate JavaScript.

= 1.4.23 =

* Fix typo in textdomain.

= 1.4.22 =

* Housekeeping 

= 1.4.21 =

* Update translation file (.pot)

= 1.4.20 =

* Don't set dependencies for style.

= 1.4.19 =

* Import @wordpress/i18n

= 1.4.18 =

* Replace build script from webpack to wp-scripts (@wordpress/scripts)

= 1.4.17 = 

* Use correct AJAX URL

= 1.4.16 =

* Upgrade Dexie.js to v 3.2.0

= 1.4.15 =

* Only load the plugin code if the admin bar is available.

= 1.4.14 =

* Force refresh using a site transient.

= 1.4.13 =

* Don't list sites that are tagged as archived, deleted, mature or spam.

= 1.4.12 = 

* Update plugin banner

= 1.4.11 =

* Add plugin banner

= 1.4.10 =

- Housekeeping

= 1.4.9 = 

* Deploy to https://wordpress.org/plugins/super-admin-all-sites-menu/

= 1.4.8 =

* Remove external dependencies.

= 1.4.7 =

* Remove `type=module` from script tag. Not needed anymore since the script and modules are packed.

= 1.4.6 =

* Pack JavaScript using webpack.

= 1.4.5 =

* Only run if multisite.
* Improved Dexie versioning.

= 1.4.4 =

* Pass only one parameter to `plugin_update_local_storage()`
* Close db connection when getting version number.

= 1.4.3 =

* IndexedDB maintenance, i.e. remove old databases.

= 1.4.2 =

* Dexie schema change, bump Dexie version number.

= 1.4.1 =

* Make sure the local storage (IndexedDB) is in sync with server changes.

= 1.4.0 =

* Refactored JavaScript again, I'm using this plugin to experiment with and to learn JavaScript better.

= 1.3.8 =

* Refactor and rename db module.

= 1.3.7 =

* Don't display search field if there's less than 20 subsites. The threshold is adjustable using the `all_sites_menu_search_threshold` filter

= 1.3.6 =

* Fix load increments bug.

= 1.3.5 =

* Housekeeping.

= 1.3.4 =

* Add filters to defaults.

= 1.3.3 =

* Update IndexedDB when you change a blog name.

= 1.3.2 =

* Only change `text/javscript`to `module` when tag has `src` attribute

= 1.3.0 =

* Refactor
  * Split JavaScript into modules
  * If empty, populate IndexedDB with sites menu data.

= 1.2.4 =

* Adjust the sites menu wrapper height

= 1.2.3 =

* Remove `window.hoverintent`, it's slow when you have a lot of sites, use `addEventListener` in capturing mode instead.

= 1.2.2 =

* Housekeeping.

= 1.2.1 =

* Update IndexedDB when Restricted Site Access is (de)activated.

= 1.2.0 =

* Store subsite menu data in IndexedDB (local storage).
  * IndexedDB is updated when a site is added / deleted.
* Add search.

= 1.1.2 =

* Fix translations.

= 1.1.1 =

* Housekeeping.

= 1.1.0 =

* Lazy load the subsite menu, using IntersectionObserver and AJAX, loading only 80 subsites at a time.
* Make subsites menu scrollable.

= 1.0.x =

* Initial release.

