# Unit testing with Pytest

https://www.youtube.com/watch?v=bbp_849-RZ4

## testing frameworks for python
* unittest - included in python std
* nose - simpler test
* pytest 

## options
* `-v` verbose output, test by test rather than file by file
* `-k "add"` run only tests which have the word add in the function name. can use conditionals in string "add and string"
* `-m my_mark` runs only tests which have the decorator `@pytest.mark.my_mark`. 
* `-x` exit on first fail
* `--tb=no` don't show stack traces for fails
* `--maxfail=2` exit on 2 fails
* `-s` print output using print function in the functions
* `-q` quiet mode, just info about number of tests run

## test syntax

start your file name with _test_
```python
import the_module_you_are_testing

def test_add_two_numbers():
  assert math_func.add(7, 3) == 10
```

your test function must start with test

to run `pytest test_file_name.py`

you can also use `py.test`, which will run any files with the test prefix

you can run a specific test with `pytest file::function`

## skipping
* `@pytest.mark.skip(reason="why to skip)` is a special mark, which will always be skipped. the option `-rsx` will show why it 
* `@pytest.mark.skipif(sys.versioninfo < (3, 3), reason="why to skip)`

## parameterise

* more tests is good, but sometimes you want to call the same function multiple times. 
*

```python
@pytest.mark.parameterize('num1, num2, result',
                              [
                                (7,3,10),
                                ('hello', 'world', 'hello world'),
                                (10.5, 25.5, 36)
                                ]
                                )
def test_add(num1, num2, num3):
  assert math_func.add(num1, num2) == result
```

## fixtures
* when you want to create/instatiate objects/data resources which will get used throughout your test suite 
* you can use it to replace 'setup' and 'teardown' methods in standard library.

```python
@pytest.fixture(scope='module')
def db():
  db = StudentDB()
  db.connect('data.json')
  yield db
  db.close()
  
def test_scott_data(db):
  scott_data = db.get_data('Scott')
  assert scott_data['id'] == 1
```
