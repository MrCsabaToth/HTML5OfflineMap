# [Off-line Google Maps concept]

This concept is developed throughout a night at the Googel Campus in Mountain View.
On the night of Oct 20 to Oct 21, 2012. It was the Google DevFest West event.

## The original problem
* Scientist go out to remote field trips where there's no internet
* Their tablet device may have GPS though
* They want to download some image tiles about certain areas therefore
* They could use those off-line images on the field
* I wanted to create something multi-platform, not ruling out any iOS or Android or other device

## Imagined workflow
* During load GPS position can be sensed and the map can automatically focuses there
* The scientist double clicks at the designated area, one pin is dropped there and GPS coordinates are loaded
* Scientist clicks on "Store tiles" button -> image tiles should be stored for that area
* When the scientist clicks "Offline mode" checkbox, the application displays the downloaded tiles

## Challenges
* How to download data and from where?
* Where and how to store them platform independently?
* How to display them?

## This particular solution features
* Based on [HTML5 Boilerplate](http://html5boilerplate.com)
* I used Aptana Studio 3 for HTML5/CSS/JS editing (I tried Eclipse and Netbeans and both sucked at JavaScript)
* HTML5/CSS3/JavaScript _theoretically_ provides platform independence
* IndexDB is used for storage of image tiles
* IDBStore wrapper JS library is used to make that less cumbersome
* jQuery UI Map is used as an extra layer over Google Maps v3 API
* Google static maps used for downloading image tiles
* Google Maps overlay layer for displaying the off-line tiles
* There is underscore.js and bakcbone.js included too, but I didn't have time to implement real UI because of the quirks (ecplained later)

## Implementation limitations, experiences
* Tried Firefox and Chrome, and developed under 12.04 Ubuntu desktop OS
* The IndexDB was very unreliable. Just try the IDBStore.js basic test! If the browser (both browsers) has good mood it works, if not then it doesn't...
* The Google tatic map doesn't work reliably.
** Chrome explicitely denies to download saying origin of reference error
** Firefox sometimes work, sometimes (mostly?) not
** Only try to download the default 256x256px dimesnions otherwise 100% Google won't reply
** Different zoom levels, and the two scale levels (1 and 2) works also
* Since the two basic functionality didn't work (took most of my night), I used a pre-staged situation at the demo:
** I manually downloaded tiles for a specific location
** I didn't store them in IndexDB but loaded them from the image/precache folder
* I only stored photos for one zoom level
* I only stored one tile per spot (in a real life app I'd store a whole area around a spot and several zoom levels)
* I managed to get Google Maps overlay layer to work

## Missing features
* Store bigger area and more zoom levels
* Get non-working parts to work
** For the static map we'd need to modify the AJAX request's Referer and Origin HTTP headers but at this level that doesn't seem to be possible
** For IndexDB some magic needed also
* Storing tiles for more spots, displaying a list of those spots for the user and he/she can slect from them

## Implementation alternatives
* Use File Storage for tile storage, but that's only available in Chrome/Chromium right now
* Use other technology stack than HTML5/CSS/JS
* Use some satellite image providers, is there any free available?

## Plans
* Use Triple play (GWT, PlayN based) framework to develop an alternative
