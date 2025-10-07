## Note

[Visit site](https://zeneral.github.io/Note/)

[GitHub](https://github.com/zeneral/Note.git)

**File structure**
```
Note/
 ├─ index.html               <- main HTML (viewer)
 ├─ index.md                 <- root index markdown
 ├─ subject1/
 │   ├─ index.md             <- subject index
 │   ├─ file1.md
 │   ├─ file2.md
 │   └─ …
 ├─ subject2/
 │   ├─ index.md
 │   └─ …
 └─ resources/
     ├─ subject_image1.png
     ├─ subject_image2.png
     └─ …
```

**Contribution Rules**:
- Create separate directory inside the `Note/` for each subject.
- Every subject should contain its own `index.md`.
- Add link of each subject at [index](Note/index.md).
- File link format `?file=subject/file.md`.
- Place all images inside `resource` directory.
- Image name format `subject_image<image number>.png`.
- Image link format `![Image][resource/subject_image1.png]`
- Keep code example consistent.
- You may create own branch and make changes.
- You may correct spelling and Grammatical mistakes


**How to run it locally?**
1. Create a directory `mkdir new` and `cd new`.
2. Clone this repository `git clone https://github.com/mini-M-py/Note.git`.
3. Start python server `python -m http.server 8000`.
4. Visit `http://localhost:8000/Note` inside the browser.

This way local server behaves same as GitHub site.
