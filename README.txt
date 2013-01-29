SearchAPI Solr Multiple View Mode Support
=========================================

This README assumes you have SearchAPI and SearchAPI Solr up and running. If not,
refer to their respective documentation to get going.

Configuration
=============

To enable the new fields returned from Solr, you need to first edit each Search server
in SearchAPI config and check off "Retrieve result data from Solr".

There is very little to configuring this module. Enabling it will add a new data
alteration callback in an index called "Multiple entity views". Select all the
view modes in its option list for the indexed entity. When processing the data,
SearchAPI will render the entity item in each view mode, storing the HTML content in
Solr.

The advantage to this is that you can bypass hooking, loading, and rendering entities
for data because you know they are already cached/stored in Solr. A good example of this
would be a search form with search presentation(s) or entities rendered in sidebars,
footers, or mobile devices.

Using this module in conjunction with Entity View Modes is highly suggested.

How to Use
==========

In your code, when dealing with a Solr response, there should be new fields returned. Each
field will be called "search_api_viewed_" with the view mode name affixed to the end.

For example, if you indexed Full, Search, List, and Mobile, you should see these in the
Solr response:

 - search_api_viewed_full
 - search_api_viewed_search
 - search_api_viewed_list
 - search_api_viewed_mobile

Caveats
=======

Right now there is no support for templates spread across multiple themes. If you have
a theme for a mobile site, for example, but the main site theme is something else, then
any custom template (.tpl) files dealing with entity renderings need to reside in the main
theme as well. SearchAPI is going to look for these tpl's here when it is processing the data.