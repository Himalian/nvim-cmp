# Repository Guidelines

## Project Structure & Modules
- `lua/`: Core plugin source (`cmp/*` modules). Tests live alongside as `*_spec.lua`.
- `plugin/`: Neovim entrypoint that loads the plugin (`cmp.lua`).
- `autoload/`: Vimscript glue for bootstrapping.
- `doc/`: Help docs (`cmp.txt`) for `:h cmp`.
- `utils/`: Developer helpers (e.g., `utils/vimrc.vim`).
- Root files: `Makefile`, `.luacheckrc`, `stylua.toml`, `nvim-cmp-*.rockspec`.

## Build, Test, and Development
- `make lint`: Run `luacheck` on `lua/`.
- `make test`: Run unit tests via `vusted --output=gtest ./lua`.
- `make pre-commit`: Lint + test; mirrors CI expectations.
- Git hooks: run `./init.sh` once to install pre-commit hook from `.githooks/`.
- Optional: `make integration` (same checks; used by CI/integration scripts).

## Coding Style & Naming
- Indentation: 2 spaces; spaces over tabs.
- Quotes: Prefer single quotes (see `stylua.toml`).
- Line width: No strict limit (configured wide to avoid hard-wraps).
- Formatting: Use `stylua` locally, e.g. `stylua lua plugin`.
- Linting: `luacheck` with `.luacheckrc` (globals like `vim`, `describe`, `it` already whitelisted).
- Modules: Namespaced under `cmp.*`; filenames use `snake_case.lua`.

## Testing Guidelines
- Framework: `vusted` (Busted for Neovim). Write `*_spec.lua` next to the code under test.
- Run all: `make test` or `vusted lua`.
- Run a file: `vusted lua/cmp/core_spec.lua`.
- Add tests for new behavior and bug fixes; keep specs deterministic (no timing-dependent asserts).

## Commit & Pull Request Guidelines
- Commits: Imperative, concise; optional scope. Examples:
  - `fix: handle winborder in neovim-0.11`
  - `fix(utils): Only call callback if function`
- PRs: Provide a clear description, minimal Neovim config to reproduce (if a bug), before/after behavior, and linked issues (`#123`). Include environment details (Neovim version, OS).

## Notes & Tips
- Prefer current Neovim APIs; avoid deprecated calls when touching code.
- Changes to user-visible behavior should update `doc/cmp.txt` as needed.
