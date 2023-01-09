---
title: "Auto-Link and Generate Page in Obsidian"
url: https://www.thoughtasylum.com/2022/03/29/auto-link-and-generate-page-in-obsidian/
---

29 Mar 2022

Last year I wrote a post about [automation with Templater for Obsidian](https://www.thoughtasylum.com/2021/07/10/automation-with-templater-for-obsidian/). I showed some examples of using Obsidian’s Templater plugin to do some automation a little bit beyond what you might typically consider as the basics. One of the things in one of the examples bugged me for quite a while, and in this post I’m going to go through how I improved things for creating a link to a new page, and the correctly filed new page at the same time.

## The Old Approach

For my work, I keep a running daily list of what I have been doing in a [daily note](https://help.obsidian.md/Plugins/Daily+notes). This often includes links to meetings, and many of the meetings I have follow a standard template, with the same agenda, participants, etc. For example a weekly resourcing meeting.

In my original approach, I used the [Templater plugin](https://github.com/SilentVoid13/Templater) to create a link to the note, and the note itself. The tricky bit was the filing of the note into the correct folder. While the functionality I was using was capable of doing this, I couldn’t find a way to do it easily and so I resorted to adding a Templater line to the template used to generate the note to file the note.

This worked fine for months, and then I started getting a timing issue. I would end up with the link, and the filed note, but also an additional copy in the root folder.

## The New Approach

After getting nowhere with the timing, which I suspect was due to an update in the Templater plugin, I returned to investigating the original issue. This was that the Templater [`tp.file.create_new()`](https://silentvoid13.github.io/Templater/internal-functions/internal-modules/file-module.html#tpfilecreate_newtemplate-tfile--string-filename-string-open_new-boolean--false-folder-tfolder) function could create files in particular folders, but those folders had to be defined as a `TFolder` and that was the not so trivial aspect.

After digging through Obisidian and Templater documentation I finally found a way to produce a `TFolder` object based on a path. For example, this would identify a folder _bar_, in the folder _foo_, of the current vault:

```
app.vault.getAbstractFileByPath("foo/bar");
```

Armed with this, I could very easily create new files in particular folders, but for some reason, even though `tp.file.create_new()` accepts either a string or a template file as an input, when I included the folder parameter, the template file seemed to get ignored. As though they were mutually exclusive. When I did not use the folder parameter, the template file was pulled in as expected.

The documentation of the function is bare bones, so I don’t now if there is something intentional here, if it is a bug, or indeed if there was some error on my part. However, it was easy enough to work around by reading in the content of the template file and then passing that to the file creation function.

```
<%*
// Set the file name to create, the folder path to create it in, and the name of the template to use
const strName = "Note on Baz";
const strFolderPath = "foo/bar";
const strTemplateName = "Template Quz"

// Create the folder object
let fFolder = app.vault.getAbstractFileByPath(strFolderPath);
// Get the template file content
let fTemplate = await tp.file.find_tfile(strTemplateName);
let strContent = await app.vault.read(fTemplate);

// Create the new file in the folder from the template (do not open it by default)
await tp.file.create_new(strContent, strName, false, fFolder);

// Insert a link at the current cursor position to the new file
tR += "[" + "[" + strName + "]]";
%>
```

Note, `tR` is a Templater return variable that is output by Templater at the end of processing. Anything placed in this variable will be output by Templater at the current cursor position.

To use this Templater script, you can add it to a template. When you insert that template it will insert a link and create the new file based on a second template.

## Making it More Maintainable

Rather than adding this to every link template, I figured that since Templater supports libraries of scripts that it would be better to keep one central copy and to call that. This means it is easier to update and reuse.

The flip side of this is that it does complicates things a little as the JavaScript does not have direct access to `tp` and `tR`, which the Templater script uses. But we can work around this.

I created the following in my Templater scripts directory (a setting in the plugin) as `buildPageAndLink.js`.

```
async function buildPageAndLink(p_tp, p_strTemplateName, p_strName, p_strFolderPath, p_bPrefixDateStamp = false)
{
let strName = p_strName;
if (p_bPrefixDateStamp) strName = p_tp.date.now("YYYY-MM-DD") + " " + strName;
let fFolder = app.vault.getAbstractFileByPath(p_strFolderPath);
let fTemplate = await p_tp.file.find_tfile(p_strTemplateName);
let strContent = await app.vault.read(fTemplate);
await p_tp.file.create_new(strContent, strName, false, fFolder);
return "[" + "[" + strName + "]]";
}
module.exports = buildPageAndLink;
```

The script is mostly converting the previous template into an exportable function. However, I also added an optional parameter to prefix a date stamp to a note title (default is not to add). So many of my notes based on templates get date stamps that it was a useful option to build into the function.

The same template set up as earlier would then become this:

```
<%* tR += await tp.user.buildPageAndLink(tp, "Template Quz", "Note on Baz", "foo/bar", false); %>
```

Note, that while I tried passing in the `tR` as a parameter, this did not produce any output, so I switched to working with it as output from the function. It is not quite as neat as I would have liked, but it is neat enough.

You can also take this further and build other functions that rely on it. For example, say you have a team and keep notes for your team members that are dated and use their initials as the identifiers in a standardised set of templates. You could then create an additional function like this that utilises the previous one.

I can start by adding the details below to my Templater scripts directory as `buildTeam121.js`.

```
async function buildTeam121(p_tp, p_strInitials)
{
return await p_tp.user.buildPageAndLink(p_tp, "1-2-1 Template for " + p_strInitials, "1-2-1 with " + p_strInitials, "Work/Team/1-2-1", true);

}
module.exports = buildTeam121;
```

This gives a much simpler function call as many of the parameters are static or can be built from a common item of data - the initials of the team member.

The resulting Templater script to create a link (and page) for a 1-2-1, for a team member called Jane Doe, then becomes:

```
<%* tR += await tp.user.buildTeam121(tp, "JD"); %>
```

If you name your templates well, helper functions like this can make the experience that much easier.

## Summary

This updated approach loses the automatic filing if the file is populated independently, but in practice, for me, that never occurs. I am always linking from somewhere as cross referencing is a large part and benefit of my note taking approach. The most important thing though is that it addresses the previous timing issue that surfaced, thus restoring my ability to insert a link and create a page all in one fell swoop, thanks to the power of the Templater plugin for Obsidian.