---
url: http://www.macdrifter.com/2021/08/obsidian-templater-fun.html
readlater:
  synchtime: 1673284020407
---
# Obsidian Templater Fun

2021-08-06

Page content

-   [Use Case](#use-case)
-   [Templater](#templater)
-   [The Template](#the-template)
    -   [Templater Files](#templater-files)
-   [Conclusion](#conclusion)

I’m still having fun and friction with Obsidian. But let’s try something a bit more challenging than deciding on a folder structure for our notes. One of the things I like about modern text editors is that they are incredibly extensible. Most have a plugin architecture and also support some sort of scripting language. Obsidian has both and they are built on JavaScript.

This article concerns the extremely powerful [Templater plugin for Obsidian](https://silentvoid13.github.io/Templater/). To a lesser extent it is about the [Eta JS templating](https://eta.js.org) engine that drives the Templater plugin and the fun of learning new things.

## Use Case

I have multiple directories in my Obsidan vault. I have a folder for work stuff and a folder for general notes. I also have a folder for Macdrifter drafts. You get the idea. There’s a bunch of folders but when I tell Obsidian to create a new file I only get one option for the default note location. This is frustrating. So, with a tiny bit of research and key mashing I created a template that does the following:

1.  Ask me for a note title
2.  Create a new note with the title containing a date suffix
3.  Add some front matter that I always want to include in notes
4.  Move the note to the right folder
5.  Show me the note ready to edit with the cursor blinking away at the bottom

## Templater

Templater is a plugin for Obsidian that adds support for the [Eta templating engine](https://eta.js.org). Templates are simple markdown documents where JS snippets are included alongside plain text. These snippets execute when Templater runs a template. The functions in Templater range from simple text insertion to manipulating the Obsidian application itself. Templater can move files, rename them, add new content, and [do pretty much anything I want to do inside Obsidian](https://silentvoid13.github.io/Templater/docs/internal-variables-functions/internal-modules/file-module).

## The Template

Let’s get to the good stuff. Here’s a Templater template that can be copied:

```javascript
 1<%*
 2let qcFileName = await tp.system.prompt("Note Title")
 3titleName = qcFileName + " " + tp.date.now("YYYY-MM-DD")
 4await tp.file.rename(titleName)
 5await tp.file.move("/Notes/" + titleName);
 6-%>
 7---
 8title: <% qcFileName %>
 9date: <% tp.file.creation_date("YYYY-MM-DD HH:mm:ss") %>
10tags: quick_note
11topic: 
12---
13
14<% tp.file.cursor() %>
```

Here’s the same script with annotations:

![Annotated Template](http://www.macdrifter.com/uploads/2021/08/2021-08-06_10-03-07.png)

The annotations are pretty self explanatory but I definitely struggled with the Eta and Templater documentation. Let me explain in some painful detail.

When Templater runs, it creates a new blank file and then runs the code in the template file. Everything we put in the template file results in some output and changes the empty file Templater just created. It’s all based on Eta templates so there’s a lot more power than just inserting predefined text.

Eta allows single line codes and larger code blocks. Checkout the the [the syntax documentation](https://eta.js.org/docs/syntax), but I’m using a code block at the top of the template file for all of the basic logic.

The code block uses an [“interpolation tag”](https://eta.js.org/docs/syntax/interpolate) (an asterisk) to tell the template to execute this and then use the results. Since this block is mostly about moving files, the block outputs a blank line. We will get to this very soon. First, let’s talk about the block.

```javascript
1let qcFileName = await tp.system.prompt("Note Title")
```

This neat. We create a variable in the template and tell Obsidian to display a text entry box. The value we put in this box is assigned to the variable `qcFileName`.

The next line creates another variable that will contain the document title plus the current date. I use this to name the file. Date suffixes are nice to avoid collisions and also add some context when browsing a folder full of files.

```javascript
1await tp.file.rename(titleName)
```

This `await` method tells Obsidian to rename the new file but make the user wait to interact until after the file rename is done. Next we tell Obsidian to move the file to a different folder.

```javascript
1await tp.file.move("/Notes/" + titleName);
```

I have no idea if the semicolon is required but it works and is predictable so I’m keeping it.

The last line closes the Eta block in a special way that is very important.

```javascript
1-%>
```

As I hinted above, every time an Eta function is executed it outputs **something**. If the function produces no text then it outputs an empty line. Since this code block is at the top of my template I would end up with a blank line before my YAML front matter, which I don’t want. Fortunately [Eta has a lot of control over whitespace](https://eta.js.org/docs/syntax/whitespace-control) and the [Templater site has some additional notes](https://silentvoid13.github.io/Templater/docs/commands/whitespace-control). That dash in the Eta block closure removes removes white space after the closure, so that blank line is magically deleted. Neat!

Now we are out of the block and into some basic template stuff. The plain text in the Templater template is inserted as is. Any Eta code is evaluated and also inserted. So this line is inserted as a literal:

```javascript
1tags: quick_note
```

But this line is inserted as a combination of literal text PLUS the value of the variable we defined in the block at the top.

```javascript
1title: <% qcFileName %>
```

It’s very cool that variables are accessible outside of the block they are created in.

We can also access Obsidian file properties from within the Templater functions. For example, this line grabs the creation date of the current file and formats it as [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) (the way nature intended).

```javascript
1date: <% tp.file.creation_date("YYYY-MM-DD HH:mm:ss") %>
```

### Templater Files

When Templater is called from within Obsidian it displays a list of all templates it knows about. There’s a configuration for the plugin where that’s defined.

![Templater Config](http://www.macdrifter.com/uploads/2021/08/2021-08-06_10-53-34.png)

Templater has two modes when called:

1.  Create a new file using a template
2.  Insert text at the current cursor using the output of a template

I’ve pinned both of these commands in Obsidian because I use them all of the time.

![Templater Commands](http://www.macdrifter.com/uploads/2021/08/2021-08-06_10-55-15.png)

There’s a problem though. Templater doesn’t differentiate between templates that I use for new files and templates that I use for snippets. So I have to give myself hints by prefixing the template names with “ff” for “file” and “ss” for “snippet”. I use repeat characters because these are easy to type on iOS and quickly filter the list.

![Filtered Templates](http://www.macdrifter.com/uploads/2021/08/2021-08-06_11-01-17.png) I store all of my templates in a “Meta” directory. There are different template plugins for Obsidian and I want everything organized so I know which templates go with which plugin. I’ve now stopped using most of the other Obsidian plugins for templates.

![Template Folder](http://www.macdrifter.com/uploads/2021/08/2021-08-06_11-03-26.png)

## Conclusion

I had fun with Templater and Obsidian is working better for what I need. That’s a double win. I still find Obsidian to be a little awkward on iOS but Templater helps out there too. Templates are quickly accessible through icons and the command palette so now I can create a new note where I need it with just three taps on iOS. There are some interesting possibilities here and I haven’t even touched Templater system commands or [user functions](https://silentvoid13.github.io/Templater/docs/user-functions).

-   [obsidian](https://www.macdrifter.com/tags/obsidian.html)
-   [text](https://www.macdrifter.com/tags/text.html)