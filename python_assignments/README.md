# python_assignments

## what it is

a starting point for Python practice in the QA training, not a finished exercise set. the folder holds two files:

| file | content |
| --- | --- |
| `fibonacci.py` | empty. this is the file a mentee fills in |
| `main.py` | one line, `import fibonacci`. it is the entry point that loads your code |

nothing else is here: no tests, no requirements file, no instructions inside the code. the task is given by the mentor, the usual first one being a function that returns Fibonacci numbers.

## when to use it

- when a mentor asks you to write a small Python function and run it from `main.py`.
- as a blank frame for the first few exercises before you touch a test framework.

when not to use it:

- you want to see real test automation in Python: use https://github.com/ClasherGeek77/pytest_web_boilerplate (browser) or https://github.com/ClasherGeek77/pytest_api_boilerplate (API)
- you want ready-made exercises with answers: none exist in this folder

## what you need

- Python 3, from https://www.python.org/downloads/ . no third-party package is used. the exact version this folder was written with is not recorded (not verified); any current Python 3 works for the two files here.

## quick start, in this order

1. open `fibonacci.py` and write your function, for example:

```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

2. open `main.py` and use it below the import:

```python
import fibonacci

print(fibonacci.fibonacci(10))
```

3. run it:

```bash
cd python_assignments
python3 main.py
```

you should see `55`. with the files exactly as they are in the repo (empty `fibonacci.py`, one-line `main.py`) the command prints nothing and exits with code 0; that was checked.

## how to read the code

- `main.py` imports `fibonacci` as a module, so both files must stay in the same folder and you must run the command from inside it.
- Python caches the imported module in `__pycache__/`; it is listed in `.gitignore`.

## if it breaks

| symptom | cause | fix |
| --- | --- | --- |
| `ModuleNotFoundError: No module named 'fibonacci'` | you ran `main.py` from another folder | `cd` into `python_assignments` first |
| `python3: command not found` (Windows) | the launcher is called `python` or `py` | use `python main.py` or `py main.py` |
| `AttributeError: module 'fibonacci' has no attribute 'fibonacci'` | the function name in `main.py` does not match the one in `fibonacci.py` | use the same name in both |
| no output at all | `fibonacci.py` is still empty, or you did not `print` the result | add the function and a `print` |

## next

- Python as real test code: https://github.com/ClasherGeek77/pytest_web_boilerplate and https://github.com/ClasherGeek77/pytest_api_boilerplate
- the same tests with Katalon and Groovy: https://github.com/ClasherGeek77/qa_training/tree/HEAD/api_automation_katalon
- the rest of this training repo: https://github.com/ClasherGeek77/qa_training
