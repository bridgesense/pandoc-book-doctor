# Markdown > Pandoc Book Doctor > Publication

After migrating my writing workflow from Org-Mode to Markdown, I needed a more 
straightforward process for quickly publishing the files into different formats. 
I came across Stefano Cecere's 
[repository](https://github.com/StefanoCecere/markdown_pandoc_book_template) 
and was duly impressed. I was also inspired by Adam Day's 
[work](https://github.com/prosegrinder/pandoc-templates). 

I knew I didn't want to lug around a bunch of custom configuration files for every 
project I tried to convert with Pandoc. Hence, my little pet project was named the 
Pandoc Book Doctor. 

The Pandoc Book Doctor is a single bash script that does all the heavy lifting.
I can publish my markup files to a PDF, ePub, or DOCX file without maintaining and 
altering several configurations. A set of sample conversions can be found in the 
`\examples` directory.

Besides saving me some time and grief, this script may be helpful to
those who aren't interested in the peculiarities of modifying modern Latex. There are
a lot of great templates out there if you like Latex. Unfortunately, none of this helps 
mediate between Markdown and Pandocs.

Markdown certainly isn't as extensive as Latex for rendering concepts precisely as 
envisioned, but that's why Markdown is everywhere, and Latex isn't. This script
has already made friends with Latex to make this process less daunting.

This project is based on the principles of GNU's copyleft mantra. So, if you 
need to share, steal or modify this script--go for it. If you are a nerd and decide 
to send me a PR, just know that I still love you; I might not be so fast to reply.

_Come to think of it;_ I hear Microsoft loves the fact that thousands of copies of 
the same repositories *are copied all over their database*. :D 
## The Process 

### >> Step One - Create the Project Template 
---
Create a working template of a novel with the following: 

```
bash doctor create <directory>
```
This command will create a 5.5 x 8.5 novel template. The size can easily be adjusted 
later.

### >> Step Two - Edit Configuration Files
First, check out where everything is in the newly created files, specifically: 
`metadata.yaml` and `front-matter.tex`. Then, note how the information in these 
files is referenced during each conversion.

The `front-matter.tex` is only used when producing a pdf file. When producing ePub documents, *all
latex* will be ignored. That is why some of the text from `front-matter.tex` is also present
in the `metadata.yaml` configuration file. The section under "rights" does not output to pdf,
but it does to ePub.

Here's a fair warning about exporting to a manuscript. I haven't made friends yet with the DOCX 
template yet. The template I discovered *and robbed* from Adam Day's
[repository](https://github.com/prosegrinder/pandoc-templates) is already mostly there,
even without all the crazy lua. In the future, I may add character counts and try to
autofill some of the missing header data. Until then, a few quick runs with search/replace
should set the document up nicely. 

Here's the file structure:
```
your-book/       # the new book directory
|- metadata.yml  # Metadata content (title, author...)
|- front-matter.tex  # (pdf only) title page, copyright, epigraph, and dedication
|- *.md          # the book's chapter files 
|- publications/ # File output is placed here 
|- images/       # Images folder
|  |- cover.png  # Cover page for epub
```
You'll also want to review, change and add additional files as needed. Please remember 
that the starting numbers of each new file are essential, as this will dictate the order 
in which Pandoc compiles the documents.

There will be a directory called `images` created in your project file. Any images you wish
to include with your project should be copied here. The standard markdown reference to images
placed in this directory would be as follows:

```
![](images/crow.jpg)
```
You may want to refer to `markdown_guide.md` for creating MD files. More information about syntax
can be found in the [Markdown syntax guide](https://www.markdownguide.org/basic-syntax).

### >> Step Three - Compile Your Project
---
Lastly, you'll want to compile your project into a new format. Currently, there are three available 
formats:  ePub, Manuscript(DOCX), and PDF. The output is always generated inside the `publication` 
directory.

```
bash doctor convert <directory> <epub, manuscript or pdf>
```
## Working with Your Project 
A repository is an excellent tool for saving changes while writing and editing a novel. 

After each writing session, commit the changes using a tool like [Lazygit](https://github.com/jesseduffield/lazygit). Lazygit comes
with some very nice features for reviewing all the save points in a project's history.

Also, check out [LazyVim](https://www.lazyvim.org/). If Lazygit is installed, LazyVim will automatically integrate 
the tool into your workflow. Just hit <space>gg to get started. A tutorial is available 
[here](https://youtu.be/CPLdltN7wgE).

Finally, you can easily add [Grammarly](https://www.grammarly.com/) to your LazyVim configuration, turning it into a 
powerful content editor. I use the [Mason Tool Installer](https://github.com/WhoIsSethDaniel/mason-tool-installer.nvim) to 
set up Grammarly in LazyVim.

<details>
<summary>LazyVim Plugin Lua</summary>

```
return {
  "WhoIsSethDaniel/mason-tool-installer.nvim",

  opts = {
    { "grammarly-languageserver", auto_update = true },
    auto_update = true,
    run_on_start = true,
    start_delay = 3000,
    debounce_hours = 5,
  },
}
```
</details>

## Requirements
---
- Install the latest version of Pandoc: [Installing Pandoc](https://pandoc.org/installing.html).
- Install a LaTeX distribution: [Installing TeX Live](https://www.tug.org/texlive/)

These can also be installed through the Ubuntu repository:
```
sudo apt-get install pandoc texlive-full
```
You also need to install the pandoc-latex-extensions.

```
pip install git+https://github.com/tbsexton/pandoc-latex-extensions.git@patch-1 --user
```
