# How to deploy your website (no coding required)

Your site is already configured with your name, SINP affiliation, bio, all
13 journal publications, your ORCID / Google Scholar / ResearchGate / LinkedIn
links, news items, and a CV page. You just need to put these files on GitHub.

## One-time setup

1. Go to https://github.com and sign in (your username appears to be `mustak-sinp`).
2. Create a new **public** repository named EXACTLY:
       mustak-sinp.github.io
   (This special name is what makes it appear at https://mustak-sinp.github.io)
   Do NOT add a README when creating it.
3. On the new repo page, click **"uploading an existing file"**.
4. Unzip the folder I gave you, then drag ALL the files and folders into the
   upload box. Commit them (green button at the bottom).
5. In the repo, go to **Settings -> Pages**. Under "Build and deployment",
   set Source = **GitHub Actions** (not "Deploy from a branch").
6. Go to the **Actions** tab. A build will run automatically (takes 2-3 min).
   When it finishes with a green check, your site is live at:
       https://mustak-sinp.github.io

## The two things you should personalize

1. **Your photo**: replace `assets/img/prof_pic.jpg` with a headshot of yourself
   (keep the same filename). You can do this right in GitHub: open that file,
   click the trash icon to delete it, then upload your photo renamed to
   `prof_pic.jpg`.

2. **Your CV PDF** (optional): upload your CV to `assets/pdf/cv.pdf`, then edit
   `_pages/cv.md` and change the line `cv_pdf:` to `cv_pdf: /assets/pdf/cv.pdf`.
   A download button will appear automatically.

## How to edit anything later

- Bio text: edit `_pages/about.md`
- Add a publication: add a BibTeX entry to `_bibliography/papers.bib`
  (copy an existing entry and change the fields). Mark `selected = {true}`
  to feature it on the homepage.
- Add a news item: create a new file in `_news/` (copy an existing one).
- CV content: edit `_data/cv.yml`

Every time you save a change on GitHub, the site rebuilds itself in a couple
of minutes. No software to install, nothing to run on your laptop.

## Custom domain (optional, later)

If you ever want something like `mustakali.in`, buy the domain and point it at
GitHub Pages via Settings -> Pages -> Custom domain. Not required.
