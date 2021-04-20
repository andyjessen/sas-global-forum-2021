# SGF Jupyter Notebook to PDF conversion tool

You _can_ export the Jupyter Notebooks to PDF (via LaTex) but when you do that through the notebook the styles are not applied. This tool allows us to apply the SGF paper styling from the `sugconf` latex class (with a couple of modifications for the quirks of Markdown).

This tool is comes with a user beware notice. The extent of the testing on this tool is the purest definition of "it works on my laptop".

## Requirements

This application has been built and tested on Fedora 33 but _should_ work on other platforms.

* pandoc 2.9
* python3
* pdflatex
* texlive-scheme-full (I actually don't know if basic/medium/full is required so in an abundance of caution I am stipulating full)

Python requirements can be found in `requirements.txt`. Be a good egg and use a `venv` when using this tool, per standard python good practices.

## Usage

From the command line: `python app.py`

| Argument | Description |
| -------- | ----------- |
| `--notebook-dir` or `-d` | The directory which contains the notebook and the supporting files. Use either this option OR `--markdown-file`.  |
| `--markdown-file` or `-m` | If you already have a markdown file, and you just want to make an SGF PDF. Use either this option OR `--notebook-dir`.|
| `--output-dir` or `-o` | (optional) The directory where the PDF and Tex (see --include-tex) files should be copied to. If nothing is specified, the output files are placed in the location where either the Notebook or Markdown files were found. |
| `--bibliography` or `-b` | (optional) If you have a bibliography and you want to include it. |
| `--csl` or `-c` | (optional) If you want the references to look different, you can use any valid [CSL](https://github.com/citation-style-language/styles).  |
| `--include-tex` or `-t` | (optional) For debugging, manual adjustments, etc. |


### Gitpod Example

From within the remote vscode terminal:

```bash
cd tools/notebook-to-pdf
python -m venv env
. env/bin/activate
pip install -r requirements.txt
python app.py --markdown-file ./DEMO.md
```

This will create a Markdown file called  DEMO.pdf in the `tools/notebook-to-pdf` directory. You could then create a PDF version of your own Markdown paper by running something like:

```bash
python app.py --markdown-file ../../papers/0000-2021-Smith/My_amazing_SGF_paper.md
```


## TODO

- [X] Map HTML named entities to Latex commands https://tex.stackexchange.com/questions/37126/how-can-i-map-html-named-entities-to-latex-commands
- [X] Allow someone to pass their own, or just a different, CSL.
- [X] Validate notebook metadata
- [ ] Workout how to possibly include text/html things from display_data nodes if notebook has been run  
- [ ] Make this an independent executable so that people can just download and run it if they want to.
