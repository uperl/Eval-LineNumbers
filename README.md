# Eval::LineNumbers ![static](https://github.com/uperl/Eval-LineNumbers/workflows/static/badge.svg) ![linux](https://github.com/uperl/Eval-LineNumbers/workflows/linux/badge.svg)

Add line numbers to heredoc blocks that contain perl source code

# SYNOPSIS

```perl
use Eval::LineNumbers qw(eval_line_numbers);

eval eval_line_numbers(<<END_HEREIS);
  code
END_HEREIS

eval eval_line_numbers($caller_level, $code)
```

# DESCRIPTION

Add a `#line "this-file" 392` comment to heredoc/hereis text that is going
to be eval'ed so that error messages will point back to the right place.

Please note: when you embed `\n` in your code, it gets expanded in
double-quote hereis documents so it will mess up your line numbering.
Use `\\n` instead when you can.

## Caller Level Example

The second form of eval\_line\_numbers where a caller-level is provided
is for the situation where the code is generated in one place and 
eval'ed in another place.  The caller level should be the number of
stack levels between where the heredoc was created and where it is
eval'ed.

```perl
sub example {
  return <<END_HEREIS
    code
   END_HEREIS
}

eval eval_line_numbers(1, example())
```

# FUNCTIONS

All functions are exportable on request, but not by default.

## eval\_line\_numbers

```
eval eval_line_numbers($code);
eval eval_line_numbers($caller_level, $code);
```

## eval\_line\_numbers\_offset

```
eval_line_numbers_offset $offset;
```

Sets the offset, which is by default 1.  The offset is file scoped.  This
is useful if you want to pass a string without a heredoc.  For example:

```
eval_line_numbers_offset 0;
eval eval_line_numbers q{
  die "here";
};
```

# AUTHOR

Original author: David Muir Sharnoff

Current maintainer: Graham Ollis <plicease@cpan.org>

Contributors:

Olivier Mengué (DOLMEN)

David Steinbrunner (dsteinbrunner)

Alexey Ugnichev (thaewrapt)

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2009-2021 by David Muir Sharnoff.

This is free software, licensed under:

```
The GNU Lesser General Public License, Version 2.1, February 1999
```
