# api_automation_katalon

## what it is

a small Katalon Studio project from an API automation training batch (2023). it has one test: send `GET /api/users?page=2` to the public practice API https://reqres.in and check the response against a JSON schema. it is written in the Gherkin (Cucumber) style, with a thin layer of "page" test cases behind the steps. the point is the structure, not the number of tests.

stack: Katalon Studio (project created with 7.9.1), Groovy, Cucumber feature files, `WS` web-service keywords.

## when to use it

- as the first Katalon API project to read: one request, one check, every layer visible.
- when a mentor tells you to open it and trace a Gherkin step down to the HTTP call.

when not to use it:

- you want a complete, maintained Katalon API project (CRUD, login, register, local target): use https://github.com/ClasherGeek77/katalon_api_boilerplate
- you want API tests as Python code: use https://github.com/ClasherGeek77/pytest_api_boilerplate

## what you need

- Katalon Studio 7.9.1 or a newer release, free, from https://katalon.com/download . the project was created with 7.9.1 (recorded in `Object Repository/users/get_list_users.rs`); a newer Studio should open and upgrade it (not verified here). Studio asks you to sign in.
- internet access, because the target is the live site https://reqres.in .
- no browser, no other install.

## quick start, in this order

1. open the project: Katalon Studio, `File`, `Open Project`, choose `QA_API_BATCH2.prj` in this folder.
2. look at the target: `Profiles/default.glbl` defines one variable, `baseUrl = 'https://reqres.in'`.
3. run it: in the Test Explorer open `Test Suites/users`, click `Run`.

you should see one test case (`Test Cases/users/get list users`) finish as PASSED in the log viewer. not run here (Katalon Studio is a GUI application). what was checked: `curl https://reqres.in/api/users?page=2` returned HTTP 200 with the fields `page`, `per_page`, `total`, `total_pages`, `data` and `support`, which is what the schema requires.

## how to read the code, in this order

follow one scenario from the top down:

| step | file | what you learn |
| --- | --- | --- |
| 1 | `Test Suites/users` | the suite only lists one test case |
| 2 | `Test Cases/users/get list users` (script in `Scripts/users/get list users/`) | one line: run the feature file `Include/features/users.feature` with tag `@get_users` |
| 3 | `Include/features/users.feature` | the scenario in plain words: "When I send get list of users request / Then I verify the json schema of the response" |
| 4 | `Include/scripts/groovy/users/get_list_users_steps.groovy` | maps each Gherkin line to a Groovy method; the methods call test cases and keep the response in `get_list_users_data.groovy` |
| 5 | `Test Cases/pages/users/get list users` | sends the request: `WS.sendRequest(findTestObject('users/get_list_users'))` |
| 6 | `Object Repository/users/get_list_users.rs` | the request itself: GET `${baseUrl}/api/users?page=2` |
| 7 | `Test Cases/pages/users/assert get list users` | the check: `WS.validateJsonAgainstSchema(response, schema)` with a draft-04 schema where every field is required |

the pattern worth copying: the feature file says what, the step file glues, the `pages/` test cases do one thing each.

## if it breaks

| symptom | cause | fix |
| --- | --- | --- |
| schema validation fails | the response is missing a required field. the local clone https://github.com/ClasherGeek77/reqresin_clone leaves out `support` on the list endpoint (checked), and this schema requires it | keep `baseUrl` on `https://reqres.in`, or remove `"support"` from the `required` list in `Test Cases/pages/users/assert get list users` |
| connection error or HTTP 401/403 | no internet, or the public API started to require a key or blocks the caller | check `curl https://reqres.in/api/users?page=2`; use the local clone with the fix above |
| Studio cannot open the project | version mismatch, or Studio not signed in | use Studio 7.9.1, sign in |
| project does not load | you opened a subfolder instead of the project file | open `QA_API_BATCH2.prj` |
| `Profiles/staging.glbl` has no variables | it is an empty profile | ignore it, or copy `baseUrl` into it |

## next

- the modern, maintained version of this exercise: https://github.com/ClasherGeek77/katalon_api_boilerplate (six tests against a local clone, runnable from the command line).
- the same tests as code: https://github.com/ClasherGeek77/pytest_api_boilerplate
- the target API as a local clone: https://github.com/ClasherGeek77/reqresin_clone
- the rest of this training repo: https://github.com/ClasherGeek77/qa_training
