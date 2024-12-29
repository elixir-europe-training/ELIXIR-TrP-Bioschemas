
# What is a sitemap and how to create one?

[add-bioschemas file='docs/training-material.yaml']

![sitemap by Vectorjuice on freepick.com](../assets/images/sitemap_byVectorjuice_freepick.png){align=left}

A sitemap tells search engines which pages and files you think are important in your site, and also provides valuable information about these files. For example, when the page was last updated and any alternate language versions of the page.

You can use a sitemap to provide information about specific types of content on your pages, including video, image, and news content. in order to keep the information in a logical and machine readable format the Sitemap usually has a hierarchical structure, this way you could include information on each type of entry, for example:

- Video entry: can specify the video running time, rating, and age-appropriateness rating.

- Image entry: can include the location of the images included in a page.

- News entry: can include the article title and publication date.

In the XML example below you can see the main URL (urlset), the child entry (loc), info about when it was last modified (lastmod), and the changing frequency (changefreq).

```xml
<?xml version="1.0" encoding="UTF-8"?>

<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">

   <url>
      <loc>http://www.example.com/</loc>
      <lastmod>2005-01-01</lastmod>
      <changefreq>monthly</changefreq>
   </url>
</urlset>
```

you can see more detail about the tags you can use in [sitemaps.org](https://www.sitemaps.org/protocol.html)

But this one example of the XML structure of a sitemap and what kind of information you can have linked. You can, but you shouldn't create a sitemap manually. Some resources can generate it automatically it for you.

## Do I need a sitemap?

If your site's pages are properly linked, search engines can usually discover most of your site. Proper linking means that all pages that you deem important can be reached through some form of navigation, be that your site's menu or links that you placed on pages. Even so, a sitemap can improve the crawling of larger or more complex sites, or more specialized files.

A sitemap helps search engines discover URLs on your site, but it doesn't guarantee that all the items in your sitemap will be crawled and indexed. However, in most cases, your site will benefit from having a sitemap!

***You might need a sitemap if:***

- <u>Your site is large</u>:

Generally, on large sites it's more difficult to make sure that every page is linked by at least one other page on the site. As a result, it's more likely Googlebot might not discover some of your new pages.

- <u>Your site is new and has few external links to it</u>:

Googlebot and other web crawlers crawl the web by following links from one page to another. As a result, Googlebot might not discover your pages if no other sites link to them.

- <u>Your site has a lot of rich media content (video, images) or is shown in Google News</u>:

Google can take additional information from sitemaps into account for Search.

***You might not need a sitemap if:***

 - <u>Your site is "small"</u>:
 
 By small, we mean about 500 pages or fewer on your site. Only pages that you think need to be in search results count toward this total.

- <u>Your site is comprehensively linked internally</u>:

This means that Googlebot can find all the important pages on your site by following links starting from the home page.

- <u>You don't have many media files (video, image) or news pages that you want to show in search results</u>:

Sitemaps can help Google and other search engines to find and understand video and image files, or news articles, on your site. If you don't need these results to appear in Search you might not need a sitemap. However, for training material that is maintained online, considering the FAIR principles we strongly advise the implementation of a sitemap and Bioschemas.

## How can I build a sitemap?

Check https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap and https://www.sitemaps.org/protocol.html on methods how to easily create a sitemap for your content.

If you use WordPress, we recommend to the use the RankMath plugin since it also provides the feature of [adding a sitemap](https://rankmath.com/kb/html-sitemap/) to your WordPress website.

## Register the sitemap in TeSS for automated ingestion of your training material

In order to increase the findability even more, we strongly recommend to register the sitemap in TeSS. Please follow the [documentation](https://tess.elixir-europe.org/about/registering#automatic) on the TeSS web site or this [ELIXIR tutorial](https://elixir-europe-training.github.io/ELIXIR-TrP-TeSS/chapters/chapter_04/).

