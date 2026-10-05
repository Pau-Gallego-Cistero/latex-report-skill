---
name: informe
description: "Writes university lab/practice reports in LaTeX using Pau's Universidad Europea de Valencia (Grado en Física) template, with logo, title page, coloured headings, figures, equations and references. Trigger words are \"informe\" and \"LaTeX pdf\" (the exact phrase; do not trigger on a bare \"pdf\"). Use this skill when the user says \"informe\", \"LaTeX pdf\", or asks for a report written as a .tex file from an assignment, results or a draft. Do not use for generic PDF tasks (reading, merging, filling or editing PDFs): those belong to the pdf skill."
---

# informe — LaTeX report skill

Produces a ready-to-compile report from the user's own template. Do not redesign the look: `assets/plantilla.tex` is the user's house style.

## Workflow

1. **Collect inputs.** From the message and attached files, find: assignment text/questions, results, figures, any existing .tex draft, and whether the report needs code. Ask at most one short question, only if something essential is missing (for example subject or title). Use the template defaults for author, university and degree.
2. **Copy the template.** Copy `assets/plantilla.tex` to `main.tex` and `assets/LogopequeUE.jpg` next to it. Edit only the configuration block at the top (`\asignatura`, `\titulo`, `\autor`, `\universidad`, `\grado`). Never hardcode the subject or title elsewhere.
3. **Code: only if needed.** The base template has no code support on purpose (no `listings` package, no code styles). Add code support only when the report really contains code:
   - Python code: paste the contents of `assets/codigo-python.tex` into the preamble, right before `\begin{document}`, and use `\begin{lstlisting}[language=Python]`.
   - Mathematica code: paste `assets/codigo-mathematica.tex` the same way, and use `\lstset{style=mathematicaStyle}` before the listing.
   - Both languages: paste both files.
   - No code in the report: add nothing, and mention no code environments. Never include code just to fill space; a result that can be stated with an equation, table or figure should be.
4. **Fill the sections** in this order: Summary and objectives, Principles, Questions, Conclusions, References. Keep the user's own wording, code and numbers; improve structure and clarity without inventing results.
5. **Compile** with `latexmk -pdf -interaction=nonstopmode main.tex` (twice if the table of contents is empty). Fix errors and undefined references. If `pdflatex` is missing, deliver the .tex and say so.
6. **Deliver** the `.tex`, the logo and the PDF (if it compiled) with `present_files`. Mention any figure files the user must place in `Figures/`.

## Logo block (keep it easy to find and remove)

The UEV logo lives in one contiguous block of `plantilla.tex`, between the banner lines `LOGO UEV - INICIO` and `LOGO UEV - FIN`, with comments explaining what it does and how to remove, replace or move it. Rules:
- Keep that block self-contained (it loads `eso-pic` and defines `\logo` itself) and keep all of its comments. Never spread logo code to other parts of the file.
- If the user asks for a report without the logo, delete everything between the two banner lines and do not ship the .jpg.

## Indentation rule: `\noindent`

Every piece of body text that starts a new line of text after a `\section`/`\subsection` heading, or after a `\\` line break, begins with `\noindent`, so the text is aligned consistently with no stray indentation. Example:

```latex
\section{Principles}
\noindent
The system is governed by ...

Second line of the block.\\
\noindent Next sentence after a line break.
```

Check this on the whole document before delivering, including text the user pasted.

## Style rules

- **Language:** write the report in the language of the assignment (the user's course is in English). Never mix languages inside one report; if the draft is mixed, ask which to keep or unify to the dominant one.
- **Questions:** each one goes in `\pregunta{...}`, followed by the figure, equation or table that answers it, and a short written answer (plus code only if the report needs it, see step 3).
- **Figures:** `[H]`, width about `0.55\textwidth`, saved in `Figures/`, with a descriptive caption that includes units. Never leave a caption empty.
- **Maths:** numbered `equation` for results that are referenced, inline `$...$` otherwise. Units with `siunitx` (`\SI{3}{\electronvolt}`, `\si{\angstrom}`), never plain text.
- **Numbers:** values with units and a sensible number of significant figures; include uncertainties when the data has them.
- **References:** `thebibliography` entries with author, year, title and URL or source. Do not invent references; use only ones the user gave or that were actually found.

## Pre-delivery check

Before delivering, scan for: empty captions, typos in title or subject, missing `\noindent` after sections or `\\`, code environments in a report that has no code, unconverted units (for example SI quantities mixed with eV or Å), constants set by hand that should be computed, text left in another language, leftover template placeholders, and figures referenced but missing. Fix what is clearly wrong in the LaTeX; for scientific or numerical problems in the user's own code or results, report them in a short list instead of silently changing them.
