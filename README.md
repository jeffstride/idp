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

### Setup (TODO: needs updating)

Create a virtual environment with Python 3.8 or higher. For example, if you use Anaconda you can write:

```bash
conda create --name 163-book python=3.8
conda activate 163-book
```

Install the book theme dependencies. All of these are libraries used for themes/templating in the book. `Sphinx` is the documentation templating tool, `sphinx-book-theme` 
is the specific book theme, `myst-nb` changes the Sphinx langauge from rST to MyST (more similar to Markdown), and `sphinx-thebe` allows interactive notebooks in the browser.

```bash
pip install -r requirements.txt
```

### Editing the book (TODO: needs updating)

The book text is stored in `docs`. Each MyST file (`.md`) corresponds to a single page of the book. Some pages, like the `index.md` files for the 
Modules don't contain any useful information other than links.

Edit the book text by editing the appropriate MyST file. See [MyST's documentation](https://myst-parser.readthedocs.io/en/latest/) for syntax examples 
(note: it is incredibly similar to plain markdown, with some extra macros available).


### Committing and pushing changes

Whenever we push to `main` branch, GitHub Actions will build the site again and deploy it to the `gh-pages` branch.

**Special note aboute deploying:**

This will likely not matter, but is a bug we ran into a few times when setting up the book so I thought we should docunment it. T
here must be a file called `.nojekyll` in the directory wherever GitHub Pages is deployed. This file exists on the `gh-pages` branch
and should stay there by itself. If something weird happens though, check to make sure it is still there.
