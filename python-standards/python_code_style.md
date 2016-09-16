# Python Code Style

##### Lint
Use pylint for finding bugs and style problems in Python source code. Run pylint over your code. Suppress warnings if they are inappropriate so that other issues are not hidden.

##### Imports
- Do not use relative names in imports. Even if the module is in the same package, use the full package name. 

**Use:**
```py
Use import x for importing packages and modules. 
Use from x import y where x is the package prefix and y is the module name with no prefix. 
Use from x import y as z if two modules named y are to be imported or if y is an inconveniently long name.
```

- For example the module `sound.effects.echo` may be imported as follows:
```py
from sound.effects import echo
echo.EchoFilter(input, output, delay=0.7, atten=4)
```

- Imports should be on separate lines.

**Use:**
```py
import os
import sys
```

**Do not Use:**
```py
import os, sys
```
- Imports are always put at the top of the file, just after any module comments and doc strings and before module globals and constants. 
- Imports should be grouped with the order being most generic to least generic:
1. standard library imports
2. third-party imports
3. application-specific imports

- Within each grouping, imports should be sorted lexicographically, ignoring case, according to each module's full package path.
```py
import foo
from foo import bar
from foo.bar import baz
from foo.bar import Quux
from Foob import bar
```

##### Packages 
Import each module using the full pathname location of the module.

**Use:**
- Reference in code with just module name
```py
from sound.effects import echo
```

##### Exceptions
- When capturing an exception, use as rather than a comma. 
**Use:**
```py
try:
  raise Error
except Error as error:
  pass
```

##### Default Argument Values
- Do not use mutable objects as default values in the function or method definition.

**Use:**
```py
def foo(a, b=None):
  if b is None:
    b = []
```

**Do not Use:**
```py
def foo(a, b=[]):
def foo(a, b=time.time()):  # The time the module was loaded???
def foo(a, b=FLAGS.my_thing):  # sys.argv has not yet been parsed
```

##### True/False evaluations
Use the `implicit` false if at all possible.

Use `is` or `is not` to compare singletons like None.
Use `if not` x to compare a boolean variable
For sequences (strings, lists, tuples), use `if not seq` to check if sequences are empty as empty sequences are false

**Use:**
```py
if not users:
  print 'no users'
```

**Do not Use:**
```py
if len(users) == 0:
  print 'no users'
```

##### Semicolons
- Do not terminate your lines with semi-colons and do not use semi-colons to put two commands on the same line.

##### Indentation
- Indent your code blocks with 2 spaces. Never use tabs or mix tabs and spaces.

##### Whitespace
- Do not use whitespace inside parentheses, brackets or braces.

**Use:** 
```py
spam(ham[1], {eggs: 2}, [])
```

**No:** 
```py
spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

- Do not use whitespace before a comma, semicolon, or colon. Do use whitespace after a comma, semicolon, or colon except at the end of the line.

**Use:**
```py
if x == 4:
  print x, y
  x, y = y, x
```
**Dont:** 
```py
if x == 4 :
  print x , y
  x , y = y , x
```

- Do not use whitespace before the open paren/bracket that starts an argument list, indexing or slicing.

**Use:**
```py
spam(1)
dict['key'] = list[index]
```
**Dont:**
```py
spam (1)
dict ['key'] = list [index]
```

- Surround binary operators with a single space on either side for assignment (=), comparisons (==, <, >, !=, <>, <=, >=, in, not in, is, is not), and Booleans (and, or, not). 

**Use:**
```py
x == 1
```

**Do not Use:**
```py
x<1
```

- Don't use spaces around the '=' sign when used to indicate a keyword argument or a default parameter value.

**Use:**
```py
def complex(real, imag=0.0): 
  return magic(r=real, i=imag)
```
**Dont:**
```py
def complex(real, imag = 0.0):
  return magic(r = real, i = imag)
```

##### Comments
Use the three double-quote `"""` (doc string) for summaries and `#` for describing a line(s) of code.
Write comment within `""" """`  if it is short. Else `"""`'Your comment here' and end the comment with `"""` in new line.

**Use:**
```py
class SampleClass(object):
  """Summary of class here.

  Longer class information....
  Longer class information....

  Attributes:
    likes_spam: A boolean indicating if we like SPAM or not.
    eggs: An integer count of the eggs we have laid.
"""

def __init__(self, likes_spam=False):
  """Inits SampleClass with blah."""
  self.likes_spam = likes_spam
  self.eggs = 0

def public_method(self):
  """Performs operation blah."""
```

##### Block and Inline Comments
**Use:**
```py
# Comment …
if i & (i-1) == 0:
```
OR
```py
if i & (i-1) == 0:        # true iff i is a power of 2
```
These comments should be at least 2 spaces away from the code.

##### Strings
Pick `'` or `"` and stick with it. It is okay to use the other quote character on a string to avoid the need to `\` escape within the string. 

##### Naming

**Use:**
```py
module_name, package_name, ClassName, method_name, ExceptionName, function_name, GLOBAL_CONSTANT_NAME, global_var_name, instance_var_name, function_parameter_name, local_var_name.
```

**Do not use**
- single character names except for counters or iterators
- dashes (-) in any package/module name
- __double_leading_and_trailing_underscore__ names (reserved by Python)

##### Main Function:
Call the main function using `if __name__ == '__main__':` This ensures main program is not executed when the module is imported.

```py
def main():
   yor main function here

if __name__ == '__main__':
    main()
```

##### Python documentation:
https://www.python.org/dev/peps/pep-0008/

##### Source:
https://google.github.io/styleguide/pyguide.html
