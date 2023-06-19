# Building in Replit

Helpful links:
* [Using Nix with Replit](https://docs.replit.com/programming-ide/nix-on-replit)
* [Building with Nix on Replit](https://docs.replit.com/tutorials/python/build-with-nix)

You'll want to change which file you build so that you can run either your functional code or your tests.
To do this, you'll want to modify the `.replit` file which is hidden in the `Config files` section that
you can't see until you `Show hidden files`.  

To run a different file, change `.replit` so that both the `run` and `entrypoint` values are what you 
want them to be. For example, the snippet of code below is set up to run `hw1_test.py`.

```bash
run = "python hw1_test.py"

entrypoint = "hw1_test.py"
# A list of globs that specify which files and directories should
# be hidden in the workspace.
hidden = ["venv", ".config", "**/__pycache__", "**/.mypy_cache", "**/*.pyc"]
```

When you run a specific python file, that file should have the `main-pattern`. Here is an example
file that follows the main-pattern.

```python
# <Students Name Here>
# <Homework Info Here>


def problem_0(arg)
    '''
    problem_0 will take an integer argument and print it.
    '''
    print(arg)


def main():
    problem_0(5)


if __name__ == '__main__':
    main()
```