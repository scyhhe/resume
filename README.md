# Resume

LaTeX template for my personal resume

## [Available as PDF via CDN](https://cdn.statically.io/gh/scyhhe/resume/master/resume.pdf)

### Build using Docker

```docker
docker build -t latex .

docker run --rm -i -v "$PWD":/data latex latexmk resume.tex
-- or --
docker run --rm -i -v "$PWD":/data latex pdflatex resume.tex
```

### Using LaTeX Workshop VS Code extension to generate the PDF and PNG via MiKTeX

Since I decided to set this up on a Windows machine and found a few issues along the way, I wrote a small guide on how to do so.

Even if not on Windows, the provided recipes and tools can help you with generating a PDF or PNG out of your LaTeX template if you happen to be using LaTeX Workshop in VS Code, which can be useful.

#### Generating locally on a Windows Machine

1. Install [MiKTeX](https://miktex.org/)
2. Install [Perl](https://www.perl.org/get.html)
3. Install [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
   1. [GitHub Docs](https://github.com/James-Yu/LaTeX-Workshop/wiki/Compile#latex-recipes) are also available and quite helpful
4. Make sure the miktex bin folder is in your `PATH` variable
5. Add these settings for running those correctly on a Windows machine in your `settings.json`
   1. You can use either latexmk or pdflatex, they both do the same thing
   2. LaTeX Workshop will by default use the first recipe defined
6. If everything is correct, you should get an updated PDF everytime you save your `.tex` resume!
   1. For PDF generation, which is using [dvipng](https://ctan.org/pkg/dvipng) under the hood, you have to manually build the project with the corresponding `PNG` recipe found below - simply open the Command Palette and click `LaTeX Workshop: Build with recipe` and choose `PNG`

```json
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
        {
            "name": "pdfLatex",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "PNG",
            "tools": [
                "latex",
                "dvi-png"
            ]
        },
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "pdflatex",
            "command": "pdftex.exe",
            "args": [
                "-synctex=1",
                "-undump=pdflatex",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ]
        },
        {
            "name": "latex",
            "command": "latex.exe",
            "args": [
                "%DOC%"
            ]
        },
        {
            "name": "dvi-png",
            "command": "dvipng.exe",
            "args": [
                "-T=tight",
                "%DOC%.dvi"
            ]
        },
        {
            "name": "latexmk",
            "command": "latexmk.exe",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ]
        }
    ]

```
