---
title: 'Laravel: Print Big Number in `maatwebsite/laravel-excel`'
date: 2024-11-18 16:49:16
tags:
- Laravel
- Laravel Excel
- maatwebsite/laravel-excel
category:
- Laravel
---

When exporting data in Laravel using the `maatwebsite/excel` package, it’s common to encounter issues with large numbers being incorrectly formatted. One such case involves account numbers, which are often stored as long integers, such as `1001009280102889`. However, when exporting them, the numbers may be displayed in scientific notation (e.g., `1.00101E+15`) or rounded incorrectly (e.g., `1001009280102880` instead of `1001009280102889`). These discrepancies can lead to critical errors in financial applications.

## The Problem

By default, when exporting data with Laravel Excel, numbers like account numbers might be treated as floats, which leads to inaccurate representations. Specifically, using the following configuration:

```php
NumberFormat::FORMAT_TEXT,
```

would result in the account number `1001009280102889` being displayed as `1.00101E+15`. On the other hand, using:

```php
NumberFormat::FORMAT_NUMBER,
```

would show `1001009280102880`, which is almost correct but with the last digit changed — an unacceptable error in many cases.

## The Why

This issue is rooted in how Excel handles numbers internally and its limited precision for large integers. Here's a more detailed breakdown:

1. Excel’s Floating-Point Precision

Excel, like many other software applications, uses the **IEEE 754 standard** for representing floating-point numbers. This standard stores numbers as approximations within a limited range of precision. Specifically, Excel uses **64-bit floating-point numbers** for numeric data, which can represent numbers up to approximately **15 significant digits**.

When you try to export a number like `1001009280102889`, which has 16 digits, Excel starts to lose precision beyond the 15th digit. As a result, Excel rounds it to the nearest value it can represent within the 15-digit limit. This leads to the value `1001009280102889` being converted to `1001009280102880`, which is the closest 15-digit number Excel can store.

This rounding behavior is why **large numbers with more than 15 digits** can appear incorrect when treated as numbers in Excel.

2. Number Format (`FORMAT_NUMBER`)

When you set the number format to `FORMAT_NUMBER` in `maatwebsite/excel`, you're telling Excel to treat the value as a standard numeric value. Excel will then attempt to display it in the most fitting numeric format, but it is still constrained by its floating-point precision.

For example:

- `1001009280102889` is stored and displayed as `1001009280102880` because Excel rounds the last digit to fit its internal format.
- This happens because Excel doesn't recognize that the last digits are critical in certain financial or scientific contexts.

This rounding effect can be particularly problematic when dealing with sensitive data like **account numbers**, where the exact value is crucial.

3. Text Format (`FORMAT_TEXT`) and Scientific Notation (`E+{number}`)

Now, when you use `FORMAT_TEXT` or force Excel to treat the value as a string, Excel will **no longer try to interpret the value as a number**. This prevents it from applying rounding or floating-point precision limitations.

However, Excel can still use **scientific notation** to represent very large numbers when they are stored as text. In the case of `1001009280102889`, Excel may display it as `1.001009280102889E+15` — this is just scientific notation, which is a shorthand for large numbers. 

Here:

- The `E+15` indicates that the decimal point should be shifted 15 places to the right, essentially returning to the original value of `1001009280102889`.

While scientific notation doesn't modify the actual value, it **can make it less readable**. This is why it's often better to store large numbers like account numbers as strings to prevent Excel from applying scientific notation, allowing the number to be displayed exactly as entered.

## The Solution

After some research, I came across a helpful comment by **Bhargav Rangani** on [this StackOverflow post](https://stackoverflow.com/questions/72430680/laravel-excel-number-value-auto-change). **Bhargav pointed** out that the solution to this problem lies in explicitly treating the account number as a string during export. This prevents Excel from applying unwanted formatting to the number and ensures it is displayed exactly as intended.

Here's how to apply the fix:

1. **Update the `value_binder`** in `config/excel.php`: Change the **value_binder** configuration from the default:

```php
'value_binder' => [
    /*
    |--------------------------------------------------------------------------
    | Default Value Binder
    |--------------------------------------------------------------------------
    |
    | PhpSpreadsheet offers a way to hook into the process of a value being
    | written to a cell. In there some assumptions are made on how the
    | value should be formatted. If you want to change those defaults,
    | you can implement your own default value binder.
    |
    */
    'default' => Maatwebsite\Excel\DefaultValueBinder::class,
],
```

to:

```php
'value_binder' => [
    /*
    |--------------------------------------------------------------------------
    | Default Value Binder
    |--------------------------------------------------------------------------
    |
    | PhpSpreadsheet offers a way to hook into the process of a value being
    | written to a cell. In there some assumptions are made on how the
    | value should be formatted. If you want to change those defaults,
    | you can implement your own default value binder.
    |
    */
    'default' => PhpOffice\PhpSpreadsheet\Cell\StringValueBinder::class
],
```

This tells `PhpSpreadsheet`, the underlying library used by `maatwebsite/excel`, to treat values as strings, preventing Excel from applying unwanted formatting or rounding to large numbers like account numbers.

## Conclusion

By updating the `value_binder` configuration, you can ensure that large numbers such as account numbers are exported as plain text, avoiding the issues of scientific notation or rounding errors. This simple change guarantees that your financial data remains accurate, which is crucial for any application that handles sensitive information like account numbers.

If you’re working with large numbers or account numbers in Laravel and using `maatwebsite/excel`, try to implement this fix to avoid export issues and maintain data integrity.