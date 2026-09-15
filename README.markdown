# sleuth.vim - fixed

## Fork behavior

This fork removes the heuristic scan's early exit after 32 qualifying
indentation increases. It examines the full bounded sample: up to 1,024
lines of the current file and up to 256 lines per neighboring file when
neighbor detection is needed. Declaration-heavy C++ prefixes can otherwise
make four-space continuation indentation outweigh two-space block indentation.
Modeline and EditorConfig precedence is unchanged.

Run the indentation regression checks with Neovim and Python 3 installed:

    python3 test/sleuth-indentation

## Overview

This plugin automatically adjusts `'shiftwidth'` and `'expandtab'`
heuristically based on the current file, or, in the case the current file is
new, blank, or otherwise insufficient, by looking at other files of the same
type in the current and parent directories.  Modelines and [EditorConfig][]
are also consulted, adding `'tabstop'`, `'textwidth'`, `'endofline'`,
`'fileformat'`, `'fileencoding'`, and `'bomb'` to the list of supported
options.
