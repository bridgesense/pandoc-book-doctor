# Markdown > Pandoc Book Doctor > Publication

After making a migration from Org-Mode to MD, I needed some easy templates
that I could quickly publish into different formats. I came upon Stefano 
Cecere's 
[repository](https://github.com/StefanoCecere/markdown_pandoc_book_template) 
and was duly impressed. So was also inspired by Adam Day's 
[work](https://github.com/prosegrinder/pandoc-templates).  

However, I didn't want to lug around a bunch of custom configuration
files for everything I wanted to convert with Pandoc. Hence, my little pet
project, the Pandoc Book Doctor. 

The Pandoc Book Doctor is a single bash script that does all the heavy lifting.
With a single script, I can now take the same markup files and publish them to
a PDF, ePub or DocX file without having to maintain and alter several configurations.
A set of samples can be found in the `\examples` directory.

Besides saving me some time and grief, this script may be helpful to
those who aren't interested in the peculiarities of modifying modern Latex
just to publish their content on different platforms. If that's you, enjoy!

This project is based on the principles of GNU's copyleft mantra. So, if
you would like to share additional template ideas or would like to offer
some general improvements, please feel free to create a PR. 

## The Process 

### >> Step One - Create the Project Template 
---
Create a working template of a novel with the following: 

```
bash doctor create <directory>
```
This will create a 5.5 x 8.5 novel template. The size can be adjusted later.

### >> Step Two - Edit Configuration Files
---
First check out the newly created configuration file, `metadata.yaml`.

Here's the file structure:
```
your-book/       # Your new book directory
|- metadata.yml  # Metadata content (title, author...)
|- front-matter.tex  # Provides a custom title page, copyright, epigraph, and dedication
|- *.md          # Your book's chapter files 
|- publications/ # File output is placed here 
|- images/       # Images folder
|  |- cover.png  # Cover page for epub
```
You'll also want to review, change and add additional files as needed. Please,
keep in mind that the starting numbers of each new file are important, as this will dictate
the order in which the documents are compiled by Pandoc.

There will be a directory called `images` created in your project file. Any images you wish
to include with your project should be copied here. The standard markdown reference to images
placed in this directory would be as follows:

```
![](images/crow.jpg)
```
You may want to refer to `markdown_guide.md` for creating MD files. More information about syntax
can be found in the [basic syntax guide](https://www.markdownguide.org/basic-syntax).

### >> Step Three - Compile Your Project
---
Lastly, you'll want to compile your project into a new format. Currently, there are three available 
formats:  ePub, Manuscript(DocX) and PDF. The output will be placed in a directory called `publication`.

```
bash doctor build <directory> <epub, manuscript or pdf>
```
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