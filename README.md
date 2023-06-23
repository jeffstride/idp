# idp : Intermediate Data Programming (Public)

# CSE 163: Intermediate Data Programming (Public)

Author: [Jeff Stride](https://www.mrstride.com/)

Contributors: xxx

This repository stores the source files for the public-facing resources for our UWHS course, CSE 163: Intermediate Data Programming.

## Note on Repo Structure

I'm looking to mimic the look and feel of the [CSE 163 GitHub Book](https://cse163.github.io/book/index.html)

## Feedback or Spot a Bug?

If you have any feedback about the book text or structure, or you spot a bug somewhere in the book, please let Mr. Stride know! The best way to contact us
is to make an [GitHub Issue](https://github.com/jeffstride/idp/issues) or to contact Mr. Stride via email, or talk to him at school.

## Contributing

This book is built with the [Sphinx Book Theme](https://sphinx-book-theme.readthedocs.io/en/latest/index.html) to generate HTML.

### Setup (Create Virtual Environment)

Create a virtual environment with Python 3.8 or higher. For example, if you use Anaconda you can launch an Anaconda command
console. CD to the root directory of this repository, and then write:

```bash
conda create --name 163-book python=3.8
conda activate 163-book
```

Install the book theme dependencies. All of these are libraries used for themes/templating in the book. `Sphinx` is the documentation templating tool, `sphinx-book-theme` 
is the specific book theme, `myst-nb` changes the Sphinx langauge from rST to MyST (more similar to Markdown), and `sphinx-thebe` allows interactive notebooks in the browser.

```bash
pip install -r requirements.txt
```

### Editing the book

The book text is stored in `book_source/source`. Each MyST file (`.md`) corresponds to a single page of the book. Some pages, like the `index.md` files for the Modules don't contain any useful information other than links. Some of the book pages are Juptyer notebooks which also get converted to HTML.

Edit the book text by editing the appropriate MyST file. See [MyST's documentation](https://myst-parser.readthedocs.io/en/latest/) for syntax examples (note: it is incredibly similar to plain markdown, with some extra macros available).

The practice problem starter code and tests live in `book_source/coding_problems`.

### Rebuilding the book

#### Step 1) Update starter code zips [optional, if changing starter code]

**If you changed starter code or tests for the practice problems, you will need to do this step first, otherwise skip to the next step** The code in `book_source/coding_problems` needs to be copied to appropriate `.zip` file in the book source. To do this, run the following Python script.

```bash
python scripts/generate_pages.py

# Or
make zips
```

#### Step 2) Build HTML output

Build the new book HTML by running (create a terminal in VS Code):

```yaml
# From the top-most directory
jupyter-book build book_source
```

This will rebuild the whole book into the `book_source/_build` directory, which might take some time depending on the change.

### Committing and pushing changes

Stage any changes to the `book_source` and push. We **do not** stage any changes to build files. Whenever we push to `main`,
GitHub Actions will build the site again and deploy it to the `gh-pages` branch. 

The GitHub actions are all established in the `.github\workflows\main.yml` file.  To get the Actions to run with permissions, 
we needed to add some configuration to the file.
```yaml
permissions:
  contents: write
```

**Special note aboute deploying:**

This will likely not matter, but is a bug we ran into a few times when setting up the book so I thought we should docunment it. 
There must be a file called `.nojekyll` in the directory wherever GitHub Pages is deployed. This file exists on the `gh-pages` branch
and should stay there by itself (i.e. add this empty `.nojekyll` file to the root of the branch). If something weird happens though, check to make sure it is still there.

When this file did not exist, then the `_static` resources were not found and the site looked like no CSS was applied.

# Notes on Development

## Working Locally
Here are some steps that I take to get things to run locally. 
1. Launch VS Code in the cse-book virtual environment.
2. In a terminal window `pip install -r requirements.txt`
3. Then, `jupyter-book build book_source` 

## Images
I have found that the only way I can get static images to deploy is to add them to the `_static` directory.
Then, the image file is copied to the `_build\html\_static` directory. The markdown will reference the image
with either: `<a href="../_static/the_image.jpg"/>` or with `![alt_text](../_static/the_image.jpg)`.

**Capitalization Matters**: The name of the image must match exactly; it is case-sensitive. You may need
to have `<a href="../_static/the_image.JPG"/>`.

## Resources
* https://github.com/executablebooks/jupyter-book/blob/master/docs/_config.yml
* https://jupyterbook.org/en/stable/customize/config.html



