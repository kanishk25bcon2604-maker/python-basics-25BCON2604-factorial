# README Audit: `factorial.py`

This audit checks each claim in the README against the actual code in `factorial.py`. Claims were verified by reading the code and by running it (Python 3.12.3) with edge-case tests.

## Summary

- **Claims checked:** 17
- **Supported:** 16 (one with a caveat)
- **Not Supported:** 1 (the clone URL, which is a placeholder the code cannot confirm)

## Source Code Audited

```python
def factorial(n):
    if n < 0:
        raise ValueError("Factorial is not defined for negative numbers.")

    result = 1
    for value in range(2, n + 1):
        result = result * value
    return result

number = 5
print(f"Factorial of {number} is {factorial(number)}")
```

## Claim-by-Claim Results

| # | Claim in README | Verdict | Evidence from the code |
|---|---|---|---|
| 1 | Calculates the factorial of a non-negative integer | Supported | The loop computes the product of 2 to `n`. Output matched `math.factorial` for every value from 0 to 500. |
| 2 | `5! = 120` and `0! = 1` | Supported | `factorial(5)` returns 120. For `n = 0`, `range(2, 1)` is empty, so `result` stays 1. |
| 3 | Implemented in a single file, `factorial.py` | Supported | All logic is in one file. |
| 4 | Iterative implementation | Supported | It uses `for value in range(2, n + 1)` and the function never calls itself. |
| 5 | No recursion-depth limit | Supported | There is no recursion, so Python's recursion limit does not apply. |
| 6 | Raises a clear `ValueError` for negative numbers | Supported | `if n < 0: raise ValueError(...)`. `factorial(-3)` raised exactly that error. |
| 7 | Returns `1` for both `0` and `1` | Supported | Both `range(2, 1)` and `range(2, 2)` are empty. Tested: `0!` and `1!` both gave 1. |
| 8 | Handles very large results using Python's big integers | Supported, with a caveat | The code uses plain `int` multiplication with no fixed-width types, and `factorial(1500)` computed correctly. However, the script's own `print(f"...")` fails on Python 3.11+ once the result exceeds 4,300 digits. `factorial(1600)` raised `ValueError: Exceeds the limit (4300 digits) for integer string conversion`. |
| 9 | No external dependencies | Supported | The file has no `import` statements. |
| 10 | Requires Python 3.6 or higher | Supported | The file uses an f-string, which was introduced in 3.6. Only 3.12 was run, so the lower bound comes from the syntax rule, not a test. |
| 11 | No third-party packages needed | Supported | Same evidence as #9. |
| 12 | `git clone https://github.com/<your-username>/<your-repository>.git` | Not Supported | The code cannot confirm any repository, URL, or folder name, and the URL is a placeholder. |
| 13 | `python factorial.py` runs the script | Supported | It ran successfully and printed `Factorial of 5 is 120`. On some systems the command is `python3`. |
| 14 | It calculates the factorial of the `number` variable at the bottom of the file | Supported | `number = 5` is followed by `print(f"... {factorial(number)}")`. |
| 15 | Changing it to `number = 10` works | Supported | `factorial(10)` returned 3628800. |
| 16 | Output is `Factorial of 5 is 120` | Supported | This is the exact output of the script. |
| 17 | A negative number gives `ValueError: Factorial is not defined for negative numbers.` | Supported | The message is word for word the same as in the code. |

## Behaviors the README Does Not Mention

### Non-integer input

A float or a string is not rejected with a clear message:

| Input | Result |
|---|---|
| `factorial(3.5)` | `TypeError: 'float' object cannot be interpreted as an integer` |
| `factorial(5.0)` | `TypeError: 'float' object cannot be interpreted as an integer` |
| `factorial("a")` | `TypeError: '<' not supported between instances of 'str' and 'int'` |

The README says "non-negative integer", which is accurate, but it never says what happens with other types.

### Import side effect

Importing the file also runs the example, because the `number = 5` and `print(...)` lines sit at module level without an `if __name__ == "__main__":` guard. In testing, the example output printed twice: once from running the file directly and once from importing it. The earlier full README mentioned this, but the clean version dropped that note.

## Test Environment

- Python 3.12.3
- Checks run: direct execution, `0!`, `1!`, `10!`, negative input, float input, string input, comparison against `math.factorial` for 0 to 500, and large-value formatting at n = 1000, 1500, 1600, and 2000.
