Read memory [](file:///Users/ddavisloc/Library/Application%20Support/Code/User/workspaceStorage/a1f0636569b276bd588487e1bf82acab/GitHub.copilot-chat/memory-tool/memories/MzdiNTNmNzUtZDZjNy00MGE5LTgzZjEtYzE3YTY5OWIyOThl/plan.md)

Since I don't currently have direct file editing tools enabled, I have provided the exact, full contents of the modernization plan in the code block below. You can easily copy and paste it or use the apply button to create the `MODERNIZATION_PLAN.md` file in the root of your workspace.

```markdown:MODERNIZATION_PLAN.md
## Plan: SoundScrape Python 3.12 Modernization & Preservation

Modernize the `SoundScrape` project to use Python 3.12 standards, replace abandoned dependencies (`nose`, `clint`, `demjson`), and migrate the legacy build system to a modern `pyproject.toml` managed by `uv`. **Crucially, all core scraping capabilities for SoundCloud, Bandcamp, Mixcloud, Audiomack, Hive, and MusicBed must be preserved exactly as described in the README.**

**Steps**

**Phase 1: Build System & Dependency Migration**
1. Initialize the `uv` environment and create a modern `pyproject.toml` file.
2. Define the project metadata (entry points, description, etc.) and set the build backend (e.g., `hatchling` or `setuptools`).
3. Add modern dependencies via `uv add`:
   - Core: `requests`, `mutagen`, `soundcloud-v2` (or keep `soundcloud` if it still works), `rich`, `demjson3`.
   - Dev: `pytest`.
4. Remove legacy build/config files (`setup.py`, `requirements.txt`, `MANIFEST.in`).

**Phase 2: Codebase Refactoring (Python 3.12)**
1. Remove all Python 2/3 compatibility blocks in `soundscrape/soundscrape.py` (e.g., `sys.version_info < (3,0,0)`, conditional `urllib` imports, `html.parser` vs `html.unescape` shims).
2. Refactor CLI UI: Replace `clint.textui` methods (colors, `puts`, `progress`) with `rich.console.Console` and `rich.progress`.
3. Swap `demjson` to `demjson3` (or stdlib `json`) and remove `simplejson`.
4. Modernize syntax: Introduce f-strings, switch `os` pathing to `pathlib.Path`, and add basic type hinting.
5. Replace `fudge` with `unittest.mock` for any testing mock behavior.

**Phase 3: Core Business Logic Preservation**
1. *Scraping Logic:* Ensure the routing logic for `process_soundcloud`, `process_bandcamp`, `process_mixcloud`, `process_audiomack`, `process_hive`, and `process_musicbed` remains intact.
2. *CLI Arguments:* Retain all exact arguments (`-n`, `-g`, `-b`, `-m`, `-a`, `-c`, `-l`, `-L`, `-d`, `-t`, `-f`, `-p`, `-P`, `-o`, `-k`, `-v`) to avoid breaking existing users' scripts.
3. *ID3 Tagging:* Ensure the `mutagen` code that applies ID3 tags and album art is preserved during the modernization.

**Phase 4: Testing Framework Migration**
1. Modify `tests/test.py` to support `pytest`. Existing `unittest.TestCase` can remain, but test execution will be managed by `pytest`.
2. Update `test.sh` to run `pytest` instead of `nosetests`.

**Relevant files**
- `pyproject.toml` — New source of truth for build configuration and dependencies.
- `setup.py`, `requirements.txt`, `MANIFEST.in` — To be deleted.
- `soundscrape/soundscrape.py` — Implement Python 3.12 features, `rich` CLI replacement, and strip out Py2 compatability. Preserve business logic.
- `tests/test.py` — Migrate to `pytest` execution and `unittest.mock`.
- `test.sh` — Update from `nosetests` to `pytest`.

**Verification**
1. Run `uv lock` and `uv sync` to ensure dependencies resolve and install correctly.
2. Run `uv run pytest tests/test.py` to ensure the test suite passes on the modern framework.
3. Run `uv run soundscrape -v` to test the CLI entrypoint registration.
4. Manually test downloading a track using the features from the README (e.g., Bandcamp flag `-b`, high-quality `-d`, folders `-f`) to verify the exact behavior is preserved.

**Decisions**
- **CLI Modernization**: Replaced unmaintained `clint` library with `rich` for modern terminal output, but retaining all original argparse arguments.
- **Business Logic**: No changes to the actual scraping URL resolution, downloading mechanisms, or mutagen ID3 tagging logic.
- **Test Framework**: Replaced deprecated `nose` and `fudge` with standard `pytest` and `unittest.mock`.
- **JSON Parsing**: Migrating from `demjson` to `demjson3` or standard library `json`.
- **Build System**: Exclusive use of `uv` to manage environment, dependencies, and `pyproject.toml`.
```