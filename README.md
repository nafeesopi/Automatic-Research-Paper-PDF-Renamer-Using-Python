## 📝 Description

This Python project automatically scans a folder of research paper PDFs, intelligently extracts the real paper titles from the first page using font-size detection, and renames each file accordingly.

The system reads PDF layout structure, detects the largest font text containing at least seven words, and uses it as the paper title — just like how a human identifies a research title. This is extremely useful for organizing large literature review folders.

### 🚀 Features

* Automatically processes all PDFs in a folder
* Detects true research titles using font-size intelligence
* Handles noisy layouts and formatting issues
* Cleans invalid filename characters
* Works perfectly inside Jupyter Notebook

### 🛠 Technologies

* Python
* PyMuPDF (fitz)
* OS & Regex modules

### 🎯 Use Case

Perfect for students, researchers, and academicians who want to clean and organize hundreds of downloaded research papers with correct titles automatically.
