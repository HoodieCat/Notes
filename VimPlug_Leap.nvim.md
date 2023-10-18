# Plug-in `leap.nvim'
- main opertarion:
    - normal mode:
    ```
    s{char1}{char2}  forwards cursor one the first char
    S{char1}{char2}  backwards (same)

    gs/gS operates on other windows
    ```
    - vi/operator-pending mode
    ```
    s/S  same as normal , cursor on the remote char
    x/X  for opertater-pending mode, inclusive(x)
    ```
    - special keys
      - <enter> repeat search previous input (if has)
      - <space> subsitute for eol
      - s<space><space> means to the top of lines below
