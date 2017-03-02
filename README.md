ged2site
========

Convert a Gedcom file to HTML to create a family tree website.

This is quite complex software, so if you are a genealogist looking to create
a website and aren't an IT guru, it would be better to e-mail me on `<njh at nigelhorne.com>`.

An example genealogy website that was produced by ged2site is available
at https://genealogy.nigelhorne.com.

It's been tested more extensively with GedComs exported and downloaded from
FindMyPast, Family Tree Maker, though it should work fine with other systems
such as GenesReunited and Ancestry.

Typical usage:

    ged2site -cFdh 'Your Name' gedfile.ged

You will then have two sites created in sub directories
- static-site is static HTML,
- dynamic-site is a [VWF](//github.com/nigelhorne/vwf) based website which uses templates to support more than one
language and present different content to mobile/web/search-engine clients.

If you decide to use the static site, just copy files in the static-site directory to your webserver.
If you decide to use the dynamic site first create a $hostname.com file in the
conf directory (use example.com as a template),
then modify the contents of the template tree so that the site looks as you
want it.
The configration file can be in any number of formats including INI and XML.
Then upload the dynamic-site directory to your webserver.

The options are:

| Flag | Meaning |
| ---- | ------- |
| -c   | Give citations |
| -d   | Download copies of objects and media and include them on the generated website rather than link to them, useful if the objects are on pay sites such as FMP |
| -f   | treat warnings as fatals, implies -w |
| -F   | print a family tree (requires GraphViz) |
| -g   | Generate Google verification file - see www.google.com/webmasters/verification Don't include the .html at the end of the code |
| -h   | set the home person |
| -l   | include living people |
| -m   | Generate a Google map on each page showing events |
| -J   | Google Maps JavaScript API key (used to display the map) |
| -G   | Google Maps geolocation API key (used to populate the map) |
| -w   | print warning about inconsistent data - a sort of lint for Gedcom files, may not do as many as *[gedcal](//github.com/nigelhorne/gedcal)* |

If gedcal is installed, ged2site will also create a calendar of births and
deaths, one page for each month in the current year.

Some of the options can be stored in *ged2site.conf*:

| Flag | Meaning |
| ---- | ------- |
| -h   |  home |
| -g   |  google_verification |
| -G   |  google_maps_geolocation_key (also can be stored in the `GMAP_KEY` environment variable) |
| -J   |  google_maps_javascript_key |

Ancestry on Windows
===================

I use FindMyPast on Linux, because export of images is better on FMP and
because Linux.  I recognise that many folks use Ancestry on Windows, so I
have this rough guide which works for me, but understand that you'll still
need to be an advanced Windows user, this is not for the Novice.

* Firstly install a Perl, either ActiveState or Strawberry will work fine. I
have also had success using Cygwin's Perl.

* Load in all the CPAN modules that ged2site uses.

* Install Family Tree Maker.  Sorry, there's no alternative, you'll just have
to find a copy and buy it.  Good luck because ACOM is dropping it, and I'm
yet to play with its successor.

* Sync your ACOM tree to FTM, ensuring you also sync all of the media.

* Create a Gedcom using File->Export, and choosing GEDCOM5.5 as the
output format.

* Run ged2site on that saved Gedcom file.

* -F may not work because it depends on Graphviz being found,
but could work under Cygwin. On the otherhand, I've been hit by a Cygwin bug
when trying to call Graphviz from ged2site.  This may be because ged2site
pipes output to Graphviz, perhaps it would work if it used a temporary file
as input.

Acknowledgements
================

http://fullcalendar.io for the calendar view

https://github.com/weichie/animated-Timeline for the family history view

Google for the map page

Graphviz for the family tree and Tree::Family from CPAN for the inspiration
	and code to use as a template

So many CPAN modules that if I list them all I'll miss one, but special mention
	goes to the Gedcom module.

# LICENSE AND COPYRIGHT

Copyright 2015-2017 Nigel Horne.

This program is released under the following licence: GPL for personal use on a single computer.
All other users (including Commercial, Charity, Educational, Government)
must apply in writing for a licence for use from Nigel Horne at `<njh at nigelhorne.com>`.
