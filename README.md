# qa_training

## what it is

four small training projects from a QA mentoring program, one folder each. each folder keeps the full commit history of the repository it used to be. every folder has its own README with what it is, how to run it and what you should see.

| folder | what it is | stack |
| --- | --- | --- |
| https://github.com/ClasherGeek77/qa_training/tree/HEAD/api_automation_katalon | one API test: `GET /api/users?page=2` checked against a JSON schema, in Gherkin style | Katalon Studio, Groovy, Cucumber |
| https://github.com/ClasherGeek77/qa_training/tree/HEAD/web_automation_katalon | one data-driven web test: invalid login shows the expected error message, in Gherkin style | Katalon Studio, Groovy, Cucumber |
| https://github.com/ClasherGeek77/qa_training/tree/HEAD/python_assignments | an empty frame for first Python exercises (`fibonacci.py`, `main.py`) | Python 3 |
| https://github.com/ClasherGeek77/qa_training/tree/HEAD/git_mentorship | practice text files for branch, commit, pull request and conflict exercises | Git, GitHub |

these are training exercises, kept as a record. they are small on purpose: the point is the structure of each project.

## when to use it

- a mentor told you to open one of the folders.
- you want to see the smallest working shape of a Katalon API test and a Katalon web test, and trace one Gherkin step down to the HTTP or browser call.

when not to use it, go to the maintained projects:

| you want | use |
| --- | --- |
| Katalon web tests | https://github.com/ClasherGeek77/katalon_web_boilerplate |
| Katalon API tests | https://github.com/ClasherGeek77/katalon_api_boilerplate |
| Python browser tests | https://github.com/ClasherGeek77/pytest_web_boilerplate |
| Python API tests | https://github.com/ClasherGeek77/pytest_api_boilerplate |

## what you need

- Git, to clone: `git clone https://github.com/ClasherGeek77/qa_training.git`
- per folder:
  - the two Katalon folders: Katalon Studio from https://katalon.com/download and internet access (they test the live sites https://reqres.in and https://www.linkedin.com).
  - `python_assignments`: Python 3 from https://www.python.org/downloads/ .
  - `git_mentorship`: Git and a GitHub account.

## quick start, in this order

a suggested order for a new mentee:

1. `git_mentorship`: learn the branch, commit, pull request cycle you will use for everything else.
2. `python_assignments`: write a first small function and run it.
3. `api_automation_katalon`: the smallest Katalon project, one request and one check.
4. `web_automation_katalon`: the same structure with a browser and locators.

inside each folder the README gives its own order. open the project file (`QA_API_BATCH2.prj` or `QAWEBBATCH2.prj`) from Katalon Studio with `File`, `Open Project`. opening the repository root in Studio does not work, because the projects are in subfolders.

## how to read the code

- the two Katalon folders share one pattern: the feature file says what, the step file glues, the `pages/` test cases do one thing each. read the API folder first, it has one request and fewer moving parts.
- `python_assignments` and `git_mentorship` have almost no code. their value is the exercise, not the files.

## if it breaks

| symptom | cause | fix |
| --- | --- | --- |
| Studio cannot open the project | you chose the repository root, or Studio is not signed in | open the `.prj` file inside the folder, sign in |
| a Katalon test fails on a live site | the site changed its page or its data (reqres.in, LinkedIn) | see the "if it breaks" table in that folder; for stable targets use the local clones https://github.com/ClasherGeek77/reqresin_clone and https://github.com/ClasherGeek77/saucedemo_clone |
| a folder README says "not run here" | that part needs a GUI tool not available when the README was written | follow the steps and treat the "you should see" lines as expected, not guaranteed |

## next

- Katalon, maintained: https://github.com/ClasherGeek77/katalon_web_boilerplate and https://github.com/ClasherGeek77/katalon_api_boilerplate
- Python, maintained: https://github.com/ClasherGeek77/pytest_web_boilerplate and https://github.com/ClasherGeek77/pytest_api_boilerplate
- the target sites as local clones: https://github.com/ClasherGeek77/reqresin_clone (port 40000) and https://github.com/ClasherGeek77/saucedemo_clone (port 50000)
- university projects: https://github.com/ClasherGeek77/uni
- profile and all repositories: https://github.com/ClasherGeek77
