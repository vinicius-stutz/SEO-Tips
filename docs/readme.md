# SEO Tips

## Set correct META tags: title & description

Setting the correct META tags for title and description is crucial for your site.

    <HTML>
      <title> Mailing List Archive - MARC</title>
      <meta name="description" content="A public mailing list archive for open source projects.">
      ...

Every page should have a unique, clear title with a proper description. This is the entry ticket form the SERPs (Search Engine Result Pages). The title & description should be considered a teaser to lure the user into clicking your link.

## Semantic page markup: h1, h2, h3, ...

Use the HTML elements to your advantage: h1 headers for your most important titles, h2 for the next level titles, h3 for the next ones, and so on. Google parses your content and uses those tags as its guideline.

Semantic markup goes  [a lot further](http://www.socialmediaexaminer.com/semantic-markup/)  than just h1 tags though. If you're an event- or booking-site, you can add structured data to your markup that can be parsed and shown directly into Google's search result pages.

## Eliminate duplicate content (in some unexpected ways)

Google doesn't like it when you have the same content be shown on different pages. You're penalised for it as it's considered  _duplicate content_  and could be seen as a way to artificially increase the size of your site.

But duplicate content is something that's very easy to get, even when you don't promote it. Take for instance the following URLs:

    http://yoursite.tld/page/?search=keyword&page=5&from=homepage
    http://yoursite.tld/page/?page=5&search=keyword&from=homepage
    http://yoursite.tld/search/keyword/?page=5
    ...

Those URLs could all be pointing to the same content: the position of the different URL variables, a clean version of the URL as rewritten by  `.htaccess`  files, ...

For Google, those could look like 3 unique URLs with the same content. That's not good.

These are a lot harder to fix and track down but it should be kept in the back of your mind when developing any new site. If there are multiple URLs to show the same content, either:

-   Set the correct META tags to prevent indexing (`<meta name="robots" content="noindex,follow"/>`)
-   Force a 301 permanent rewrite to the final URL

For websites that offer a search function this can happen quite a lot: different keywords showing the same results and thus the same content. Because of this, many people add the  `noindex,follow`  headers to search result pages to prevent those from being indexed.

**Update:**  as correctly mentioned in the comments, another way to tackle this problem is by creating  [canonical URLs](https://support.google.com/webmasters/answer/139066?hl=en). This allows you to communicate one URL to search engines where multiple variants of that URL may exist.

## Clean URLs

If you remember the early 2000's, you remember URLs like these:

    site.tld/page.php?page_id=512
    site.tld/profile.php?id=12
    site.tld/forumpost.php?thread=66
    ...

These kind of URLs, where the database IDs are so clearly visible, are become more and more rare. Nowadays, you have URLs like these:

    site.tld/9-ways-to-make-money-online
    site.tld/profile/mattias-geniar
    site.tld/forum/thread/how-do-i-undelete-a-file-in-linux
    ...

These URLs have a couple of things in common:

-   The site's information architecture is clearly visible: the URLs show the hierarchy in which content is organised.
-   The URL contains keywords and usually gives away part of the content of the page, without opening the page yet (useful in search engine results to lure the user into clicking your link).

If you still have URLs like the first example, consider creating a clear hierarchy of all your pages and structure them like the 2nd example.

As for the whole "trailing slash or no trailing slash debate": I don't care about that. I don't believe the trailing slash makes any difference from a technical SEO point of view, so pick a style that makes you happy.

## Responsive layouts

Responsive designs are given a higher score for mobile searchers than non-responsive layouts. If your current site isn't made responsive yet, consider making it one of your priorities for the next redesign.

For the mailing list archive I simply relied on  [Twitter Bootstrap](http://getbootstrap.com/), the CSS framework which comes with responsiveness out of the box. One of the key  _technical_  aspects of a responsive layout is the presence of the following meta tag in the HEAD of the HTML.

<meta name="viewport" content="width=device-width, initial-scale=1.0">

Because of Twitter Bootstrap, it was a no-brainer to get a responsive layout. It didn't take me any more work. As a non-webdeveloper, it did take me longer to get used to Bootstrap's grid system and having to test the layout in multiple resolutions, but in the end -- that effort pays of.

## Robots.txt

Search engines will look for a  `robots.txt`  file in the root of your website for instructions on  _how_  and  _if_to crawl your site. The following file allows all indexing to occur, nothing is blocked.

    User-agent: *
    Disallow:

For a couple of live ones, see here:  [google.com/robots.txt](http://www.google.com/robots.txt) and [nucleus.be/robots.txt](https://nucleus.be/robots.txt).

If you don't want search engines to crawl portions of the site, add excludes like this:

    User-agent: *
    Disallow: /search
    Allow: /search/about
    Disallow: /sdch
    Disallow: /groups
    ...

Be warned though: this is a suggestion to search engines. Google will honour it, but there's no guarantee that tomorrows search engines will too.

## Sitemap.xml

A sitemap is a structured set of data (in XML) that lists all the pages of a site and when that particular page was last updated. It's useful to get a comparison between all the pages you have, and the ones that have been indexed.

Example: [cronweekly.com/sitemap_index.xml](https://www.cronweekly.com/sitemap_index.xml): an overview of multiple sitemap files

Most content management systems can generate these for you. If you've written your own code, there are probably community contributed modules that can help generate them.

If you've got a static website, where all files are already generated, you can use a python script to parse those files and generate a sitemap for you.

[This python script can do that for you](http://goog-sitemapgen.sourceforge.net/).

    $ /bin/python sitemap_gen.py --config=config.xml

The config comes included in the download, you probably only need to modify the following parts (leave the original version and just change out these parameters).

    $ cat config.xml
    <site
      base_url="https://www.test.com"
      store_into="/path/to/htdocs/sitemap.xml.gz"
      verbose="0"
    >
    
    <directory
      path="/path/to/htdocs/"
      url="https://www.test.com"
      default_file="index.php"
    />

A very simple config, you tell it which directory to index (`~/htdocs/`), the name of the site and where to output the sitemap file.

Done.

## Google's Webmaster Tools

Every site should be added to  [Google's Webmaster Tools](https://www.google.com/webmasters/tools/home?hl=en).

This tool gives you insights in the crawl status of your site, which problems Google detected when crawling or parsing the site, ...

The webmaster tools also allow you to explicitly add your sitemap.xml and get feedback on which pages have been crawled and which have been added to Google's Index.

Adding the sitemap is no guarantee that Google will crawl and index all sites, but you can clearly see Google's status and difference between what you submitted (the sitemap) and what Google crawled.

## Twitter Cards

_"What does Twitter have to do with SEO?"_

Well, more than you think. Having URLs that reached further trough social media increase the chances to be posted on multiple websites, thus increasing your organic reach and pagerank.

Implementing  [Twitter Cards](https://dev.twitter.com/cards/overview)  doesn't take a lot of effort, but the gains can be substantial.

You essentially add a set of  [additional header tags](https://dev.twitter.com/cards/markup)  which Twitter can parse whenever a link is shared on the network. For  [MARC](https://marc.ttias.be/openssl-announce/2016-03/msg00002.php), it looks like this:

    <meta name="twitter:card" content="summary" />
    <meta name="twitter:title" content="[openssl-announce] OpenSSL Security Advisory" />
    <meta name="twitter:description" content="Public mailing list archive for [openssl-announce] OpenSSL Security Advisory" />
    <meta name="twitter:image" content="https://www.test.com/assets/social_logo.png" />
    <meta name="twitter:creator" content="@mattiasgeniar" />
    <meta name="twitter:site" content="@mattiasgeniar" />

Now whenever a user shares a link to that site, Twitter parses it nicely and presents it in a more clean way. This  _should_  encourage more shares and further reach of your posts.

Which is better than just a post with a link, without additional content.

## Facebook's Open Graph

For the same reason as Twitter Cards, you should implement Facebook's Open Graph. Facebook also offers a  [URL debugger](https://developers.facebook.com/tools/debug/)  to help diagnose problems with those headers.

For MARC, they look like this.

    <meta property="og:url" content="https://www.test.com/openssl-announce/2016-03/msg00002.php" />
    <meta property="og:type" content="article" />
    <meta property="og:title" content="[openssl-announce] OpenSSL Security Advisory" />
    <meta property="og:description" content="Public mailing list archive for [openssl-announce] OpenSSL Security Advisory." />
    <meta property="og:site_name" content="Mailing List Archive (MARC)" />
    <meta property="og:image"  content="https://www.test.com/assets/social_logo.png" />

Use the  [debugger](https://developers.facebook.com/tools/debug/) to parse.

A better view in the timeline will increase the reach of any of your pages.

## HTML meta tags for indexing

Unless a particular page is blocked in the robots.txt, Google will assume the page can be indexed.

You can make this even more clear by adding HTML tags in the head that explicitly tell the search engine to index this page and follow all its pages it links to.

    <meta name="robots" content="index, follow">

Alternatively, if this page shouldn't be indexed (like on duplicate content pages mentioned above) you can prevent it with the  `noindex`  value.

    <meta name="robots" content="noindex, follow">

There are some more  [variations possible](http://www.metatags.info/meta_name_robots)  you could read up on.

## Crawl your site for 404's

Having dead pages or links is something to avoid, but if you have a site that's been alive for a couple of years -- chances are, you'll have 404's in your pages you have no idea about.

Here's a very simple command line script to crawl your site and report any 404 found. Each of these should be checked or redirect to a new page (preferably by a 301 HTTP redirect, indicating a permanent redirect).

    $ wget --spider -r -p http://www.cronweekly.com 2>&1 | grep -B 2 ' 404 '

    --2016-03-09 22:08:14--  https://www.cronweekly.com/three-tiers-package-managers/
    Reusing existing connection to www.cronweekly.com:443.
    HTTP request sent, awaiting response... 404 Not Found

This told me, on my own site, that I linked to a page that wasn't there anymore: it gave a 404 error.

Now I should probably look for where I linked to that page and fix the referer.

## Crawl your site for anything but HTTP 200's

If you crawl your own site, ideally you should find only HTTP/200 responses. An HTTP/200 is an "OK, content is here" message.

Anything else could mean content is missing (404), broken (503) or redirect (301/302). But ideally, you don't link to any of that content but directly to the final destination page.

So here's a small crawler completely crawls your site and stores it in a file called  `~/crawl_results.log`.

    $ wget --spider -r -o ~/crawl_results.log -p http://www.cronweekly.com 2>&1

The result is in the  `~/crawl_results.log`  file:

    $ cat  ~/crawl_results.log

    ...
    --2016-03-09 22:13:16--  https://www.cronweekly.com/
    Reusing existing connection to www.cronweekly.com:443.
    HTTP request sent, awaiting response... 200 OK

    2016-03-09 22:13:16 (114 MB/s) - 'www.cronweekly.com/index.html' saved [17960]

You can now analyse the resulting log file for any HTTP status code that wasn't expected.

## Geolocation of your IP address

If you have a site targeting Belgium, make sure to have the site hosted in Belgium.

The WHOIS data behind IP addresses can specify a location. For Google's "local" results, the location is -- in part -- determined by the IP address that is hosting your site.

So if you went to  [Hetzner](https://www.hetzner.de/en/), a massive German hosting provider, because it was cheap, but your business is aiming at Belgian visitors, you're much better of hosting your site at  [Nucleus, a local Belgian hosting provider](https://www.nucleus.be/en/). If you're targeting Norway, host your site in Norway. etc.

If you're targeting multiple regions, consider a couple of extra technical features:

-   A CDN like CloudFlare, that helps you host your site across the globe by mirroring it
-   Set up your own proxy in multiple languages, and redirect your .NL domains to a proxy in the Netherlands, a .BE domain to your proxy in Belgium, etc.

In short: be where your visitors are. It'll give them lower latency and a faster experience, and Google will keep the location in mind when serving local results.

## Site maintenance: HTTP 503 errors

Whenever you have to take your site offline for a longer period due to maintenance, consider sending out HTTP 503 headers to all pages.

An HTTP 503 header means "Service Unavailable". And that's exactly what happens during maintenance.

Google won't index a 503 and it'll consider it as "temporarily not working", so it can try again later.

You can even redirect your visitors to a page explaining the maintenance, while still serving the HTTP 503 header for all indexing bots. A rewrite rule like this triggers that behaviour.

    RewriteEngine On
    RewriteCond %{SCRIPT_FILENAME} !maintenance.html
    RewriteRule ^.*$ /maintenance.html [R=503,L]
    ErrorDocument 503 /maintenance.html

    # Make sure no one caches this page
    Header Set Cache-Control "max-age=0, no-store"

All traffic gets redirected to  `/maintenance.html`  while keeping a correct HTTP status code.
