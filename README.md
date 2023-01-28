# 💡 Modicator.nvim

_Cursor line number mode indicator._

A small Neovim plugin that changes the foreground color of the `CursorLineNr` highlight based on the current Vim mode.

![modicator](https://user-images.githubusercontent.com/15816726/194103616-5fb6d1d3-5049-43cd-83da-20ed0c207d42.gif)

## Setup

```lua
require('modicator').setup()
```

Note that modicator requires you to have `termguicolors`, `cursorline`, `number` set. In Lua this is done by adding

```lua
vim.o.termguicolors = true
vim.o.cursorline = true
vim.o.number = true
```

somewhere in your Neovim configuration.

Modicator sets the Normal mode highlight foreground based on the default foreground color of `CursorLineNr` so if you're using a colorscheme make sure that it gets loaded before this plugin.

With [lazy.nvim](https://github.com/folke/lazy.nvim/):

```lua
return {
  'mawkler/modicator.nvim',
  dependencies = 'mawkler/onedark.nvim' -- Add your colorscheme plugin here,
  init = function()
    -- These are required for Modicator to work
    vim.o.cursorline = true
    vim.o.number = true
    vim.o.termguicolors = true
  end,
  config = function()
    require('modicator').setup({
      -- ...
    })
  end,
}
```

Or with [packer.nvim](https://github.com/wbthomason/packer.nvim/):

```lua
use {
  'mawkler/modicator.nvim',
  after = 'onedark.nvim', -- Add your colorscheme plugin here
  setup = function()
    -- These are required for Modicator to work
    vim.o.cursorline = true
    vim.o.number = true
    vim.o.termguicolors = true
  end,
  config = function()
    require('modicator').setup({
      -- ...
    })
  end
}
```

## Configuration

Use `highlights.modes[<mode>].color` to set the color for each mode, and pass it to `require('modicator').setup()`, as seen below. The key for each mode is the output `mode()` for that mode. Check out `:help mode()` for more information.

For normal mode, Modicator uses the `CursorLineNr`'s `fg` highlight.

**Default configuration:**

```lua
local modicator = require('modicator')

-- NOTE: Modicator requires line_numbers and cursorline to be enabled
modicator.setup({
  -- Show warning if any required option is missing
  show_warnings = true,
  highlights = {
    -- Default options for bold/italic. You can override these individually
    -- for each mode if you'd like as seen below.
    defaults = {
      bold = false,
      italic = false
    },
    -- Color and bold/italic options for each mode
    modes = {
      ['n'] = {
        color = M.get_highlight_fg('CursorLineNr'),
        bold = false,
        italic = false,
      },
      ['i']  = {
        color = M.get_highlight_fg('Question'),
        bold = false,
        italic = false,
      },
      ['v']  = {
        color = M.get_highlight_fg('Type'),
        bold = false,
        italic = false,
      },
      ['V']  = {
        color = M.get_highlight_fg('Type'),
        bold = false,
        italic = false,
      },
      ['�'] = {
        color = M.get_highlight_fg('Type'),
        bold = false,
        italic = false,
      },
      ['s']  = {
        color = M.get_highlight_fg('Keyword'),
        bold = false,
        italic = false,
      },
      ['S']  = {
        color = M.get_highlight_fg('Keyword'),
        bold = false,
        italic = false,
      },
      ['R']  = {
        color = M.get_highlight_fg('Title'),
        bold = false,
        italic = false,
      },
      ['c']  = {
        color = M.get_highlight_fg('Constant'),
        bold = false,
        italic = false,
      },
    },
  },
})
```
