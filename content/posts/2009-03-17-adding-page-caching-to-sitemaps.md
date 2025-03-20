---
date: '2009-03-17T00:00:00+0000'
title: 'Adding Page Caching to Sitemaps'
tags: ['Web']
aliases: /2009/03/17/adding-page-caching-to-sitemaps/
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: false
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
---

The shortest distance between two points is not a straight line. The shortest distance is zero. Admittedly, we're not about to fold space or do time travel, but you get the idea.

Likewise, for any web framework, the fastest way to deliver content to clients is to not use the framework at all, but let the webserver serve static files to clients.

In Rails this means using page caching and leave the heavy lifting to the webserver. Keeping your cache fresh and still maintaining stellar performance might seem like a daunting task, but Rails gives you quite a bit of help, so it is actually not that hard to do.

In this post I will take you through the steps to add page caching to our Sitemap, that we created in [Creating Sitemaps with Comatose CMS](/blog/2009/03/16/creating-sitemaps-with-comatose-cms.html.)

## Enable page caching for our Sitemap

As you can see below, enabling page caching is as simple as just adding one extra line in a controller

```ruby
## app/controllers/info_controller.rb
class InfoController < ApplicationController
    caches_page :sitemap
    def sitemap
        respond_to do |format|
      format.xml do
                @website_url = 'http://example.com'
                @pages = ComatosePage.find(:all, :conditions => "full_path not like ''")
                render :action => 'sitemap', :layout => false
            end
        end
    end
end
```

### Verify caching

To verify that we are have succesfully enabled page cache, let's update the development environment to mimick the production environment.

```ruby
## config/environments/development.rb
config.action_controller.perform_caching = true
```

Then we need to restart the server, do a request to <http://localhost:3000/sitemap.xml> and you should see something like the following in your log.

```shell
Processing InfoController#sitemap (for 127.0.0.1 at 2009-03-17 17:04:26) [GET]
  Parameters: {"action"=>"sitemap", "controller"=>"info"}
  SQL (0.2ms)   SET NAMES 'utf8'
  SQL (0.1ms)   SET SQL_AUTO_IS_NULL=0
  ComatosePage Load (1.5ms)   SELECT * FROM `comatose_pages` WHERE full_path not like ''
Rendering info/sitemap
  ComatosePage Columns (2.0ms)   SHOW FIELDS FROM `comatose_pages`
Cached page: /sitemap.xml (0.7ms)
Completed in 16ms (View: 9, DB: 4) | 200 OK [http://localhost/sitemap.xml]
```

The line we're looking for is `Cached page: /sitemap.xml (0.7ms)`

In your public folder you should also see a `sitemap.xml` file.

If everything is configured correctly, subsequent requests to `/sitemap.xml` should not show up in the applications log, as the webserver is now serving the static file and not using Rails at all :-)


## Add a cache sweeper

Now that we can succesfully cache the sitemap, we need to make sure it stays fresh, when content in Comatose is updated.

Rails provides us with Cache Sweepers, which is kind of like an observer, but specialised. Let's create a cache sweeper that observes ComatosePage, and deletes the cached sitemap.xml when pages are saved or destroyed.

```ruby
## app/sweepers/comatose_sweeper.rb
class ComatoseSweeper < ActionController::Caching::Sweeper
    observe ComatosePage

    def after_save(page)
        expire_cache(page)
    end

    def after_destroy(page)
        expire_cache(page)
    end

    def expire_cache(page)
        # Use the ApplicationController, as were outside the scope
        # of the executing controller
        ApplicationController.expire_page( "/sitemap.xml" )
  end
end
```

Finally, we need to tell Comatose to use the sweeper.

```ruby
## config/initializers/comatose.rb
# set a cache sweeper to react when comatose expires pages from it's page caching
ComatoseAdminController.send :cache_sweeper,
    :comatose_sweeper, :only => 'expire_cms_page'
```

### Verify cache sweeper

To verify that your cache sweeper is working, all you need to is to is to save a page in Comatose and then verify the absense of `sitemap.xml` from the public folder.

## Finally

That's it! You know have a Comatose based Sitemap that will only be generated when there are changes.

P.S. Don't forget to set your development environment to NOT use caching anymore.

## Resources

* [Rails Envy: Ruby on Rails Caching Tutorial](http://www.railsenvy.com/2007/2/28/rails-caching-tutorial)
* [Rails Envy: Ruby on Rails Caching Tutorial - Part 2](http://www.railsenvy.com/2007/3/20/ruby-on-rails-caching-tutorial-part-2)
* [Scaling Rails Screencasts](http://railslab.newrelic.com/scaling-rails)
