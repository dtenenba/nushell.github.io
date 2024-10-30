---
title: polars str-join
categories: |
  dataframe
version: 0.99.0
dataframe: |
  Concatenates strings within a column or dataframes
usage: |
  Concatenates strings within a column or dataframes
---
<!-- This file is automatically generated. Please edit the command in https://github.com/nushell/nushell instead. -->

# `polars str-join` for [dataframe](/commands/categories/dataframe.md)

<div class='command-title'>Concatenates strings within a column or dataframes</div>

::: warning This command requires a plugin
The `polars str-join` command resides in the `polars` plugin.
To use this command, you must install and register `nu_plugin_polars`.
See the [Plugins](/book/plugins.html) chapter in the book for more information.
:::

## Signature

```> polars str-join {flags} (other)```

## Flags

 -  `--delimiter, -d {string}`: Delimiter to join strings within an expression. Other dataframe when used with a dataframe.
 -  `--ignore-nulls, -n`: Ignore null values. Only available when used as an expression.

## Parameters

 -  `other`: Other dataframe with a single series of strings to be concatenated. Required when used with a dataframe, ignored when used as an expression.


## Input/output types:

| input | output |
| ----- | ------ |
| any   | any    |

## Examples

Join strings in a column
```nu
> [[a]; [abc] [abc] [abc]] | polars into-df | polars select (polars col a | polars str-join -d ',') | polars collect
╭───┬─────────────╮
│ # │      a      │
├───┼─────────────┤
│ 0 │ abc,abc,abc │
╰───┴─────────────╯

```

StrJoin strings across two series
```nu
> let other = ([za xs cd] | polars into-df);
    [abc abc abc] | polars into-df | polars str-join $other
╭───┬───────╮
│ # │   0   │
├───┼───────┤
│ 0 │ abcza │
│ 1 │ abcxs │
│ 2 │ abccd │
╰───┴───────╯

```