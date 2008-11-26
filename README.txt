=== Use Google Libraries ===
Contributors: jczorkmid
Donate link: http://jasonpenney.net/donate
Tags: javascript, performance, CDN, Google, jQuery, Prototype, MooTools, Dojo
Requires at least: 2.6
Tested up to: 2.7b3
Stable tag: 1.0

Allows your site to use common javascript libraries from Google's AJAX 
Libraries CDN, rather than from Wordpress's own copies.

== Description ==

A number of the javascript libraries distributed with Wordpress are also 
hosted on Google's [AJAX Libraries API](http://code.google.com/apis/ajaxlibs/).
This plugin allows your Wordpress site to use the content distribution 
network side of Google's AJAX Library API, rather than serving these files from your Wordpress install directly.

This provides numerous potential performance benefits:

* increases the chance that a user already has these files cached
* takes load off your server
* uses compressed versions of the libraries (where available)
* Google's servers are set up to negotiate HTTP compression with the requesting browser

= Supported Libraries and Components =

* [Dojo](http://dojotoolkit.org/)
* [jQuery](http://jquery.com/)
* [jQuery UI](http://ui.jquery.com/)
* [MooTools](http://mootools.net/)
* [Prototype](http://www.prototypejs.org/)
* [script.aculo.us](http://script.aculo.us/)

== Installation ==

# Upload the `use-google-libraries` folder to the `/wp-content/plugins/` folder.
# Activate **Use Google Libraries** through the 'Plugins' menu in WordPress.
# Er... That's it really.

== Frequently Asked Questions ==

= What happens when Google updates their library versions? =

Google has stated that they intend to keep every file they've hosted 
available indefinitely, so you shouldn't need to worry about them 
disappearing.  

This plugin loads scripts using only their major and minor versions, so if 
WordPress asks for jQuery 2.6.3, the plugin will load the latest 2.6.x 
available on Googles servers.  

== Technical Details ==

**Use Google Libraries** uses the following hooks (each with a priority of 1000).

= wp_default_scripts =

**Use Google Libraries** compares it's list of supported scripts to those 
registered, and replaces the standard registrations `src` with ones that 
point to Google's servers.  Other attributes (like dependencies) are left 
intact.

= print_scripts_array =

If jQuery is enqued **Use Google Libraries** will inject a small javascript file 
to ensure that it is running in 
[noConflict mode](http://docs.jquery.com/Core/jQuery.noConflict) as it would 
with the standard WordPress version.

= script_loader_src =

**Use Google Libraries** removes the `ver=x.y.z` query string from the URL
used to load the requested library *if* it is going to load the library from
`ajax.googleapis.com`.  Otherwise the URL is left unaltered.  This both 
improves the chances of the given URL already being cached, and prevents 
**script.aculo.us** from including scripts multiple times.


== References ==

Parts of this plugin (specificly, the dropping of the micro number) were 
inspired by John Blackbourn's 
**[Google AJAX Libraries](http://lud.icro.us/wordpress-plugin-google-ajax-libraries/)**, 
which has very similar goals to this plugin.

