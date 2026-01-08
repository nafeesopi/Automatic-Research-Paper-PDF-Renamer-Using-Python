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

Code:


pip install PyMuPDF
import fitz
import os
import re

folder = r"C:\Users\opina\Downloads\Literature _Review_Prediction"

def clean(name):
    return re.sub(r'[\\/:*?"<>|]', '', name).strip()

for f in os.listdir(folder):
    if f.lower().endswith(".pdf"):
        path = os.path.join(folder, f)

        try:
            doc = fitz.open(path)
            page = doc[0]
            blocks = page.get_text("dict")["blocks"]
            doc.close()

            font_map = {}

            for b in blocks:
                for line in b.get("lines", []):
                    for span in line.get("spans", []):
                        size = round(span["size"])
                        text = span["text"].strip()
                        if len(text) > 3:
                            font_map.setdefault(size, []).append(text)

            title = None

            for size in sorted(font_map.keys(), reverse=True):
                candidate = " ".join(font_map[size])
                if len(candidate.split()) >= 7:
                    title = candidate
                    break

            if not title:
                print("Skipped:", f)
                continue

            title = clean(title)
            new_name = title[:120] + ".pdf"
            os.rename(path, os.path.join(folder, new_name))
            print("Renamed:", f, "➡", new_name)

        except Exception as e:
            print("Error:", f)
