---
title: "Automation with Templater for Obsidian"
url: https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/
---

# Automation with Templater for Obsidian

10 Jul 2021

Please note, an updated approach to creating a page and link in one action is [now available](https://www.thoughtasylum.com/2022/03/29/auto-link-and-generate-page-in-obsidian/).

  

## Contents

-   [What is Templater?](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#what-is-templater)
-   [But Obsidian Has Templating in the Set of Core Plugins](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#but-obsidian-has-templating-in-the-set-of-core-plugins)
-   [What About TextExpander?](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#what-about-textexpander)
-   [The Power of Templater](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#the-power-of-templater)
-   [An Example Filing Automation](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#an-example-filing-automation)
    -   [Using Folders](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#using-folders)
    -   [The Template: Content](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#the-template-content)
    -   [The Template: Automating Filing](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#the-template-automating-filing)
-   [An Example Linking and Creating Automation](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#an-example-linking-and-creating-automation)
-   [Command Line Gurus](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#command-line-gurus)
-   [Poetic License](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#poetic-license)
-   [Conclusion](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#conclusion)

Obsidian is my current personal knowledge management tool of choice. The primary reason for this is undoubtedly because it utilises plain text Markdown files, which gives me flexibility for the future, and access to easily process notes using any other text processing tool of choice. A second factor is the range of plugins available for the application. One of my absolute favourites is _Templater_, a plugin for templating within Obsidian, and I’m going to explain in this post one of the ways I use it to automate my use of Obsidian.

## What is Templater?

Templater is an extra component, written by an Obsidian community member (SilentVoid13), that you can add into Obsidian using its plugin architecture. When configured and run, it allows you to create new text content in your Obsidian note. Here is how it is described in the community plugins catalogue.

> Templater is a template language that lets you insert variables and functions results into your Obsidian notes. It will also let you execute JavaScript code manipulating those variables and functions.
> 
>![](notes/images/e69f5f215c17144907220ce4ca23c976_MD5.gif)

-   [Obsidian Help: Enabling Third Party Plugins](https://help.obsidian.md/Advanced+topics/Third-party+plugins#For+users)

> If you want to know how to set-up and use Templater, I have [a brief walk through that explains it step-by-step](https://www.thoughtasylum.com/2021/07/24/the-basics-of-templater-for-obsidian/).

At an introductory level, it allows you to specify text in a file, and then through a few keystrokes, have [Obsidian](https://obsidian.md/) insert the content into your note. This allows you to have boiler plate text for things like meeting notes or daily logs.

## But Obsidian Has Templating in the Set of Core Plugins

As well as offering an option to use plugins that you, or other members of the Obsidian community create, Obsidian also utilises the plugin architecture itself to offer optional core features. One of these is the _Templates_ plugin. It is similar to Templater in that it allows you to automatically add content from other template notes.

The difference is that Templates is only intended to be a bare bones solution, whereas Templater is a much more flexible and powerful solution for those who are looking to do more

## What About TextExpander?

Many of you may be thinking that this sounds a lot like the sort of stuff that as tool like [TextExpander](https://texexpander.com/) can do, but that tool applies across applications, whereas Templater would only work within the scope of Obsidian. This is entirely true, but due to some of the options that Templater provides, I have settled on a combination of both TextExpander and Templater.

Anything that could be of use outside of Obsidian goes in TextExpander. Anything Obsidian specific that can benefit from Templater’s tighter integration and automation options goes into Templater. Anything else, I just go with a gut feel, safe in the knowledge I can always change it later if I need to.

For example, I tend to put all my different meeting outline frameworks into Templater. Many of them could be triggered by TextExpander just as easily, if not more so. But then I would be splitting my templates for meeting outlines across two sources. Because some of them can benefit from Templater functionality, I consolidated them into Templater.

## The Power of Templater

The [documentation for Templater](https://silentvoid13.github.io/Templater/docs/) feels to me at this point to be a bit of a work in progress, much as the plugin. There are examples of how to use the features, including some of the more advanced features, but not all features work quite as expected and in many cases additional examples and explanations would help to explain how to use features, and when you would even use some features. I’ll be covering an example of this in the automation I’ll describe later.

To my mind, the documentation gives you a view of two different levels of automation potential.

The first is built around Templater’s [internal functions and variables](https://silentvoid13.github.io/Templater/docs/internal-variables-functions). These allow you to do some pretty cool things, and you can even [evaluate them dynamically](https://silentvoid13.github.io/Templater/docs/commands/dynamic-command) each time you preview a Markdown page. This functionality has a large scope on its own.

The second opens up Templater to be able to use JavaScript (much like TextExpander does) to carry out processing, but because it can also utilise the internal functions and variables, this allows for a much deeper level of processing than a tool like TextExpander does, as it simply does not have access to the Obsidian/note information that Templater does.

## An Example Filing Automation

At this point, I want to get down to the detail of a worked example that I use in my own Obsidian vaults<sup id="fnref:1" role="doc-noteref"><a href="https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#fn:1" rel="footnote">1</a></sup>. The example I’m going to work through is how I use the Templater automation functionality in respect to meeting outline templates.

### Using Folders

Within the personal knowledge management (PKM) space, the storing of content in folders is generally eschewed. Content, or knowledge could connect in many different ways and may be applicable in several places. Combined with the searching and linking capabilities, why would you ever want to compartmentalise content into folders, seemingly isolating them and constraining their use?

Well, for me, I feel that the only merit to the arguments presented is the additional effort required to maintain the folder structure. The fact that we do have powerful searching and linking functionality in tools such as Obsidian means that we can layer whatever we like on top to meet our current needs. This is like having a structured database where we can put any app or presentation layer we like on top, but the structure we apply to the underlying data gives us performance and management efficiencies.

For me this is entirely analogous to a file and folder structure as much as it is a database. Many operating systems tend to hit performance issues when processing thousands of files in the same folder. Especially when attempting to display such a folder. I use GitHub as my back end sync between devices, and GitHub certainly likes a bit of structure and limited listings of files in folders in the web interface.

Logical groupings into folders also lets me easily copy or share sets of content in a structured manner for other vaults or projects that don’t even use Obsidian. I could even share a particular folder with others in a team, controlling the permissions at the folder level.

I strongly believe that folders are not obsolete in the PKM space, and in fact hold a very important place. But I do agree that folders should not necessarily define the structure of the data in terms of how it is accessed and used.

On that basis, let’s take a look at an example folder structure branch within a vault.

```
Work/
├─ 5 - Meetings/
│  ├─ 5.2 Meetings - 1-2-1 Personal/
│  │  ├─ 2021/

```

Here I have a “Work” folder for containing information relating to work. Within that a folder for meetings, and a sub-folder of that to store meeting information about my one-to-one meetings. Finally, there are annual sub folders. This makes it easy to share (e.g. combine into a single PDF using some command line tools to render the Markdown files) or archive a specific year of meetings.

### The Template: Content

I’m going to start with my basic one-to-one example template. Keep in mind that everything here could just as easily be generated by your text expansion tool of choice, including Obsidian’s core _Templates_ plugin.

I’ve named this template `Meeting - 1-2-1 Me (Template)`. Having some compound terms to generate the name of the file like this makes it easy for me to find the template when I’m wanting to use it or edit it. In reality I have several one-to-one templates as I manage a team, many meeting templates for my regular meetings (plus a generic one of course), and I use `(Template)` in the title so I can quickly and easily search for my personal templates <sup id="fnref:2" role="doc-noteref"><a href="https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/#fn:2" rel="footnote">2</a></sup>.

In the template, I’ve included a link to a page about the person I’m having the one-to-one with, some details about the meeting (I would tend to modify the location line after the content has been added), and then a breakdown of the standing agenda.

```
## Attendees
- Stephen Millard
- [[Zach Young]]

## Meeting Details
- **Topic:** 1-2-1 with Zach Young
- **Location:** Virtual / In Person
- **Date:** <% tp.date.now("YYYY-MM-DD") %>
- **Time/Duration:** xx:xx - xx:xx

## Agenda
1. Employees
2. Projects
3. Sales/Lead Generation/Proposals
4. Actions from Teams Planner
5. Objectives
6. AOB

## Employees
- N/A.

## Projects
- N/A.

### Sales/Lead Gen/Proposals
- N/A.

## Actions from Teams Planner
- N/A.

## Objectives
### Objective 1
- 

### Objective 2
- 

### Objective 3
- N/A.

### Objective 4
- N/A.

### Objective 5
- N/A.

## AOB
- N/A.

---

**Tags:** [[My Team]]
```

There are probably two points of note here. The first is the date line in the meeting details, and the second is the tags line at the very end. I promise to come back to my use of Obsidian’s hash tag based tagging at some point, and how I use them, but for now, I’ll just note that I “tag” my content with links to other pages using the wiki-style cross-link syntax favoured by Obsidian and many other PKM tools.

On the date line, you can see the following syntax:

```
<% tp.date.now("YYYY-MM-DD") %>
```

The angle brackets with percentage signs are the markers for Templater to tell it to process the commands between the markers when the content from this file is inserted into a new file.

`tp` is a Templater ‘object’, and is the top level for accessing the internal functions and variables we made reference to earlier. One of those sets of functions is for dates and times, and is called `date`, which is the next level of the command (separated by periods). The third entry is the function we are using , `now()`. This is telling Templater that we want to insert the current date and time. The string in the brackets of `"YYYY-MM-DD"` tells Templater that we want to insert the current date and time in a particular format of year, hyphen, month, hyphen, day (an ISO 8601 standard format).

That’s the basic template. Nothing amazing in that, but here is where we add the special Templater sauce.

### The Template: Automating Filing

I have added the following line to the end of the template. It is used to automatically move the file to the folder where I want to file my personal one-to-one notes as outlined earlier.

```
<% await tp.file.move("/Work/5 - Meetings/5.2 Meetings - 1-2-1 Personal/" + tp.date.now("YYYY") + "/" + tp.file.title) %>
```

Again, we see the angle bracket and percentage symbol syntax to mark the instruction that we want Templater to process. We also see the `tp` object, but this time it is preceded by the word `await`. This is a special JavaScript keyword that tells the instruction to wait before continuing. It probably is not going to make any difference here as we are not queuing up anything after this file move, but it is good practice to include this just in case you begin utilising the template in more sophisticated processes.

This time instead of working with the current date and time, we are working with the file itself, and so use `tp.file`. We want to put the file in a specific folder, so here we use the `move()` function, which takes a relative path (excluding the file extension) for where to move the file to. The file will be created in the default Obsidian location initially, and exists by the time we are running this command, which means we can get the existing name of the file to use in the move.

Having seen how the date worked above, you can probably already understand how the path is built up. `+` symbols are used to concatenate a path string together made of the folder path I outlined previously, the current year, a folder path separator, and finally the name of the file excluding the file extension (this is the `title`).

Now when I create a new personal one-to-one file via this template, it automatically gets filed to the right folder.

## An Example Linking and Creating Automation

The way I work for work is primarily off of a daily note. Through daily notes, Obsidian allows me to create a work journal that allows chronological linking of information, which is very useful for completing my time sheets! As a result I often, though not always, start from my daily note page by creating a link out to a meeting. Therefore it would be a natural extension to create a quick way to link to a meeting.

My original approach, before Templater got some of this extra functionality, was to use a TextExpander snippet to create links. After all, my standard naming convention is to use an ISO date followed by some standardised name for the meeting - e.g. `2021-07-10 1-2-1 with ZY`. That meant I created the link with a text expansion, opened the link, then inserted the template into the new note that was created.

Instead of doing that, I now use Templater to create the link, and the entire note, all in one expansion. Here’s the template I use to do that.

```
[[<% (await tp.file.create_new(tp.file.find_tfile("Meeting - 1-2-1 Me (Template)"), tp.date.now("YYYY-MM-DD") + " 1-2-1 with ZY", false)).basename %>]]
```

This command is a little more complex still than the previous commands, so let’s break it down.

As with the previous Templater instructions, you should be able to see the angle bracket and percentage symbol markers. Outside of these are double square brackets. This is just the notation for a wiki-style internal link that Obsidian can use to allow you to link from one note to another. With the extremities out of the way, that leaves us with the following.

```
(await tp.file.create_new(tp.file.find_tfile("Meeting - 1-2-1 Me (Template)"), tp.date.now("YYYY-MM-DD") + " 1-2-1 with ZY", false)).basename
```

The next layer we’ll look at is `(…).basename`. This is going to return the base file name of a particular file. It appears to be a shorthand way of referencing the same data as `tp.file.title` for the current file, but it can be applied to any file. The only mention of `basename` in the Templater documentation is in one of the examples, and I _strongly_ suspect it is actually something being leveraged from the Obsidian data model. Unfortunately it is obscurity like this and nothing about function return values that makes me feel like the Templater documentation is still a work in progress, but is also why I think posts like this are going to be useful to people.

To this point we have set-out what we are going to output as the wiki-style link in the current note. The remaining instructions between the parentheses are what is used to create (and return) the file we will link to.

```
await tp.file.create_new(tp.file.find_tfile("Meeting - 1-2-1 Me (Template)"), tp.date.now("YYYY-MM-DD") + " 1-2-1 with ZY", false)
```

Once again, we see an `await`, but it is most definitely important this time as we need to process the result to get the base name of the file that is created. Here we are using `tp.file.create_new()` to create a new file from a template, and it is the result of this function that is the new file.

We are passing three parameters to this function.

1.  The template file to create the new file from.
2.  The base name for the new file (i.e. excluding the `.md` file extension).
3.  A Boolean (true/false) value on whether to open the file for editing.

I think it is important at this point to note that there is a fourth parameter that accepts a folder for where to create the new file. However, this parameter accepts a `TFolder` object. An object that is not defined in the documentation, and once again seems to be part of the Obsidian plugin architecture, but leaves Templater users with no easy Templater way to specify a folder.

For the third parameter, I am specifying `false` such that when the template is processed I am **not** automatically navigated to the new file. This is to forego the issues described in the documentation of this function and potential race conditions causing undesired effects.

The second parameter you will note is quite similar to one of the earlier templates using a combination of the `now()` function and a static text string to generate the name of the file.

The first parameter identifies the template file to use, and here we are going to use the template file we created earlier. This means that not only will it include the same content, but it will automatically get filed, which has the benefit of helping us work around the limitation of the fourth parameter. Here, I’m using the `find_tfile()` function of `file` to search for a template file by name.

And that is how to build a template that will create not only a link to a new file, but also create (and move) the file in the background based on another template.

This linking template is stored in a template file called `zzz_Meeting - 1-2-1 Me (Link)`, meaning I can quickly access these templates by prefixing with three ‘z’ characters. I might well change this prefix at some point. It is something I’m still considering options for. The point of using the `zzz_` prefix is that Obsidian will sort these to the bottom of my templates when I’m choosing one to insert, and the triple ‘z’ should be a good identifier as English words only contain a maximum of two consecutive ‘z’ characters.

## Command Line Gurus

There will inevitably be people who have scripts set-up outside of Obsidian that can accomplish the same things. These have the advantage of being entirely independent of Obsidian should you want to change tooling from Obsidian at a later date, or even use something else in parallel.

Honestly, that is great, and if Templater did not exist, I strongly suspect I would have created a few scripts to do this sort of thing. But, the advantage here is that the plugin architecture should work everywhere Obsidian is. This means that I can utilise a single solution across any OS, including, in theory, the upcoming mobile applications.

As someone who is very much in a cross-platform, cross-ecosystem way of life, this is a definite consideration for me at this time. The convenience it provides outweighs any future-proofing, and I can see myself using Obsidian for years to come.

## Poetic License

> Before I wrap up I would like to explain one underlying point to the above. My _actual_ templates are similar to these, but not necessarily exactly the same. These are taken from a demo vault I am using to write about Obsidian. My actual templates are typically more tailored and often contain many more expansions and functions within them. They are very much tailored to my own specific needs. Therefore, my actual real-world use is a little different to what is presented here - a simplified and sanitised version; but hopefully it is better suited to people’s learning.

## Conclusion

Templater is a powerful plugin, and I think, should be installed by anyone who wants to automate their Obsidian use. While there is documentation for Templater, it is a little too light in places, but I am sure that this will improve over time.

For me Templater does not replace TextExpander. Instead, it complements it, giving me additional options that tie into automations such as those described in this post.

I hope that what I have described above is incentive enough for you to try out Templater, and maybe even to use the above templates as a basis for driving some additional automation out of Obsidian.