---
url: https://www.macdrifter.com/2021/11/link-archiving-in-obsidian.html
readlater:
  synchtime: 1673284342363
---
# Link Archiving in Obsidian

2021-11-03

I’ve tried hard not to write about the Obsidian text editor because it gets tedious and boring. But I’ve been very happy with a couple of new plugins and this topic is really about link-rot. Let’s backup and talk about that first.

I’m a thousand years old now, so many of my bookmarks no longer work. The URLs are dead or, just as likely, the website is now behind a paywall. My bookmark services, like [Raindrop](https://raindrop.io) and [Pinboard](https://pinboard.in), offer offline copies of webpages but those also have limits. Many sites now block them from crawling pages or the page disappears before an offline copy is updated. I still bookmark URLs but for any info I want to **really** keep I try to capture it as a note, which requires a lot of commitment. It takes time to read and make summary notes so I end up skimming only the most basic information or I copy and paste the entire web page into some travesty of rich text and broken images.[1](#fn:1) Which brings me back to Obsidian and three plugins.

1.  [Link Archive](https://github.com/tomzorz/obsidian-link-archive)
2.  [Extract URL Content](https://github.com/trashhalo/obsidian-extract-url)
3.  [Local Images](https://github.com/aleksey-rezvov/obsidian-local-images)

Link Archive submits the selected URLs in Obsidian to Archive.org and gets back a “permanent” Archive.org URL. So if I have a link to a [Kieran Healy blog post](https://kieranhealy.org/blog/archives/2021/10/30/the-polarization-of-death/) about COVID death rates I just have to run the command and Obsidian will update the document with an [Archive.org version](https://web.archive.org/web/20211103/https://kieranhealy.org/blog/archives/2021/10/30/the-polarization-of-death/).

The plugin processes every link in a document which is very convenient.

If I want to be completely self sufficient I can use the Extract URL Content plugin to grab a Markdown copy of the page. This is a destructive plugin because it overwrites the current note with the Markdown, so I don’t recommend running it on a link in a document of notes.

![Extract URL Content](notes/images/c043826fd811a63f72d6b2e7e4744bf8_MD5.png)

The Local Images plugin retrieves a copy of every image linked in the document and stores them in the Obsidian attachments directory and updates the images links with new local links. That means if I paste in [an image from the internet](https://img.huffingtonpost.com/asset/5d02d614210000dc18f2057a.jpeg?ops=scalefit_630_noupscale) I can easily update the Obsidian note to replace the remote image link with a local Obsidian copy.

The plugin turns converts the image link from this:

![Before Local Image](notes/images/89e71bf2552623898a61d254566f4fbe_MD5.png)

To this local version:

![After Local Image](notes/images/50b1d9393207b5c7bcb98664aa440bde_MD5.png)

There are a couple of caveats with the Local Image plugin. First, it renames image files using a GUID. This avoids overwriting image files.

Second, this plugin only works with about 70% of the images I use. It fails with PNG and even some JPEG image links fail to be recognized by the plugin.

---

1.  Feel free to use that as a band name. I’d absolutely buy every album from _RIch Text and Broken Images_. [↩︎](#fnref:1)
    

-   [obsidian](https://www.macdrifter.com/tags/obsidian.html)