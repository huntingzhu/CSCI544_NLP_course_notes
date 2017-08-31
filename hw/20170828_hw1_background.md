# HW1 Limerick

## 1 Terminologies

### 1.1 Limerick

A limerick is a form of poetry in five-line, predominantly anapestic meter with a strict rhyme scheme (AABBA), often humorous and sometimes obscene. The third and fourth lines are shorter than the other three. The following example is a limerick of unknown origin:

```
    The limerick packs laughs anatomical
    Into space that is quite economical.
    But the good ones I've seen
    So seldom are clean
    And the clean ones so seldom are comical.
```
The standard form of a limerick is a stanza of five lines, with the first, second and fifth rhyming with one another and having three feet of three syllables each; and the shorter third and fourth lines also rhyming with each other, but having only two feet of three syllables.

### 1.2 Syllable

A syllable is a unit of organization for a sequence of speech sounds. For example, the word water is composed of two syllables: wa and ter. A syllable is typically made up of **a syllable nucleus (most often a vowel)** with optional initial and final margins (typically, consonants).

### 1.3 Rhyme

To recap, if we consider these rules as a pronunciation normalization, the original and **preferred definition** is:

- Starting with the beginning of the pronunciation, throw out sounds until the first vowel is reached

The alternate definition is:

- Starting with the beginning of the pronunciation, throw out sounds until the first consonant is reached, then continue throwing out sounds until the next vowel is reached...unless there are no consonants reached, in which case do not throw out anything

Both these definitions, if **implemented correctly with everything else**, will result in full credit in the tests.

## 2 sys

### 2.1 sys.version_info
```python
import sys
print sys.version_info
# Result: sys.version_info(major=2, minor=7, micro=13, releaselevel='final', serial=0)
```

## 3 argparse

### 3.1 ArgumentParser objects

class argparse.ArgumentParser(prog=None, usage=None, description=None, epilog=None, parents=[], formatter_class=argparse.HelpFormatter, prefix_chars=’-‘, fromfile_prefix_chars=None, argument_default=None, conflict_handler=’error’, add_help=True, allow_abbrev=True)

Create a new ArgumentParser object. All parameters should be passed as keyword arguments. Each parameter has its own more detailed description below, but in short they are:

- prog - The name of the program (default: sys.argv[0])
- usage - The string describing the program usage (default: generated from arguments added to parser)
- **description** - Text to display before the argument help (default: none)
- epilog - Text to display after the argument help (default: none)
- parents - A list of ArgumentParser objects whose arguments should also be included
- **formatter_class** - A class for customizing the help output
- prefix_chars - The set of characters that prefix optional arguments (default: ‘-‘)
- fromfile_prefix_chars - The set of characters that prefix files from which additional arguments should be read (default: None)
- argument_default - The global default value for arguments (default: None)
- conflict_handler - The strategy for resolving conflicting optionals (usually unnecessary)
- add_help - Add a -h/--help option to the parser (default: True)
- allow_abbrev - Allows long options to be abbreviated if the abbreviation is unambiguous. (default: True)

### 3.2 The add_argument() method

ArgumentParser.add_argument(name or flags…[, action][, nargs][, const][, default][, type][, choices][, required][, help][, metavar][, dest])

- **name or flags** - Either a name or a list of option strings, e.g. foo or -f, --foo.
  ```python
  >>> parser = argparse.ArgumentParser(prog='PROG')
  >>> parser.add_argument('-f', '--foo')
  >>> parser.add_argument('bar')
  >>> parser.parse_args(['BAR'])
  Namespace(bar='BAR', foo=None)
  >>> parser.parse_args(['BAR', '--foo', 'FOO'])
  Namespace(bar='BAR', foo='FOO')
  >>> parser.parse_args(['--foo', 'FOO'])
  usage: PROG [-h] [-f FOO] bar
  PROG: error: too few arguments
  ```
- **action** - The basic type of action to be taken when this argument is encountered at the command line.
  ```python
  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('--foo', action='store_true')
  >>> parser.add_argument('--bar', action='store_false')
  >>> parser.add_argument('--baz', action='store_false')
  >>> parser.parse_args('--foo --bar'.split())
  Namespace(foo=True, bar=False, baz=True)
  ```
- **nargs** - The number of command-line arguments that should be consumed.
  ```python
  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('infile', nargs='?', type=argparse.FileType('r'), default=sys.stdin)
  >>> parser.add_argument('outfile', nargs='?', type=argparse.FileType('w'), default=sys.stdout)
  >>> parser.parse_args(['input.txt', 'output.txt'])
  Namespace(infile=<_io.TextIOWrapper name='input.txt' encoding='UTF-8'>,
            outfile=<_io.TextIOWrapper name='output.txt' encoding='UTF-8'>)
  >>> parser.parse_args([])
  Namespace(infile=<_io.TextIOWrapper name='<stdin>' encoding='UTF-8'>,
            outfile=<_io.TextIOWrapper name='<stdout>' encoding='UTF-8'>)
  ```
- const - A constant value required by some action and nargs selections.
- **default** - The value produced if the argument is absent from the command line.
  ```python
  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('--length', default='10', type=int)
  >>> parser.add_argument('--width', default=10.5, type=int)
  >>> parser.parse_args()
  Namespace(length=10, width=10.5)
  ```
- **type** - The type to which the command-line argument should be converted.
  ```python
  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('foo', type=int)
  >>> parser.add_argument('bar', type=open)
  >>> parser.parse_args('2 temp.txt'.split())
  Namespace(bar=<_io.TextIOWrapper name='temp.txt' encoding='UTF-8'>, foo=2)
  ```
- choices - A container of the allowable values for the argument.
- required - Whether or not the command-line option may be omitted (optionals only).
- help - A brief description of what the argument does.
  ```python
  >>> parser = argparse.ArgumentParser(prog='frobble')
  >>> parser.add_argument('bar', nargs='?', type=int, default=42, help='the bar to %(prog)s (default: %(default)s)')
  >>> parser.print_help()
  usage: frobble [-h] [bar]

  positional arguments:
   bar     the bar to frobble (default: 42)

  optional arguments:
   -h, --help  show this help message and exit
  ```
- metavar - A name for the argument in usage messages.
- **dest** - The name of the attribute to be added to the object returned by parse_args().
  ```python
  >>> parser = argparse.ArgumentParser()
  >>> parser.add_argument('--foo', dest='bar')
  >>> parser.parse_args('--foo XXX'.split())
  Namespace(bar='XXX')
  ```
## 4 nltk

### 4.1 Install

1. install pip
2. Install NLTK: run sudo pip install -U nltk
3. Install Numpy (optional): run sudo pip install -U numpy
4. Test installation: run python then type import nltk
5. open a python shell, download the cmudict:
  ```python
  >>> import nltk
  >>> nltk.download()
  ```

### 4.2 A Pronouncing Dictionary
A slightly richer kind of lexical resource is a table (or spreadsheet), containing a word plus some properties in each row. NLTK includes the CMU Pronouncing Dictionary for US English, which was designed for use by speech synthesizers.

Examples:
```python
>>> prondict = nltk.corpus.cmudict.dict()
>>> prondict['fire']
[['F', 'AY1', 'ER0'], ['F', 'AY1', 'R']]
>>> prondict['blog']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'blog'
>>> prondict['blog'] = [['B', 'L', 'AA1', 'G']]
>>> prondict['blog']
[['B', 'L', 'AA1', 'G']]
```
