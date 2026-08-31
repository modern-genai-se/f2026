# Modern GenAI in Software Development (CSCI 6907/4907)

Course site source. Fall 2026, George Washington University.

Site: https://modern-genai-se.github.io/f2026/

Built by GitHub Pages directly from the `main` branch using the
[Just the Docs](https://just-the-docs.github.io/just-the-docs/) remote theme.
No build workflow and no local Ruby install required.

## Editing

Edit the `.md` files, commit, push to `main`. The site rebuilds in about a
minute.

| File | Page |
|---|---|
| `_config.yml` | Site config. `url` and `baseurl` must match the org and repo names. |
| `index.md` | Home |
| `syllabus.md` | Syllabus |
| `schedule.md` | Schedule |
| `presentations.md` | Paper Presentations (parent page) |
| `guidance.md` | Paper Presentations > Guidance and Structure |
| `rubric.md` | Paper Presentations > Rubric |
| activities.md | Hands-On Activities (parent page) |
| activity1.md | Hands-On Activities > Activity 1 |

Nav is controlled by the front matter at the top of each file, not by folder
structure. `nav_order` sets position, `parent:` makes a page a subpage.

## Next semester

Fork this repo into a new one, update `baseurl` in `_config.yml` and the dates
in `schedule.md`.
