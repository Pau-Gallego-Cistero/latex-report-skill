# 🎓 Claude Skill: LaTeX University Report Generator

This repository contains a "Skill" (system instructions and assets) designed for AI models like Claude. Its purpose is to automate the writing and typesetting of Physics laboratory reports in LaTeX, using a specific template from the Universidad Europea de Valencia (UEV).

## Features

- **Smart template usage:** Automatically injects the house style (`plantilla.tex`) without altering the original design.
- **Dynamic code injection:** Adds syntax highlighting support (Python or Mathematica) *only* if the report requires it, keeping the preamble clean.
- **Strict formatting control:** Forces the use of `siunitx` for units, manages indentation with `\noindent`, and properly structures figures and equations.
- **Logo Management:** Modular block to easily include or remove the university logo.

## 📂 Repository Structure

- `system_prompt.md`: The main prompt you should provide to the AI (Ideal for Claude Projects or Custom GPTs).
- `assets/`: Folder containing the files the AI needs to read to build the final document.
  - `plantilla.tex`: Base template.
  - `codigo-python.tex` / `codigo-mathematica.tex`: Conditional preamble blocks.
  - `LogopequeUE.jpg`: University logo.

## How to Use

### In Claude Projects
1. Create a new Project in Claude.
2. Copy the content of `system_prompt.md` into the "Custom Instructions" section of the project.
3. Upload the `assets` folder (or its individual files) to the project's knowledge base.
4. Ask Claude: *"Write a report for my latest quantum physics lab, here are the results..."* and watch it generate the perfect `.tex` file.

### In Agent / CLI Environments
If you use this skill in a local environment with command execution capabilities, the AI will use `latexmk` to automatically compile the file and deliver the final `.pdf`.

## 📄 License and Copyright

This project (the prompts, instructions, and `.tex` configuration files) is distributed under the [MIT License](LICENSE). You are free to use, modify, and adapt this repository for your own purposes.

**⚠️ Trademark Disclaimer:**
The `LogopequeUE.jpg` file included in the `assets/` folder contains the logo of the Universidad Europea. This logo is a registered trademark and the exclusive property of the institution. Its inclusion in this repository is for purely educational and typesetting purposes for students of said university. The logo is **NOT** covered by this repository's MIT license and must not be used for commercial purposes or outside the university scope without the express permission of the Universidad Europea.
