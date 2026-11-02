*This project has been created as part of the 42 curriculum by scamlett.*

# Python Module 06: The Alchemy of Imports

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![42](https://img.shields.io/badge/42-Málaga-000000)

## Description

A module about how Python finds and loads code: modules, packages,
`__init__.py`, absolute and relative imports, and what goes wrong with
circular imports. Everything is wrapped in an alchemy theme: elements,
potions, a transmutation recipe and a grimoire of light and dark spells.

```
elements.py                  create_fire, create_water (top-level module)
alchemy/
├── __init__.py              chooses what `import alchemy` exposes
├── elements.py              create_earth, create_air
├── potions.py               mixes both elements modules
├── transmutation/recipes.py relative imports with `..`
└── grimoire/                light and dark spellbooks + validators
```

| Scripts | Topic |
|---------|-------|
| `ft_alembic_0.py` to `ft_alembic_5.py` | Six ways to import the same thing: `import x`, `from x import y`, `import pkg.mod`, `from pkg import mod`, and what `import pkg` alone gives you |
| `ft_distillation_0.py`, `ft_distillation_1.py` | Aliases (`healing_potion as heal`) and names re-exported from `__init__.py` |
| `ft_transmutation_0.py` to `ft_transmutation_2.py` | Reaching a function through a sub-package and relative imports (`from ..potions import ...`) |
| `ft_kaboom_0.py`, `ft_kaboom_1.py` | Circular imports: one way that works, and one that fails on purpose |

## Instructions

Run every script from the repository root, so that both `elements.py` and
the `alchemy` package can be found:

```bash
python3 ft_alembic_0.py
python3 ft_transmutation_2.py
python3 ft_kaboom_1.py   # raises an ImportError on purpose
```

Two scripts are meant to fail: `ft_alembic_4.py` shows that `import alchemy`
only exposes what `__init__.py` imports, and `ft_kaboom_1.py` shows a
circular import between `dark_spellbook` and `dark_validator`.

## What I learned

- A module is a `.py` file and a package is a folder with an `__init__.py`
- `__init__.py` decides the public face of a package: anything it does not
  import is not reachable as `alchemy.something`
- Absolute imports start from the project root, relative imports (`.`, `..`)
  start from the current package
- Python searches `sys.path`, which starts with the folder of the script you
  run, so where you run from matters
- Two modules importing each other at the top level crash with "partially
  initialized module". Moving one import inside the function that needs it
  (as `light_validator.py` does) breaks the cycle
