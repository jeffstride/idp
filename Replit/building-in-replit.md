# Building in Replit

## Shell 
The best way to run a specific file in Replit is to use the `Shell` tab. Inside Shell, type: `python file_name.py`
![shell window](../../_static/shell_run.png)  

This allows one to easily run the tests. For example: `python hw1_test.py`  

The `shell` keeps track of your history. To access previously typed commands, hit the up-arrow. You can even move forward and backwards through the history with the up and down arrow keys. This reduces your typing immensely.  

## Setting Entrypoint
Another way to change which file you run is to modify the `.replit` file. This file is hidden in the `Config files` section that
you can't see until you click `Show hidden files`.  

To run a different file, change `.replit` in two ways:  
1) The `run` value references the file that you want to run. For example, the snippet of code below is set up to run `hw1_test.py`.  
2) The `entrypoint` value references the file you want to run.  

```bash
# The command that runs the program. If the interpreter field is set, it will have priority and this run command will do nothing
run = "python hw1_test.py"

entrypoint = "main.py"
# A list of globs that specify which files and directories should
# be hidden in the workspace.
hidden = ["venv", ".config", "**/__pycache__", "**/.mypy_cache", "**/*.pyc"]
```

## Main-Pattern
When you run a specific python file, that file should have the `main-pattern`. Here is an example
file that follows the main-pattern.

```python
'''
<Students Name Here>
<Homework Info Here>
'''

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


