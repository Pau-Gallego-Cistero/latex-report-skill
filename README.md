# Claude Skills: LaTeX University Report Generator & PDF Renderer

This repository contains two complementary "Skills" (system instructions and assets) designed for AI models like Claude. Their combined purpose is to automate the writing, typesetting, and visual rendering of Physics laboratory reports using a specific template from the Universidad Europea de Valencia (UEV).

## The Skills

This workflow is divided into two distinct system prompts:

1. **informe**: Responsible for generating the LaTeX source code (`main.tex`), organizing the structure, injecting code blocks, managing assets (logo, figures), and formatting the scientific content.
2. **renderizado-pdf**: Responsible for taking the generated `main.tex` and its assets, interpreting the LaTeX structure, and visually reconstructing it into a final PDF document without requiring a native LaTeX compiler.

## Features

- **Smart template usage:** Automatically injects the house style (`plantilla.tex`) without altering the original design.
- **Dynamic code injection:** Adds syntax highlighting support (Python or Mathematica) *only* if the report requires it, keeping the preamble clean.
- **Strict formatting control:** Forces the use of `siunitx` for units, manages indentation with `\noindent`, and properly structures figures and equations.
- **Compiler-less PDF Rendering:** Reconstructs the LaTeX document into a visually accurate PDF without relying on tools like TeX Live, MiKTeX, `pdflatex`, or `latexmk`.
- **High Visual Fidelity:** Preserves the structural layout, mathematical equations, tables, cross-references, and typography directly within the AI environment.
- **Logo Management:** Modular block to easily include or remove the university logo.

## 📂 Repository Structure

- `informe.md`: The system prompt for the LaTeX code generation skill. (Previously named system_prompt.md).
- `renderizado-pdf.md`: The system prompt for the visual PDF rendering skill.
- `assets/`: Folder containing the files the AI needs to read to build the final document.
  - `plantilla.tex`: Base template.
  - `codigo-python.tex` / `codigo-mathematica.tex`: Conditional preamble blocks.
  - `LogopequeUE.jpg`: University logo.

## 🎯 Trigger Words

To instruct Claude to activate these specific skills, use the following keywords in your chat:

### For the "informe" skill (Generation)
- **`informe`**
- **`LaTeX pdf`** (use this exact phrase; avoid using just "pdf" so Claude doesn't confuse it with generic tasks).

### For the "renderizado-pdf" skill (Rendering)
- **`renderizado`**
- **`renderiza el informe`**
- **`haz el renderizado`**
- **`renderiza el main.tex`**
*(Note: Do not trigger this step with generic "make a PDF" requests. Explicitly use the word "renderizado").*

## How to Use (Two-Step Workflow)

### In Claude Projects
1. Create a new Project in Claude.
2. Copy the content of BOTH `informe.md` and `renderizado-pdf.md` into the "Custom Instructions" section of the project (or set them up as separate tools/skills if your environment allows it).
3. Upload the `assets` folder (or its individual files) to the project's knowledge base.
4. **Step 1 (Generate):** Ask Claude: *"Haz un **informe** de mi última práctica de física cuántica, aquí tienes los resultados..."*. Claude will generate the perfect `main.tex` and prepare the assets.
5. **Step 2 (Render):** Once the `.tex` is ready, ask Claude: *"Ahora haz el **renderizado** del documento."* Claude will read the `.tex` file and output a visually accurate `main.pdf`.

### In Agent / CLI Environments
If you use the `informe` skill in a local environment with command execution capabilities, the AI might use `latexmk` to automatically compile the file. If no compiler is available, the `renderizado-pdf` skill acts as the perfect fallback to deliver the `.pdf` visually.

## How It Was Created

This skill suite was engineered with the assistance of Claude itself. By feeding the AI with many precise instructions, strict formatting rules, and the base LaTeX documents, Claude helped structure and refine the perfect system prompts. This meta-prompting approach ensures a highly robust skill that anticipates edge cases, handles conditional code formatting, and avoids common AI LaTeX hallucinations.

## 📄 License and Copyright

This project (the prompts, instructions, and `.tex` configuration files) is distributed under the [MIT License](LICENSE). You are free to use, modify, and adapt this repository for your own purposes.

**⚠️ Trademark Disclaimer:**
The `LogopequeUE.jpg` file included in the `assets/` folder contains the logo of the Universidad Europea. This logo is a registered trademark and the exclusive property of the institution. Its inclusion in this repository is for purely educational and typesetting purposes for students of said university. The logo is **NOT** covered by this repository's MIT license and must not be used for commercial purposes or outside the university scope without the express permission of the Universidad Europea.
