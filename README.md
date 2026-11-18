# rift-conform

conform.nvim for rift: format files on save with external formatters.

After a save, the formatter runs on the file, only the lines it changed are
replaced in the buffer, and the buffer is saved again. rift can't pipe a
buffer into a process, so this formats the saved file. If you switch buffers
or type before it finishes, the result is dropped.

| Command | Effect |
|---|---|
| `:Format` | Format the current buffer now |
| `:ConformInfo` | Show the formatters, the executable found and the last error |

Out of the box it runs prettier on JavaScript, TypeScript and JSON.
Executables are looked up on `PATH` and in `~/.bun/bin` (`.exe`, `.cmd`,
`.bat` on Windows).

## Options

These go in `opts` in the riftpm spec (see Install):

```lua
{
  format_on_save = true,
  formatters_by_ft = {            -- filetype -> formatters, first found wins
    javascript = { "prettier" },
  },
  formatters = {
    prettier = { command = "prettier", args = { "$FILENAME" } },  -- prints to stdout
  },
  filetypes = { js = "javascript" },  -- file extension -> filetype
}
```

## Limitations

No LSP formatting fallback, and formatters that only read stdin aren't
supported yet.

## Install

rift-conform installs through riftpm. Install riftpm first from
[Monster0506/riftpm](https://github.com/Monster0506/riftpm) (see its README),
then add rift-conform to your `plugins.lua` spec:

```lua
{ "AndrewRoddy/rift-conform" },
```

With options:

```lua
{ "AndrewRoddy/rift-conform", opts = { format_on_save = true } },
```

Run `:PluginSync` to clone it.

Tested with rift 0.7.5.
