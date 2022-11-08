# Lua API

You can also manually bind new items after you've already called `require('legendary').setup()`.
This can be useful for things like binding language-specific keyaps in the LSP `on_attach` function.

The main API functions are described below. To see full API documentation, run `:LegendaryApi`.

```lua
-- bind a single keymap
require('legendary').bind_keymap(keymap)
-- bind a list of keymaps
require('legendary').bind_keymaps({
  -- your keymaps here
})

-- bind a single command
require('legendary').bind_command(command)
-- bind a list of commands
require('legendary').bind_commands({
  -- your commands here
})

-- bind a single function
require('legendary').bind_function(fn_tbl)
-- bind a list of functions
require('legendary').bind_functions({
  -- your function tables here
})

-- bind single or multiple augroups and/or autocmds
-- these all use the same function
require('legendary').bind_autocmds(augroup)
require('legendary').bind_autocmds(autocmd)
require('legendary').bind_autocmds({
  -- your augroups and autocmds here
})

-- search keymaps, commands, functions, and autocmds
require('legendary').find()
-- search keymaps
require('legendary').find({ kind = 'keymaps' })
-- search commands
require('legendary').find({ kind = 'commands' })
-- search functions
require('legendary').find({ kind = 'functions' })
-- search autocmds
require('legendary').find({ kind = 'autocmds' })

-- filter keymaps by current mode
require('legendary').find({
  filters = { require('legendary.filters').current_mode() },
})

-- find only keymaps, and filter by current mode
require('legendary').find({
  kind = 'keymaps',
  filters = { require('legendary.filters').current_mode() }
)
-- filter keymaps by normal mode
require('legendary').find({
  filters = require('legendary.filters').mode('n')
})
-- filter keymaps by normal mode and that start with <leader>
require('legendary').find({
  filters = {
    require('legendary.filters').mode('n'),
    function(item)
      if not string.find(item.kind, 'keymap') then
        return false
      end

      return vim.startswith(item[1], '<leader>')
    end
  }
})
```