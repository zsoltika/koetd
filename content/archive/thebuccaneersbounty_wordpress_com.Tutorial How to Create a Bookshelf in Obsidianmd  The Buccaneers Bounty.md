# [Tutorial: How to Create a Bookshelf in Obsidian.md – The Buccaneer's Bounty](https://thebuccaneersbounty.wordpress.com/2021/08/21/tutorial-how-to-create-a-bookshelf-in-obsidian/?share=twitter%20%22Click%20to%20share%20on%20Twitter%22)
This is a tutorial on how to create a book library or database in Obsidian.md. The guide also shows you how to use the Dataview, Templates, and Quick Add plugins.

#### Update History ####

* *09/02/2022: Added the code format to insert a local image as the book folder.*
* *08/23/2022: Added screenshots on the How to Install section.*
* *06/19/2022: Fixed the missing screenshots. Sorry about that!*
* *04/05/2022: Added a new optional feature (inline dataview query language) and updated the sample vault in Github*.
* *01/09/2022: Added a new optional feature (list of read books) and the sample vault*.
* *09/04/2021: Added the optional Obsidian Banners plugin*.
* *08/23/2021: Added a new optional feature*.

Things Needed
----------

* Obsidian
  * Dataview (Community Plugin)
  * QuickAdd (Community Plugin)

How to Install the Community Plugins
----------

1. Click on the Settings button in Obsidian. You can find it in the bottom-left corner.

