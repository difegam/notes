# Python String

## Raw Strings
Raw strings are string literals prefixed with an `⁠r`, where the backslash (\) is always treated as a literal character. Always use raw strings for regular expression patterns.

```python
import re
pattern = re.compile(r"\d{3}-\d{3}-\d{4}")
```
```python
print(r"Hello\tWorld")
# Hello\tWorld

print("Hello\tWorld") # \t is treated as a tab
# Hello   World
```

## Formatted Strings (f-strings)

Formatted strings are string literals prefixed with an `⁠f`, where expressions inside curly braces are evaluated at runtime.

```python
name = "Diego"
print(f"Hi, {name}", this is a formatted string)
# Hello, Diego
```

In Python 3.8 and later, you can show both an expression and its result by adding an equal sign (⁠=) at the end, like this:

```python
x = 31
print(f"{x=}")
# x=31
print(f"{x+2=}")
# x+2=33
print(f"{x + 2 = }") # Spaces are allowed before and after the equal sign
# x + 2 = 33
```


## Format Specifications
You can also specify the format of the expression inside the curly braces.

| Format | Description | Example | Result |
| --- | --- | --- | --- |
| `!r` | Calls `repr()` on the expression | `f"{x!r}"` | `'31'` |
| `!a` | Calls `ascii()` on the expression | `f"{x!a}"` | `'31'` |
| `!s` | Calls `str()` that is the default | `f"{x!s}"` | `'31'` |
| `:=+` | Includes the sign of the number | `f"{-31:=+}"` | `'-31'` |
| `:<6` | Left aligns the value in a field of width 6 | `f"{x:<6}"` | `'31    '` |
| `:>6` | Right aligns the value in a field of width 6 | `f"{x:>6}"` | `'    31'` |
| `:^6` | Center aligns the value in a field of width 6 | `f"{x:^6}"` | `'  31  '` |
| `:*^6` | Center aligns the value in a field of width 6 and pads with asterisks | `f"{x:*^6}"` | `'*31**'` |
| `:06` | Pads the number with zeros | `f"{x:06}"` | `'000031'` |
| `:.3f` | Formats the number as a float with 3 decimal places | `f"{x:.3f}"` | `'31.000'` |
| `:06.4f` | Formats the number as a float with 4 decimal places and pads with zeros | `f"{3.14159:06.4f}"` | `'003.1416'` |
| `:06.4e` | Formats the number in scientific notation with 4 decimal places and pads with zeros | `f"{3.14159:06.4e}"` | `'3.1416e+00'` |
| `:%` | Formats the number as a percentage | `f"{0.50:%}"`| `50.000000%` |
| `.2%` | Formats the number as a percentage with 2 decimal places | `f"{0.50:.2%}"` | `50.00%` |
| `:_` | Adds an underscore as a thousands separator | `f"{1000000:_}"` | `1_000_000` |
| `:,` | Adds a comma as a thousands separator | `f"{1000000:,}"` | `1,000,000` |
| `:,.2f` | Adds a comma as a thousands separator and formats the number as a float with 2 decimal places | `f"{1000000:,.2f}"` | `1,000,000.00` |
| `:#x` | Formats the number in hexadecimal with a leading `0x` | `f"{255:#x}"` | `0xff` |
| `:#X` | Formats the number in hexadecimal with a leading `0x` | `f"{255:#X}"` | `0xFF` |
| `:#o` | Formats the number in octal with a leading `0o` | `f"{255:#o}"` | `0o377` |
| `:#b` | Formats the number in binary with a leading `0b` | `f"{255:#b}"` | `0b11111111` |

```python
text = "text"
print(f"{text:*^10}")
# ***text***

n = 20
print(f"{text:*^{n}}")
# ********text********

n=50
print(f"{text:*>{n}}")
# **********************************************text
```

## f-strings for datetime formatting
f-strings can also be used to format dates and times.

```python
from datetime import datetime
now = datetime.now()
print(f"{now:%Y-%m-%d %H:%M:%S}")
# 2024-12-01 14:41:58
```

| Format | Description | Example | Result |
| --- | --- | --- | --- |
| `:%x` | Locale's appropriate date representation | `{now:%x}` | `12/01/24` |
| `:%X` | Locale's appropriate time representation | `{now:%X}` | `14:41:58` |
| `:%c` | Locale's appropriate date and time representation | `{now:%c}` | `Sun Dec  1 14:41:58 2024` |
| `:%H:%M:%S` | Hour, minute, and second | `{now:%H:%M:%S}` | `14:41:58` |
| `:%Y` | Year with century as a decimal number | `{now:%Y}` | `2024` |
| `:%y` | Year without century as a zero-padded decimal number | `{now:%y}` | `24` |
| `:%m` | Month as a zero-padded decimal number | `{now:%m}` | `12` |
| `:%B` | Full month name | `{now:%B}` | `December` |

# References
- [Dead Simple Python: Idiomatic Python for the Impatient Programmer](https://www.amazon.com/Dead-Simple-Python-Idiomatic-Programmers/dp/1718500920)
- [Fluent Python: Clear, Concise, and Effective Programming](https://www.amazon.nl/-/en/Luciano-Ramalho/dp/1491946008)
- [Every F-String Trick In Python Explained](https://www.youtube.com/watch?v=9saytqA0J9A)