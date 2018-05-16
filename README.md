# Python Coding Standards

## Style

Follow [PEP 8][], when sensible.


### Structure

## File, class, function length and naming

Files should ideally be less than 350 lines, classes should be less than 150 lines, functions should be less than 50 lines

If functions or classes are getting too long, consider the [single responsibility principle](https://medium.com/@graeme_boy/designing-code-using-the-single-responsibility-principle-ff4433734fdb)

If files are getting too long, consider breaking files into more functional files:

**Example**
- `models.py`

Can become

- `models/`
    - `advertisers.py`
    - `domains.py`
    - `etc`
    
Avoid circular dependencies by clearly defining the flow through the application
    
## Code flow
Short circuit when possible, avoid excessive code blocks and indentation

**Yes**
```
def foobar(cannot_be_none, var):
    if cannot_be_none is None:
        return
        
    if cannot_be_none is not var:
        return
    
    return var[cannont_be_none]
```

**No**
```
def foobar(cannot_be_none, var):
    if cannot_be_none is not None:
        if cannot_be_none is in var:
            return var[cannont_be_none]
```

### Naming

- Variables, functions, methods, packages, modules
    - `lower_case_with_underscores`
- Classes and Exceptions
    - `CapWords`
- Protected methods and internal functions
    - `_single_leading_underscore(self, ...)`
- Private methods
    - `__double_leading_underscore(self, ...)`
- Constants
    - `ALL_CAPS_WITH_UNDERSCORES`

#### General Naming Guidelines 

Avoid one-letter variables (esp. `l`, `O`, `I`). 

For very short blocks, when the meaning is clearly visible from the immediate context, use a double one-letter variable.

**Fine**
```python
for ee in elements:
    ee.mutate()
```
Avoid abbrevations (passwd vs password, adm vs admin, etc)

Avoid redundant labeling.

**Yes**
```python
import audio

core = audio.Core()
controller = audio.Controller()
```

**No**
```python
import audio

core = audio.AudioCore()
controller = audio.AudioController()
```

Prefer "reverse notation".

**Yes**
```python
elements = ...
elements_active = ...
elements_defunct = ...
```

**No**
```python
elements = ...
active_elements = ...
defunct_elements ...
```

Avoid getter and setter methods.

**Yes**
```python
person.age = 42
```

**No**
```python
person.set_age(42)
```

#### Indentation

Use 4 spaces--never tabs. Enough said.

#### Imports

Import entire modules instead of individual symbols within a module. For example, for a top-level module `canteen` that has a file `canteen/sessions.py`,

**Yes**

```python
import canteen
import canteen.sessions
from canteen import sessions
```

**No**

```python
from canteen import get_user  # Symbol from canteen/__init__.py
from canteen.sessions import get_session  # Symbol from canteen/sessions.py
```

*Exception*: For third-party code where documentation explicitly says to import individual symbols.

*Rationale*: Avoids circular imports. See [here](https://sites.google.com/a/khanacademy.org/forge/for-developers/styleguide/python#TOC-Imports).

Put all imports at the top of the page with three sections, each separated by a blank line, in this order:

1. System imports
2. Third-party imports
3. Local source tree imports

*Rationale*: Makes it clear where each module is coming from.


### Django specific standards

## Models
Models should contain the majority of the business logic

## Views
Views should be as simple as possible, they should parse the input from the url and handle any permissions, but after that should just call into a 'service'

## Urls
TBD
