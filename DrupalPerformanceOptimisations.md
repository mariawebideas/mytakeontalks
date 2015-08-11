# End-to-End Drupal Performance Optimisations

[Dennis Digital DropIn, London] (http://www.meetup.com/DennisDigitalDropIn/events/223812922/) - 10 August 2015

## Speakers
* Konstantin Kamskov
* David Grayston
* Chris Kinch

## Block Catching
* Use [New Relic](https://newrelic.com) for performance monitoring
* Use the **Performance** page on Drupal (admin/config/development/performance) for the following CATCHING settings:
  * Instead of using **Cache pages for anonymous users** use Varnish - https://www.varnish-cache.org/
  * Tick **Cache blocks**
  * Set **Minimum cache lifetime** to 1 minute
  * Set **Expiration of cached pages** to 1 hour
* Use [Block Cache Audit](https://www.drupal.org/sandbox/PeterC/1836684) sandbox module
* Use [Block Mass Cache](https://www.drupal.org/project/blocks_mass_cache) module. **Important**: In Drupal, blocks are not cached if you are logged in as admin (user id 1), so make sure you test blocks caching with an user different than user 1 or as anonymous.
* Use Drupal API [constant DRUPAL_CACHE_CUSTOM](https://www.drupal.org/project/blocks_mass_cache) for more fine grained catching when needed

## Pagers
* Avoid full pagers if possible
* Use [Views Litepager](https://www.drupal.org/project/views_litepager) module. This module does not have all the features of Drupal full pager but you might find that your customers might be ok with just using the next and previous links which are provided with this module.

## Path Catching
* Use [Path Cache](https://www.drupal.org/project/views_litepager) module if you have replaced your catching backend with memcache

## Forms
* Use [Varnish](https://www.varnish-cache.org/)
* If you use Varnish avoid using form API AJAX for anonymous users. Instead implement a custom solution using hook_menu and javascript
* Offload user generated content to third party providers such as [Disqus](https://disqus.com). Then use the APIs to pull content back to Drupal.

## MySQL
* Select only necessary fields
* Remove unnecessary sorting
* Index custom tables

## Landing Pages
* Remove unnecessary use of pagers
* Limit to a subset of data if soring e.g. past year
* Use a custom module to select page content in a single query that then is broken down on different blocks for display
* If you are using Varnish provide **Save and purge** buttons to editors

## The Need for Speed - Front end Performance
[Slides available](http://slides.com/chriskinch/perf-op#/)

### Fundamentals
* Compress your images, e.g. Photoshop
* Avoid javascript that manipulates the DOM too heavily
* Avoid bloated libraries, this does not include jQuery

### Know your tools
* Use the [Advanced Aggregation](https://www.drupal.org/project/advagg) module
* Use **Grunt** or **Gulp** as task runners
* Use **Google Page Speed Insights** or **ySlow** to find current performance
* Use the good old network inspector

### Less then Obvious
* Use **data URIs** for example to load things like the logo
* Use font and/or svgs for icons, e.g. [Fontello](http://fontello.com)
* Use **WOFF2** as your font format

### Perceived Speed
* Optimise images more:
  * Interlaced or progressive images
  * Use the **Picture and Breakpoints** modules
* Render your resources
  * Use a script loader like [Require.js](http://requirejs.org)
* Critical CSS a.k.a. Prioritising Visible Content
  * Use [CSS Delivery](https://www.drupal.org/project/css_delivery) module and
  * Use [Jacket SASS](https://github.com/at-import/jacket) mixins

## Other
* Check out the **Robots.txt** file - might be blocking pages that Google Analytics needs to access to provide meaningful statistics
* Use lazy loading (no specific modules mentioned) particularly when you have image galleries
* Check whether [Google considers your website to be mobile friendly](https://www.google.co.uk/webmasters/tools/mobile-friendly)
