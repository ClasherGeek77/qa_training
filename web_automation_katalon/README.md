# web_automation_katalon

## what it is

a small Katalon Studio project from a web automation training batch (2023). it has one data-driven test: open a login page, type an invalid email and password, click login, and check that the page shows the expected error text. it is written in the Gherkin (Cucumber) style with a thin layer of "page" test cases behind the steps. the point is the structure and the locators, not the number of tests.

stack: Katalon Studio, Groovy, Cucumber feature files, `WebUI` keywords, XPath locators in the Object Repository.

the scenario (`Include/features/login/login.feature`) is a `Scenario Outline` with two examples:

| email | password | message expected on the page |
| --- | --- | --- |
| `name1@gmail.coms` | `pass123` | `We don't recognize that email` |
| `name1@gmail.com` | `pass143` | `not the right password` |

## when to use it

- as a first Katalon web project to read: one flow, every layer visible (feature file, steps, page test cases, locators, profile).
- when a mentor tells you to open it and trace a Gherkin step down to the browser call.

when not to use it:

- you want a complete, maintained Katalon web project with a target that does not change: use https://github.com/ClasherGeek77/katalon_web_boilerplate
- you want web tests as Python code: use https://github.com/ClasherGeek77/pytest_web_boilerplate
- you want a stable practice site: use the local clone https://github.com/ClasherGeek77/saucedemo_clone (runs on port 50000)

## what you need

- Katalon Studio, free, from https://katalon.com/download . the project file name and layout come from Studio 7.x or 8.x; the exact Studio version is not recorded in this folder, so a version is not verified here. Studio asks you to sign in.
- internet access, because the target is the live site https://www.linkedin.com (`baseUrl` in `Profiles/default.glbl`).
- Chrome or another browser that Katalon supports.

## quick start, in this order

1. open the project: Katalon Studio, `File`, `Open Project`, choose `QAWEBBATCH2.prj` in this folder.
2. look at the target: `Profiles/default.glbl` defines `baseUrl = 'https://www.linkedin.com'`, `waitFast = 5` and `waitSlow = 15` (seconds).
3. run it: in the Test Explorer open `Test Suites/login`, pick a browser, click `Run`.

you should see a browser open the page `https://www.linkedin.com/checkpoint/lg/sign-in-another-account`, type the two credentials, click the sign-in button and finish with two PASSED rows (one per example) in the log viewer. not run here (Katalon Studio is a GUI application, and the target is a live third-party site, see "if it breaks").

## how to read the code, in this order

follow one scenario from the top down:

| step | file | what you learn |
| --- | --- | --- |
| 1 | `Test Suites/login` | the suite lists one test case, `Test Cases/login/login` |
| 2 | `Test Cases/login/login` (script in `Scripts/login/login/`) | one line: run `Include/features/login/login.feature` with tag `@scenarioLogin` |
| 3 | `Include/features/login/login.feature` | the scenario in plain words, with the two example rows |
| 4 | `Include/scripts/groovy/login/login.groovy` | maps each Gherkin line to a method; each method calls one page test case and passes values in as variables (`emailTC`, `passwordTC`, `status`) |
| 5 | `Test Cases/pages/login/go to login page` | `WebUI.openBrowser(GlobalVariable.baseUrl + '/checkpoint/lg/sign-in-another-account')` |
| 6 | `Test Cases/pages/login/type email and password login` | `WebUI.sendKeys` on `login/ipt_email` and `login/ipt_pass` |
| 7 | `Test Cases/pages/login/click login` | waits until `login/btn_login` is clickable (`waitFast`), then clicks |
| 8 | `Test Cases/pages/login/verify status message login failed` | `WebUI.verifyElementVisible` on `login/txt_login_validation_msg_dynamic`, filled with the expected text |
| 9 | `Object Repository/login/*.rs` | the locators, all XPath (see below) |

the locators:

| object | XPath |
| --- | --- |
| `ipt_email` | `//input[@id='username']` |
| `ipt_pass` | `//input[@id='password']` |
| `btn_login` | `//button[@data-litms-control-urn='login-submit']` |
| `txt_login_validation_msg_dynamic` | `//*[contains(text(), "${statusOB}")]` (a parameter, so one object serves both error messages) |

the pattern worth copying: the feature file says what, the step file glues, the `pages/` test cases do one thing each, and one dynamic locator replaces many near-identical ones.

things to notice and discuss:

- no test case calls `WebUI.closeBrowser()`, so the browser is left to the suite settings.
- the project file `QAWEBBATCH2.prj` records a Windows path (`projectFileLocation`); Studio ignores it when you open the project from another place.

## if it breaks

| symptom | cause | fix |
| --- | --- | --- |
| a step fails with element not found on `login/ipt_email` | the live site changed its page, a captcha or a different sign-in page was served, or the site blocks automated browsers | open the page by hand, inspect the field, update the XPath in `Object Repository/login/`; this is expected over time with a live third-party site |
| the message check fails but the steps before pass | the site wording changed | change the text in the `Examples` table of `login.feature` |
| nothing happens or no internet error | no connection | check that https://www.linkedin.com opens in the same browser |
| Studio cannot open the project | version mismatch, or Studio not signed in | use a current Studio, sign in |
| project does not load | you opened a subfolder instead of the project file | open `QAWEBBATCH2.prj` |

## next

- the maintained version of this exercise: https://github.com/ClasherGeek77/katalon_web_boilerplate
- the same kind of tests as code: https://github.com/ClasherGeek77/pytest_web_boilerplate
- a stable local site to practice on: https://github.com/ClasherGeek77/saucedemo_clone
- the API exercise from the same training: https://github.com/ClasherGeek77/qa_training/tree/HEAD/api_automation_katalon
- the rest of this training repo: https://github.com/ClasherGeek77/qa_training
