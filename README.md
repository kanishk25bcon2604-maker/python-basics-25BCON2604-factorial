# Factorial Calculator

A simple Python program that calculates the factorial of a non-negative integer.

## Description

The factorial of a non-negative integer `n`, written `n!`, is the product of all positive integers from 1 to `n`. For example, `5! = 5 × 4 × 3 × 2 × 1 = 120`, and by definition `0! = 1`.

This project implements that calculation in a single, easy-to-read Python file, `factorial.py`.

## Features

- Iterative implementation (no recursion-depth limit)
- Raises a clear `ValueError` for negative numbers
- Correctly returns `1` for both `0` and `1`
- Handles very large results using Python's built-in big integers
- No external dependencies

## Requirements

- Python 3.6 or higher
- No third-party packages

## Installation

Clone the repository and move into the project folder:

```bash
git clone https://github.com/kanishk25bcon2604-maker/python-basics-25BCON2604-factorial.git
cd <your-repository>
```

## Usage

Run the script from the command line:

```bash
python factorial.py
```

The script calculates the factorial of the value assigned to the `number` variable at the bottom of `factorial.py`. To calculate a different factorial, change
