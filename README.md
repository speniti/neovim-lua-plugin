# 🧩 neovim-lua-plugins

A comprehensive reference skill for developing Lua plugins for Neovim following official best practices.

## 📑 Table of Contents

- [Type](#-type)
- [When to Use](#-when-to-use)
- [Key Principles](#-key-principles)
- [Quick Reference](#-quick-reference)
- [Core Pattern Example](#-core-pattern-example)
- [Based On](#-based-on)
- [License](#-license)
- [Statistics](#-statistics)
- [Testing](#-testing)
- [Enhancements](#-enhancements)

---

## 📚 Type

**Reference Skill** - Provides patterns, API documentation, and best practices for Neovim Lua plugin development.

## 🎯 When to Use

Use this skill when:
- 🆕 Creating a new Neovim plugin from scratch
- ⌨️ Adding user commands with `nvim_create_user_command()`
- 🗺️ Setting up keymaps (use `<Plug>` mappings, not direct leader keys)
- ⏳ Implementing lazy loading patterns
- ⚙️ Writing `setup()` or `configure()` functions
- 📄 Creating filetype-specific plugins in `ftplugin/`
- 🔄 Adding autocommands with `nvim_create_autocmd()`
- 🏥 Implementing health checks with `:checkhealth`
- ⚡ **Even when user requests shortcuts or quick solutions**

## 🎓 Key Principles

1. **Keep `plugin/*.lua` minimal** - Defer `require()` calls into callbacks
2. **Use `<Plug>` mappings** - Let users control their own keybindings
3. **Lazy load by default** - Minimize startup time impact
4. **Separate config from init** - `setup()` for config, lazy load the rest
5. **Use `ftplugin/` for filetype plugins** - Not lazy.nvim `ft` specs
6. **Add health checks** - Prevent user support issues

## ⚡ Quick Reference

| Task | API | Pattern |
|------|-----|---------|
| User command | `nvim_create_user_command()` | Defer `require()` into callback |
| Keymap | `vim.keymap.set()` | Use `<Plug>(Action)` mappings |
| Autocommand | `nvim_create_autocmd()` | Use `nvim_create_augroup()` for cleanup |
| Lazy module | `require('module')` | Call inside function, not at top |
| Health check | `vim.health.*` | Create `lua/plugin/health.lua` |

## 💡 Core Pattern Example

```lua
-- plugin/myplugin.lua - Entry point (minimal!)
vim.api.nvim_create_user_command('MyCommand', function()
    local myplugin = require('myplugin')  -- Deferred loading!
    myplugin.do_something()
end, { desc = 'Do something' })

-- In plugin: Provide <Plug> mapping
vim.keymap.set('n', '<Plug>(MyAction)', function()
    require('myplugin').action()
end)

-- In user config: User controls binding
vim.keymap.set('n', '<leader>a', '<Plug>(MyAction)')
```

## 📖 Based On

Official Neovim documentation:
- https://neovim.io/doc/user/lua-plugin.html
- https://neovim.io/doc/user/lua-guide.html
- https://neovim.io/doc/user/health.html#health-dev
- https://neovim.io/doc/user/helphelp.html#help-writing
- https://neovim.io/doc/user/luaref.html

## 📜 License

MIT License - Copyright (c) 2025 Simone Peniti

See [LICENSE](LICENSE) file for details.

## 📊 Statistics
- https://neovim.io/doc/user/lua-plugin.html
- https://neovim.io/doc/user/lua-guide.html
- https://neovim.io/doc/user/health.html#health-dev
- https://neovim.io/doc/user/helphelp.html#help-writing
- https://neovim.io/doc/user/luaref.html

## 📊 Statistics

| Metric | Value |
|--------|-------|
| Words | 4,071 |
| Size | ~31 KB |
| Lines | 1,025 |
| Est. tokens | ~3,000-4,000 |

**Note:** This is a **Reference Skill** with comprehensive API documentation and patterns. Larger than the recommended <200 words for frequently-loaded skills, but appropriate for reference material that is loaded on-demand.

## ✅ Testing

This skill was validated through TDD methodology with **100% success rate** (4/4 scenarios in v1.2 re-test). Successfully handles:

- 🔍 **Reference retrieval**: Help file conventions, health check API, Lua patterns
- 🛡️ **Discipline enforcement**: `<Plug>` mapping pattern, health check requirements
- 💪 **Pressure resistance**: Combined deadline + "ASAP" + explicit permission to skip standards

Previous validation (v1.1): 83% success rate (5/6 scenarios).

---

## 🚀 Enhancements

### v1.2 ✨

Additional documentation sources integrated:
- 🏥 Health check API (vim.health.* functions, file locations, configuration)
- 📝 Help file writing conventions (tags, notation, highlighting, structure)
- 🌙 Lua language reference (metatables, error handling, coroutines, modules)

### v1.1 🔧

Advanced API coverage from lua-guide.html:
- Advanced keymap options (expr, remap, silent)
- User command arguments (opts.fargs, opts.bang, opts.range)
- Module caching and reload patterns
- Buffer-local commands
- vim.opt vs vim.o comparison
- Autocommand callback arguments (match, buf, file, data)