![](https://imgpile.com/images/Td8UMS.png)
1. Go to the Community Plugins tab and turn off Safe Mode to enable plug-in installation.

![](https://imgpile.com/images/Td85jb.png)
1. Click on Browse and type “**Dataview**“ on the search form.

![](https://imgpile.com/images/Td8TC3.png)
1. Click on the **Install** button and the **Enable** button. Repeat steps 3 and 4 to install **QuickAdd**.

How to Create a Book Note using a Template
----------

*Screenshot of the book template*

**Templates** are used to automatically fill in the content for your note.

1. Create a folder called `_templates`. This will house the templates used for your book notes.
2. Click on the Settings button on the bottom left corner and select **Core Plugins**. Turn on Templates to enable this plugin.

![](https://imgpile.com/images/TdzlK8.png)*Templates plugin in the Core plugins menu*
1. Look for **Templates** under Plugin Options.
2. Set the template folder location to `_templates`.

![](https://imgpile.com/images/Tdzm2b.png)
1. Create a new note and name it “Book Template”. Type the following on the **top of the note**:

```
---
Alias:
Author:
Status:
ISBN:
Cover:
---
```

|                                                                                                                                                                                                                                                                                                                      |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|💡 What you have just added is called a YAML frontmatter. This is a type of custom metadata that you can put in your notes and it will be used by the Dataview plugin to display your books. You can use it to sort your books by author for example. Note that this frontmatter is hidden when viewed in Preview mode.|

Here is an explanation for each YAML frontmatter:

* **Alias:**
  * This is an optional metadata you can put if a book has an alternate title. For example, you can put Divina Commedia as an alias for The Divine Comedy, the original Japanese title for a manga, or the full title of a non-fiction book.

* **Author:**
  * This is where you put the author of the book. If the book has a translator (in the case for classics or international books) put `[Author, Translator]`.

* **Status:**
  * This is where you put if the book is filed under “unread”, “currently reading” and “read”.

* **ISBN:**
  * An optional metadata if you want to include the book’s ISBN.

* **Cover:**
  * This is where you put the cover of the book. I recommend adding a URL of the picture for it to work. The downside of this method is that you cannot view the image offline.
  * If you want to use a local image, use this format and replace the file path after the `src=` part of the code: `<img width="150px" src="file:///C:/Users/USERNAME/Obsidian/Vault Name/_image source/Book Covers/Book Cover.jpg">`

After creating the template, we can now use it to generate a new book note using the QuickAdd plugin.

How to Add a New Book Note using QuickAdd
----------

![](https://imgpile.com/images/Tdz89l.png)*QuickAdd command to add a new book*

**QuickAdd** is a plugin that lets you quickly add templates and new content to your vault. Using this plugin allows you to add a new book note from the command palette instead of adding a new note, applying the template, and moving it to the folder (saving you three or more clicks!)

### Setting Up QuickAdd ###

1. Go to **Settings** and look for QuickAdd under the Plugin Options.

![](https://imgpile.com/images/TdzB9a.png)
1. On the textbox, add a name for the command (I use “Add New Book”) and then click **Add Choice**.

![](https://imgpile.com/images/TdzF8X.png)
1. Click on the gear icon to open up the settings of the Add New Book command.

![](https://imgpile.com/images/Tdzv5E.png)
1. On **Template Path**, select the Book Template you just made.

![](https://imgpile.com/images/Tdz3cr.png)
1. Turn on the **Create in folder** button and select the folder location of the books (Make sure to add a folder in your vault first!). Press the **Add button** to confirm.

![](https://imgpile.com/images/TdzpIg.png)
1. **Optional:** Click the toggle on the **Open** and **New Tab settings** if you want QuickAdd to open up the newly added book in either a vertical or horizontal tab.

![](https://imgpile.com/images/TdzSMc.png)
1. **Optional:** Click on the lightning bolt icon to add a shortcut to this command on the Command Palette.

![](https://imgpile.com/images/TdzZAN.png)

### How to Use QuickAdd ###

Once you’ve set up the QuickAdd command, open the Command Palette (or press Ctrl + P) and type QuickAdd. Select the Add New Book command.

![](https://imgpile.com/images/TdzaeW.png)

A new window will pop up after clicking on the Add New Book command. Type the name of the book and QuickAdd will automatically create a new note with the Book Template applied.

![](https://imgpile.com/images/TdzjCP.png)

From here, you can add the metadata for the book.

![](https://imgpile.com/images/TdzyV1.png)

How to Create the Book Library using Dataview
----------

*The library note in Edit and Preview mode*

In this section, I’ll explain how to use the Dataview plugin to display a list of your books in the Book Library note.

1. Create a new note called Library. Make sure to put the note outside of the Books folder.
2. Add the following Dataview code below in the Library note:

*The dataview code to display the list of books in the Library note.*

Here is a line by line explanation:

* `table Author, ("![coverimg|100](" + Cover + ")") as Cover`
  * This tells the Dataview plugin to create a table with the following rows: author and the book cover.

* `from "Books"`
  * This tells the Dataview plugin to specifically display the contents from the Books folder.

Add Optional Features
----------

### Create a Book Tracker ###

![](https://images2.imgbox.com/b7/90/FCw7jjzg_o.png)

You can also use the Dataview plugin to create a book tracker to sort the books according to their status.

Add the following Dataview code below in your Library note:

*The Dataview code to display the tracker.*

Here is a line by line explanation:

* `table rows.file.link as Book`
  * This tells the Dataview plugin to create a table with the row called ‘Book’ to display the files.

* `from "Books"`
  * This tells the Dataview plugin to specifically display the contents from the Books folder.

* `group by Status`
  * This will group the contents from the Books folder according to their Status metadata.

* `sort Status`
  * This sorts the table according to Status. This only works if there are books with multiple statuses (unread, read, currently reading).

### Add Lines on a Dataview Table ###

![](https://thebuccaneersbounty.files.wordpress.com/2021/08/dataview-add-lines-per-table.png)*Add a line per entry in a Dataview table*

If you want to add a line in between each entry on a Dataview table, you can use the following CSS Snippet:

```
.table-view-table tr {
    border-bottom: 1px solid;
}
```

|                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------|
|💡If you want to change the thickness of the lines, change the number on the border-bottom field. I use 0.5px on my vault as an example.|

To add this to Obsidian, open Notepad and copy-paste the snippet. Save the document as a .css file and move it to the snippets folder (Vault Name -> .obsidian -> snippets).

If the snippets folder is missing, go to your Settings and select **Appearance**. Under CSS Snippets, click on the folder icon for Obsidian to create the snippets folder automatically.

After adding it to the snippets folder, open Settings in Obsidian and select Appearance. Under CSS Snippets, click on the refresh icon to reload the snippets and click the toggle to enable it.

![](https://imgpile.com/images/Td8Icj.png)

### Add a Top Banner ###

*An example top banner in a library note*

If you want to add a top banner to your Library (just like in Notion pages) you can either add a local image (a picture from your attachments folder) or link an image online.

For local images, add `![[Top Banner Image.png]]`. To add an image from the Internet, add `![Banner](Image URL)`. Use the following dimensions: `1500px x 300px` to match the size of the image shown above.

#### Optional: Install the Obsidian Banners Plugin ####

You can also use the [Obsidian Banners](https://github.com/noatpad/obsidian-banners) plugin to add a top banner using a local image or an image from the internet.

Install the plugin from the Community Plugins and add the following on **top of the Library note**:

```
---
banner:
---
```

If you want to add an image from the Internet, simply add the image’s URL. See the example code below:

```
---
banner: https://images.unsplash.com/photo-1519052537078-e6302a4968d4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80
---
```

For local images, press **Ctrl + P**, type `Add Local Image`, and select **Banners: Add/Change banner with local image**.

Type the name of the image you want to use as a banner and press enter.

Once you have a banner in place, you can click and hold the image to reposition it. This adds `banner_x` and `banner_y` in the YAML frontmatter. You can manually input the number or reposition the image to change the numbers.

*Repositioning the banner adds two fields (banner\_x and banner\_y) in the YAML frontmatter*

### Sort Books in Alphabetical Order ###

*Three books in alphabetical order in the Library note*

If you want to sort multiple books in alphabetical order, add the following in your Dataview code:

```
sort file.name asc
```

### Display a Specific Book Based on Its Type ###

If you want to display a specific type of book (like books about fitness), you can add the **Type:** YAML frontmatter on the book note.

*A book note with the Type: Fitness on the YAML frontmatter*

Once you have added the frontmatter, go back to your Library note and add the following in your Dataview code:

```
where Type = "Fitness"
```

This code will tell Dataview to only display books that are listed with “Fitness” on their Type.

#### Display Books with Multiple Types ####

If you have added multiple values on the Type frontmatter (like `Type: [Fiction, Sci-Fi]`) and only want to specify one, add the following in your Dataview code:

```
where contains(Type, "Sci-Fi")
```

This will tell Dataview to display books that contains `Sci-Fi` on their Type. It will not display any books that only have `Fiction` or `[Fiction, Other Genre]` on the table.

### Create a List of Read Books ###

*A list of books read in 2021*

If you want to display a list of books that you have read in a year, add the **Date-Read** YAML frontmatter on the book note.

*A book note with the Date-Read: 2021-04-09 on the YAML frontmatter*

Go to your Library note and add the following Dataview code:

*The Dataview code used to display a list of read books in 2022.*

Here is a line by line explanation:

* `table rows.file.name as Book`
  * This tells the Dataview plugin to create a table with the row called ‘Book’ to display the files.

* `from "Library/Books"`
  * This tells the Dataview plugin to specifically display the contents from the Books folder.

* `where Status = "Read" and Date-Read >= date(2022-01-01) AND Date-Read <=date(2022-12-31)`
  * This tells the Dataview plugin to only display books with `Read` on the Status and with the year `2022` on the Date-Read.

* `group by Date-Read`
  * This will group the books according to their Date-Read metadata.

* `sort Date-Read asc`
  * This will sort the Date-Read data in ascending order.

### Display the YAML Values in Your Note ###

*The book note in both Editing Mode and Reading Mode. The Metadata list displays the YAML frontmatter values via an inline dataview query language.*

You can use an inline dataview query language (DQL) to display the values that you have added in the YAML frontmatter of your book note without manually copying them over.

The format for this code looks like this:

*The inline DQL code to display YAML values.*

Using this code allows you to view the YAML values in Reading Mode. In addition, if you make any changes to the YAML frontmatter, such as changing the Status to “Read”, the inline code will auto-update to match the value.

Download the Sample Vault
----------

I have created a sample vault of this bookshelf that includes all the files, folders, plugins, and optional features. You can find it in this [Github link](https://github.com/GentryGibson/ObsidianBookshelf).

To download and open the vault in Obsidian, follow the instructions below:

1. Click on this [Github link](https://github.com/GentryGibson/ObsidianBookshelf/releases) to take you to the download link.
2. Select the latest version of the **ObsidianBookshelf.zip** file and download it to your computer.
3. Unzip the file.
4. On Obsidian, click on the vault icon and press the Open button.
5. Select the Bookshelf folder to open it as a vault in Obsidian.

Credits
----------

If you found this helpful, consider supporting me on Ko-fi!

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/X8X8DBHQW)