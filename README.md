wordpress-migration
===================

A tool for us to use when converting blogs from Wordpress to SunBlogNuke

## What will I need?

* Get the [agency](https://github.com/agencyrevolution/agency) subcommand.
* Stable [Mono Runtime](http://www.go-mono.com/mono-downloads/download.html)
* Clone the `WPBlog2ML.exe` into your `bin` like so…
`git clone -b tool git://github.com/agencyrevolution/wordpress-migration.git ~/bin`

## How do I get started?

1. Login, Tools, and Export a Wordpress blog to your `~/Downloads`
2. Change directories to `~/Downloads`
3. In your shell run `wpmigrate blogname.wordpress.2013.03.04.xml` just make
sure to match the filename instead of this example's bogus filename.
4. The tool will create a new file caled `blogname.blogml.2013.03.04.xml` in
your `~/Downloads` folder.

## Fixing Hyperlinks and Image References

Please note that due to the lack of custom permalinks in SunBlogNuke, we won't
be able to fix links referencing existing blog posts because there is no way of
predicting `entryid` for every blog post we create in the migration process.

Using a text editor with regex find and replace, the following:

*`{portalname}` and `{domain}` are tokens that should be customized before
running these searches.*

**Search** `http://{portalname}.arevblog.com/files`
**Search** `http://blog.{domain}/files`
**Replace** `/Portals/{portalname}/images/blog`

**Search** `http://blog.{domain}/wp-content/uploads`
**Replace** `/Portals/{portalname}/images/blog/uploads`

**Search** `http://www.{domain}/`
**Replace** `/`

**Search** `http://blog.{domain}/20([0-9]*/)*(\w*(-)?)*/`
**Replace** `/blog`

**Search** `root-url="http://blog.{domain}"`
**Replace** `root-url="http://{domain}/blog"`

**Search** `http://blog.{domain}`
**Replace** `/blog`

**Search** `email="{portalname}@blog.{domain}"`
**Replace** `email="service@{domain}"`

**Search** `href="(http://)?(www.)?{domain}`
**Replace** `href="/`
