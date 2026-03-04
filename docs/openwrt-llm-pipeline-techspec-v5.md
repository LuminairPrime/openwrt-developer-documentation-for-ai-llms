# OpenWrt LLM Documentation Pipeline
# Technical Design Document — v5
# Status: Approved for Implementation
# Supersedes: v4 (incorporates all corrections from workflow-fixes.diff)

---

## 1. Purpose and Scope

This document defines the complete design for an automated GitHub Actions
pipeline that collects, processes, and publishes OpenWrt developer documentation
in formats optimized for LLM consumption (large language models).

The pipeline runs monthly at no cost (GitHub Actions free tier + GitHub Models
free tier), publishes results to a GitHub Pages URL, and produces a file layout
designed for both RAG (retrieval-augmented generation) use cases and direct
context-window injection.

A separate, manually-maintained set of static "rulebook" files is maintained
locally by the user and uploaded to the `static-docs/` folder in the repository.
The pipeline promotes these files to the GitHub Pages root on each run.

---

## 2. High-Level Architecture

### 2.1 Two-Tier Split

**Tier 1 — Automated (GitHub Actions, monthly, $0)**

Handles everything that can be done mechanically and repeatably:
- Cloning upstream source repositories
- Generating API documentation from annotated source code (jsdoc-to-markdown)
- Scraping the OpenWrt wiki using the DokuWiki raw export endpoint
- Extracting curated LuCI application examples (raw, unmodified source files)
- Extracting package metadata from the OpenWrt buildroot source
- Injecting cross-references between all generated files (root-relative links)
- Detecting deprecated symbols and injecting warnings into wiki docs
- Running lightweight AI post-processing via GitHub Models (free tier)
- Assembling single-file merged references for each documentation set
- Publishing everything to GitHub Pages
- Committing generated files back to the repository for version-controlled access

**Tier 2 — Static / manual (local machine, updated rarely)**

Handles content that requires deep judgment and significant AI processing.
Generated locally with a capable model, reviewed manually, and uploaded when
substantially stale:
- `SYSTEM-PROMPT.md` — platform "rules" for injecting into LLM custom instructions
- `concepts-glossary.md` — plain-English definitions of all major OpenWrt concepts
- `openwrt-recipes.md` — curated "how to do X" code patterns with working examples

These files live in `static-docs/` in the repo root. The pipeline copies them
to the GitHub Pages root unchanged on each run. They are not regenerated.

### 2.2 Data Flow

```
upstream repos (GitHub)          openwrt.org wiki         static-docs/ (manual)
        |                               |                          |
        v                               v                          |
  [clone / sparse-checkout]    [sitemap → age filter]              |
        |                               |                          |
        v                               v                          |
  [jsdoc2md per file]          [?do=export_raw + pandoc]           |
        |                               |                          |
        v                               v                          |
  [per-file .md output]        [per-file .md output]               |
        |                               |                          |
        +-------------------+-----------+                          |
                            |                                      |
                            v                                      |
              [Step 8: cross-reference injection]                  |
                            |                                      |
                            v                                      |
              [Step 9: deprecation checker]                        |
                            |                                      |
                            v                                      |
              [Step 10: AI module summaries]                       |
                            |                                      |
                            v                                      |
              [Step 11: assemble single-file references]           |
                            |                                      |
                            v                                      |
              [Step 12: generate root llms.txt]                    |
                            |                                      |
                            +--------------------------------------+
                            |
                            v
              [Step 13: GitHub Pages publish]
              https://[user].github.io/[repo]/
              [Step 14: commit back to repo]
```

---

## 3. Repository Structure

### 3.1 Source layout (this repo, maintained by user)

```
.github/
  workflows/
    generate-llm-docs.yml        ← the main workflow (defined by this document)

static-docs/                     ← manually maintained, user-uploaded
  SYSTEM-PROMPT.md
  concepts-glossary.md
  openwrt-recipes.md

README.md                        ← describes the project and how to use the outputs
```

### 3.2 Generated output layout (committed to repo + published to Pages)

```
ucode-docs/
  llms.txt
  ucode-tutorial-usage.md
  ucode-tutorial-syntax.md
  ucode-tutorial-memory.md
  ucode-tutorial-arrays.md
  ucode-tutorial-dictionaries.md
  ucode-module-core.md
  ucode-module-debug.md
  ucode-module-digest.md
  ucode-module-fs.md
  ucode-module-io.md
  ucode-module-log.md
  ucode-module-math.md
  ucode-module-nl80211.md
  ucode-module-resolv.md
  ucode-module-rtnl.md
  ucode-module-socket.md
  ucode-module-struct.md
  ucode-module-uci.md
  ucode-module-uloop.md
  ucode-module-zlib.md

luci-docs/
  llms.txt
  luci-api-LuCI.md               ← top-level LuCI class
  luci-api-baseclass.md
  luci-api-dom.md
  luci-api-form.md
  luci-api-fs.md
  luci-api-headers.md
  luci-api-network.md
  luci-api-poll.md
  luci-api-request.md
  luci-api-response.md
  luci-api-rpc.md
  luci-api-session.md
  luci-api-uci.md
  luci-api-ui.md
  luci-api-validation.md
  luci-api-view.md
  luci-api-xhr.md
  ... (additional files for nested classes)

openwrt-wiki-docs/
  llms.txt
  openwrt-techref-ubus.md
  openwrt-techref-uci.md
  openwrt-techref-procd.md
  openwrt-techref-netifd.md
  openwrt-techref-nftables.md
  openwrt-techref-sysupgrade.md
  openwrt-techref-filesystems.md
  openwrt-guide-developer-packages.md
  openwrt-guide-developer-feeds.md
  openwrt-guide-developer-procd-init-scripts.md
  openwrt-guide-developer-luci-helloworld.md
  openwrt-guide-developer-luci-modules.md
  openwrt-guide-developer-debugging.md
  ... (all pages passing the 2-year age filter)

openwrt-buildroot-docs/
  llms.txt
  openwrt-buildroot-network.md
  openwrt-buildroot-kernel.md
  openwrt-buildroot-utils.md
  openwrt-buildroot-system.md
  openwrt-buildroot-libs.md
  openwrt-buildroot-include-mk.md

openwrt-examples/
  llms.txt
  luci-app-example/              ← hello world / bare minimum modern LuCI app
    ... (raw unmodified .uc and .js files)
  luci-app-commands/             ← HTTP API / controller pattern
    ... (raw unmodified .uc and .js files)
  luci-app-ddns/                 ← standard config app / rpcd integration
    ... (raw unmodified .uc and .js files)
  luci-app-dockerman/            ← advanced: UNIX sockets, streaming, multi-file
    ... (raw unmodified .uc and .js files)

SYSTEM-PROMPT.md                 ← promoted from static-docs/ to root
concepts-glossary.md             ← promoted from static-docs/ to root
openwrt-recipes.md               ← promoted from static-docs/ to root

ucode-complete-reference.md      ← all ucode content merged, TOC at top
luci-jsapi-complete-reference.md
openwrt-wiki-complete-reference.md
openwrt-buildroot-complete-reference.md
openwrt-examples-complete-reference.md

llms.txt                         ← root index following the llms.txt standard
```

### 3.3 Root llms.txt Format

The root `llms.txt` follows the official llms.txt standard (https://llmstxt.org):
an H1 title, a blockquote summary, and H2-sectioned bulleted markdown links in
the format `- [Name](url): Description`. It is generated dynamically from files
that actually exist in the output — not from a hardcoded template — so it
remains accurate when steps are skipped.

Example structure:

```markdown
# OpenWrt Developer Documentation for LLMs

> Automated documentation mirror optimized for AI context ingestion. Covers the
> ucode scripting language, LuCI client-side JS API, OpenWrt wiki developer
> guides, buildroot package metadata, and curated full-stack application examples.
> Updated monthly from upstream sources.

## Rulebooks and Guidelines

- [SYSTEM-PROMPT.md](/SYSTEM-PROMPT.md): Core OpenWrt platform rules for LLM custom instructions
- [concepts-glossary.md](/concepts-glossary.md): Plain-English definitions of all major OpenWrt concepts
- [openwrt-recipes.md](/openwrt-recipes.md): Curated "how to do X" code patterns with working examples

## Complete References (single-file, feed directly to context window)

- [ucode-complete-reference.md](/ucode-complete-reference.md): Complete ucode scripting language API
...

## Modular References (individual files for targeted RAG or selective loading)

- [ucode-docs/llms.txt](/ucode-docs/llms.txt): Index of all ucode module and tutorial files
...
```

---

## 4. Data Sources

### 4.1 ucode Scripting Language

| Property | Value |
|---|---|
| Source repository | https://github.com/jow-/ucode |
| Live documentation | https://ucode.mein.io/ |
| Config detection | Scrape live site HTML for embedded jsdoc config path before cloning; write to `$GITHUB_ENV` |
| Config fallback | `jsdoc/conf.json` |
| Tutorial source | `docs/tutorial-*.md` — already markdown, copy directly with metadata header prepended |
| Module source | `lib/*.js` and `lib/*.c` — JSDoc comment blocks in both JS stubs and C source |
| Processing tool | `jsdoc-to-markdown` per file, `--heading-depth 2 --global-index-format none` |
| Output prefix | `ucode-tutorial-` for tutorials, `ucode-module-` for modules |
| Minimum content threshold | Skip output with fewer than 15 words (no meaningful documentation found) |

### 4.2 LuCI Client-Side JS API

| Property | Value |
|---|---|
| Source repository | https://github.com/openwrt/luci |
| Live documentation | https://openwrt.github.io/luci/jsapi/ |
| Config detection | Scrape live site HTML for embedded jsdoc config path; fallback to `jsdoc.conf.json` |
| Source directory | `modules/luci-base/htdocs/luci-static/resources/` |
| Processing tool | `jsdoc-to-markdown` per file, `--heading-depth 2 --global-index-format none` |
| Output prefix | `luci-api-` |
| Minimum content threshold | Skip output with fewer than 15 words |

### 4.3 OpenWrt Wiki

| Property | Value |
|---|---|
| Source | https://openwrt.org/ |
| Discovery method | Sitemap XML at `https://openwrt.org/sitemap.xml` |
| Age filter | Read `<lastmod>` from sitemap XML; skip pages older than 2 years. One HTTP request for all page metadata. |
| Export endpoint | Append `?do=export_raw` — returns raw DokuWiki markup, no HTML rendering artifacts |
| Conversion tool | `pandoc -f dokuwiki -t gfm --wrap=none` |
| Crawl scope | Pages under `/docs/techref/` and `/docs/guide-developer/` only |
| Skip patterns | `/toh/`, `/inbox/`, `/meta/`, `/playground/`, `changelog`, `release_notes` |
| Minimum content length | 200 characters after conversion (skip stub pages) |
| Request delay | 1.5 seconds between HTTP requests |
| Output filename convention | Derived from URL path, e.g. `/docs/techref/ubus` → `openwrt-techref-ubus.md` |
| On failure | Wiki scraping failures are non-fatal — the workflow continues without wiki output |

### 4.4 OpenWrt Buildroot Source Annotations

| Property | Value |
|---|---|
| Source repository | https://github.com/openwrt/openwrt |
| Clone strategy | `git clone --depth=1 --filter=blob:none --sparse`, checking out only `package/`, `include/`, `scripts/` |
| Extracted content | `PKG_DESCRIPTION`, `PACKAGE_DESCRIPTION`, `PKG_VERSION`, `PKG_LICENSE`, `PKG_MAINTAINER`, `PKG_SOURCE_URL` from Makefiles; README files verbatim; header comment blocks from `include/*.mk` |
| Output grouping | One file per top-level package category, plus one file for `include/*.mk` |
| README cap | 2000 characters per package, with a note pointing to the source URL |
| Minimum threshold | Skip packages with no extractable README and no description fields in Makefile |
| Output prefix | `openwrt-buildroot-` |

### 4.5 Curated LuCI Application Examples

Source location: `applications/` within the already-cloned `repo-luci/`.
Full URL: `https://github.com/openwrt/luci/tree/master/applications`

Four apps selected, each demonstrating a distinct development pattern:

| App | Pattern | Key concepts taught |
|---|---|---|
| `luci-app-example` | Hello world / baseline | Minimum viable app structure, ucode↔JS bridge, ACL, UCI form, rpcd scaffolding |
| `luci-app-commands` | HTTP API / controller | Custom HTTP endpoints, URL parsing via `luci.http.urldecode`, secure `popen` |
| `luci-app-ddns` | Standard config app | Service state checking, rpcd microbus, deep UCI config read/write |
| `luci-app-dockerman` | Advanced / streaming | UNIX socket communication, HTTP streaming, large JSON, multi-file architecture |

**Extraction rules:**
- Copy all `.uc` (ucode backend) and `.js` (JavaScript frontend) files
- Preserve internal directory structure with `cp --parents`
- Do not copy images, Makefiles, translation files, or test fixtures
- Leave all files completely unmodified — no header injection, no reformatting
- If fewer than 3 `.uc`/`.js` files are found in an app directory, log a warning
  and skip that app; do not fail the workflow

### 4.6 GitHub Models AI Summarization

| Property | Value |
|---|---|
| Model identifier | `openai/gpt-4o-mini` (provider prefix required) |
| API endpoint | `https://models.github.ai/inference/chat/completions` |
| Authentication | `$GITHUB_TOKEN` — automatically available in GitHub Actions; no extra secrets |
| Free tier availability | All GitHub accounts; no Copilot subscription required |
| Rate limit tier | Low — approximately 150 requests/day |
| Token limits | ~8,192 input tokens, ~4,096 output tokens per request |

**Note on endpoint:** The endpoint `https://models.inference.ai.azure.com` is
deprecated. All implementations must use `https://models.github.ai/inference`.
The model name must include the provider prefix: `openai/gpt-4o-mini`, not
`gpt-4o-mini`. Omitting the prefix will result in a 404 or model-not-found error.

---

## 5. Processing Steps (Workflow Order)

### Step 0: Setup

Install and configure the processing environment:
- Node.js 20 (via `actions/setup-node`)
- Python 3.12 (via `actions/setup-python`)
- System packages: `pandoc` (via `apt-get`)
- Node packages: `jsdoc-to-markdown` (global install via `npm install -g`)
- Python packages: `requests`, `beautifulsoup4`, `lxml`
- Create all output directories
- Clear stale files from previous runs with `rm -f` on each output directory's
  `.md` files and `llms.txt` files

### Step 1: Detect jsdoc Config Paths from Live Documentation Sites

Before cloning anything, fetch the HTML of the live documentation websites and
search for the embedded jsdoc config file path. Write results to `$GITHUB_ENV`
(not a separate file) so all subsequent shell steps automatically inherit
`$UCODE_CONF` and `$LUCI_CONF` as environment variables without needing a
`source` command.

Fall back to known defaults (`jsdoc/conf.json` for ucode, `jsdoc.conf.json` for
luci) if detection fails. Detection failures must not abort the workflow.

### Step 2: Clone Upstream Repositories

```bash
git clone --depth=1 https://github.com/jow-/ucode.git repo-ucode \
  || { echo "Failed to clone ucode repo"; exit 1; }

git clone --depth=1 https://github.com/openwrt/luci.git repo-luci \
  || { echo "Failed to clone luci repo"; exit 1; }

git clone --depth=1 --filter=blob:none --sparse \
  https://github.com/openwrt/openwrt.git repo-openwrt \
  || { echo "Failed to clone openwrt repo"; exit 1; }
```

**Error handling requirement:** All `git clone` commands must use the
`|| { echo "..."; exit 1; }` pattern — not `|| true`. Clone failures are fatal
because no downstream step can produce meaningful output without the source
repositories. The failure message must identify which repo failed. This
distinction matters: upstream repos (git clones) are fatal failures; downstream
scraped data sources (wiki) are non-fatal.

**Record commit hashes into `$GITHUB_ENV`** for use in file metadata headers
and the final git commit message:
```bash
echo "UCODE_COMMIT=$(git -C repo-ucode rev-parse --short HEAD)" >> $GITHUB_ENV
```

### Step 3: Generate ucode Documentation

1. Run `npm install --silent` with explicit failure handling:
   ```bash
   npm install --silent || { echo "npm install failed"; exit 1; }
   ```
   npm install failures are fatal — jsdoc2md cannot run without its dependencies.

2. Check whether `$UCODE_CONF` exists in the repo; set `$CONF_ARG` only if it
   does. jsdoc2md functions correctly without `--configure`.

3. **Heredoc indentation rule (applies to all heredocs throughout the workflow):**
   Heredoc content lines must be indented to match the heredoc closing delimiter
   column, not the surrounding YAML step indentation. The closing delimiter
   (`LLMS_EOF` etc.) must not be indented further than the content lines, or the
   shell will not recognize it as the delimiter. Wrong indentation silently
   produces heredocs that include all subsequent lines until end-of-file.
   ```bash
   # CORRECT — delimiter and content at same indentation level:
   cat > "$OUT/llms.txt" << LLMS_EOF
   # Content line at column 0
   # Another content line
   LLMS_EOF

   # WRONG — content indented further than delimiter:
   cat > "$OUT/llms.txt" << LLMS_EOF
             # Content unexpectedly included as literal text
   LLMS_EOF
   ```

4. **jsdoc2md stderr handling:** Redirect stderr to a named file (`jsdoc.err`),
   not to `/dev/null`. Discarding stderr with `/dev/null` hides errors that are
   useful for debugging when a module produces no output unexpectedly:
   ```bash
   OUTPUT=$(jsdoc2md $CONF_ARG --heading-depth 2 --global-index-format none \
     "$src" 2>jsdoc.err || true)
   ```

5. Filter: skip output with fewer than 15 words.

6. Prepend metadata block to each output file (source URL, live docs URL,
   generation timestamp, upstream commit hash).

7. Write `ucode-docs/llms.txt` with one descriptive line per file.

8. Do **not** assemble the single-file reference yet — cross-reference injection
   (Step 8) must run first.

### Step 4: Generate LuCI JS API Documentation

Same structure as Step 3. Apply the same heredoc indentation rule, the same
jsdoc2md stderr-to-file pattern, and the same 15-word filter.

Source directory: `modules/luci-base/htdocs/luci-static/resources/`

Live doc URL construction:
- Top-level class: `https://openwrt.github.io/luci/jsapi/LuCI.html`
- All other modules: `https://openwrt.github.io/luci/jsapi/LuCI.{modname}.html`

Do **not** assemble single-file reference yet.

### Step 5: Scrape OpenWrt Wiki

**Non-fatal step.** All failures in this step must use `exit(0)`, not `exit(1)`.
If openwrt.org is unreachable, the workflow should continue and produce all other
documentation outputs. The wiki output directories will simply be empty.

```python
# CORRECT:
except Exception as e:
    print(f"WARNING: Could not fetch sitemap: {e}")
    print("Skipping wiki documentation generation.")
    exit(0)   # graceful — do not fail the workflow

# WRONG:
except Exception as e:
    print(f"FATAL: Could not fetch sitemap: {e}")
    exit(1)   # kills the entire workflow run
```

Processing order:
1. Fetch `https://openwrt.org/sitemap.xml` (one request for all page metadata)
2. Parse `<loc>` and `<lastmod>` for every `<url>` entry
3. Filter to `/docs/techref/` and `/docs/guide-developer/` paths only
4. Apply skip patterns: `/toh/`, `/inbox/`, `/meta/`, `/playground/`, `changelog`,
   `release_notes`
5. Drop pages with `<lastmod>` older than 2 years (no page fetch needed)
6. Fetch `{url}?do=export_raw` for remaining pages
7. Run `pandoc -f dokuwiki -t gfm --wrap=none` on each raw response
8. Skip output under 200 characters
9. Prepend metadata block (source URL, lastmod from sitemap, fetch timestamp)
10. Write `openwrt-wiki-docs/llms.txt`
11. Enforce 1.5-second delay between HTTP requests

Do **not** assemble single-file reference yet.

### Step 6: Extract OpenWrt Buildroot Documentation

1. Iterate over top-level category directories in `repo-openwrt/package/`
2. Extract Makefile metadata and README content per package
3. Group by category into one output file per category
4. Extract leading comment blocks from `include/*.mk`
5. Skip packages with no extractable content
6. Cap README at 2000 characters with a source link note if truncated
7. Write `openwrt-buildroot-docs/llms.txt`

Do **not** assemble single-file reference yet.

### Step 7: Extract Curated LuCI Application Examples

Apply the heredoc indentation rule to the `llms.txt` generation heredoc.

For each of the four apps:
1. Check the directory exists; skip with a warning if not
2. Count `.uc` and `.js` files; if fewer than 3, log a warning and skip — do
   not fail the workflow
3. Copy with `cp --parents` to preserve internal directory structure
4. Files are copied raw and unmodified — no header injection

Do **not** assemble single-file reference yet.

### Step 8: Cross-Reference Injection (Pure Python, No AI, No Cost)

Runs **before** Step 11 (assembly) so both individual files and the concatenated
complete references contain the cross-reference links.

All injected links use **absolute root-relative paths** (e.g.
`/luci-docs/luci-api-rpc.md`), not relative paths between files. Relative paths
break when individual files are concatenated into the root-level complete
reference documents at a different directory depth.

**Symbol index construction:**
1. Scan all generated markdown files in `ucode-docs/`, `luci-docs/`,
   `openwrt-wiki-docs/`, `openwrt-buildroot-docs/`
2. For each heading matching a symbol name pattern, record the root-relative URL
3. **Priority rule:** API reference files (`ucode-docs/`, `luci-docs/`) take
   precedence over wiki and buildroot files as the canonical definition source
4. **Collision logging:** When two API reference files define the same symbol,
   log a warning rather than silently overwriting:
   ```python
   elif this_is_api and ("ucode-docs" in current or "luci-docs" in current):
       print(f"Warning: API symbol collision for {symbol} between {current} and {root_url}")
   ```
5. Minimum symbol name length: 4 characters (shorter names produce too many
   false positive matches in body text)

**Injection algorithm — collect-then-apply-reverse (required pattern):**

Do **not** use offset tracking (accumulating a character offset as insertions
are made). Offset tracking is error-prone when multiple insertions occur in the
same file. The correct approach:

1. Collect all insertion positions into a list: `(start, end, replacement)`
2. Sort the list in **reverse order** by start position
3. Apply insertions from the end of the file backwards

Applying in reverse order means each insertion does not shift the character
positions of earlier insertions, making the algorithm correct by construction:

```python
# CORRECT: collect, sort reverse, apply
insertions = []
for symbol, target_url in sorted(symbol_index.items(), key=lambda x: -len(x[0])):
    if target_url == this_root_url:
        continue
    for m in re.finditer(rf'\b({re.escape(symbol)})\b(?!\()', original):
        if not any(i in protected for i in range(m.start(), m.end())):
            insertions.append((m.start(), m.end(), f"[{symbol}]({target_url})"))
            protected.update(range(m.start(), m.end()))

insertions.sort(key=lambda x: x[0], reverse=True)
for start, end, replacement in insertions:
    modified = modified[:start] + replacement + modified[end:]

# WRONG: offset tracking (causes incorrect positions on second+ insertion)
offset = 0
for ...:
    adj_start = m.start() + offset
    adj_end   = m.end()   + offset
    modified  = modified[:adj_start] + replacement + modified[adj_end:]
    offset   += len(replacement) - len(symbol)  # fragile
```

**File writing:** All file writes in Python must use `with open()` context
managers, never bare `open().write()` calls:
```python
# CORRECT:
with open(fpath, "w", encoding="utf-8") as f:
    f.write(modified)

# WRONG:
open(fpath, "w", encoding="utf-8").write(modified)
```
The `with` statement guarantees the file handle is closed even if an exception
occurs mid-write, preventing silent truncation of output files.

**Protected range tracking:** Before scanning for symbol names, build a set of
character positions that are inside fenced code blocks, inline code spans, or
existing markdown links. Do not inject links into these ranges.

### Step 9: Deprecation Checker (Pure Python, No AI, No Cost)

**Deprecated symbol detection window:** Use a **1500-character** lookahead
window after each symbol heading, not 300. The `**Deprecated**` marker in
jsdoc-to-markdown output may appear after a description, parameter list, and
return value documentation, which can easily exceed 300 characters. Using 300
characters risks missing many deprecated symbols:

```python
# CORRECT:
window = content[m.end():m.end() + 1500]

# WRONG (too small — misses many deprecated markers):
window = content[m.end():m.end() + 300]
```

When a deprecated symbol is found in a wiki file, inject a GitHub-flavored
markdown `> [!WARNING]` callout after the first `---` separator.

All file writes must use `with open()` context managers (same rule as Step 8).

### Step 10: AI Post-Processing via GitHub Models

**API endpoint and model identifier (critical — these changed from v4):**

| Property | Correct value | Deprecated / wrong value |
|---|---|---|
| Endpoint | `https://models.github.ai/inference/chat/completions` | `https://models.inference.ai.azure.com/chat/completions` |
| Model name | `openai/gpt-4o-mini` | `gpt-4o-mini` |

The provider prefix (`openai/`) in the model name is required. Omitting it
produces a model-not-found error. The old Azure endpoint is deprecated and will
not work.

**API response validation:** Never access nested response keys with direct
dictionary indexing. The API may return unexpected response shapes on errors.
Always use `.get()` with appropriate fallbacks:

```python
# CORRECT — safe access:
resp_json = r.json()
if not resp_json.get("choices") or not resp_json["choices"]:
    print("  API returned empty choices — skipping this file")
    return "SKIP"
message = resp_json["choices"][0].get("message", {})
content = message.get("content", "")
return content.strip()

# WRONG — will crash on unexpected response shapes:
return r.json()["choices"][0]["message"]["content"].strip()
```

**Budget management:**
- Hard cap: 40 files per run
- Priority: ALL `ucode-module-*.md` files first (~15–18 files), then
  `luci-api-*.md` files with remaining budget
- Skip files that already contain `**Summary:**` (idempotent across runs)
- 1.5-second delay between API calls
- On HTTP 429: stop the step cleanly, log how many files were processed, do
  not retry, do not fail the workflow
- Skippable via `workflow_dispatch` input `skip_ai`

All file writes must use `with open()` context managers.

**This step is skipped for:** wiki docs, buildroot docs, example source files.

### Step 11: Assemble Single-File References + Promote Static Docs

Runs **after** Steps 8–10 so all enhancements (cross-references, deprecation
warnings, AI summaries) are present in both the individual modular files and
the concatenated complete reference files.

Five complete reference files produced at the repo root:
- `ucode-complete-reference.md`
- `luci-jsapi-complete-reference.md`
- `openwrt-wiki-complete-reference.md`
- `openwrt-buildroot-complete-reference.md`
- `openwrt-examples-complete-reference.md`

Each file structure: title + source URLs + timestamp → description paragraph →
table of contents → `---` separator → all individual files concatenated,
separated by `---`.

For the examples complete reference, each embedded source file is wrapped in a
labelled fenced code block identifying the app, filename, and file type
(ucode backend vs JavaScript frontend).

**Static docs promotion:** Copy files from `static-docs/` to the repo root.
If `static-docs/` is absent or empty, log a note and continue without failing.

### Step 12: Generate Root llms.txt

Generate `llms.txt` dynamically from files that actually exist in the output.
Do not use a hardcoded template — files may be absent if steps were skipped.
Follows the llmstxt.org standard format (see Section 3.3).

### Step 13: Publish to GitHub Pages

Use pinned action versions:
```yaml
- uses: actions/upload-pages-artifact@v4   # v4, not v3
  with:
    path: '.'
- uses: actions/deploy-pages@v4
```

**Action version pinning requirement:** Always use the current major version
of official GitHub Actions. `upload-pages-artifact@v3` is outdated; use `@v4`.
Outdated action versions may produce deprecation warnings or fail silently.

Remove cloned repos (`repo-ucode`, `repo-luci`, `repo-openwrt`) **before** the
`upload-pages-artifact` step. These directories must not be served via GitHub
Pages and can be hundreds of megabytes.

Requires `pages: write` and `id-token: write` in the workflow `permissions`
block. GitHub Pages source must be set to "GitHub Actions" in repository
settings before first use.

### Step 14: Commit Generated Files Back to Repository

**`git add` with `--all` flag:** Use `git add --all <path>` rather than plain
`git add <path>`. The `--all` flag ensures that deletions are tracked — if a
wiki page was removed or renamed upstream, its corresponding `.md` file will be
removed from the commit. Without `--all`, deleted files remain in the repository
indefinitely:

```bash
# CORRECT — tracks additions, modifications, AND deletions:
git add --all ucode-docs/
git add --all luci-docs/
[ -d "$d" ] && git add --all "$d/" || true

# WRONG — misses deletions:
git add ucode-docs/
```

**`git push` is non-fatal:** The commit step uses `|| true` (correct, since
no changes is a valid state), but the push step should use `|| echo "..."` to
prevent workflow failure on transient push issues while still logging the
problem:

```bash
git commit -m "..." || echo "No changes to commit — output identical to previous run."
git push || echo "Git push failed — artifact was still deployed to Pages successfully"
```

The Pages artifact is uploaded before the commit step, so a push failure does
not prevent the documentation from being published.

---

## 6. Workflow Trigger and Schedule

```yaml
on:
  schedule:
    - cron: '0 2 1 * *'      # Monthly on the 1st at 02:00 UTC
  workflow_dispatch:
    inputs:
      skip_wiki:
        description: 'Skip OpenWrt wiki scraping (faster run)'
        type: choice
        options: ['false', 'true']
        default: 'false'
      skip_buildroot:
        description: 'Skip buildroot source extraction (faster run)'
        type: choice
        options: ['false', 'true']
        default: 'false'
      skip_ai:
        description: 'Skip AI summarization (saves GitHub Models quota)'
        type: choice
        options: ['false', 'true']
        default: 'false'

permissions:
  contents: write
  pages: write
  id-token: write

concurrency:
  group: generate-llm-docs
  cancel-in-progress: true
```

Monthly cadence aligns with the pace of OpenWrt upstream changes, minimizes
load on openwrt.org servers, and fits comfortably within all free tier limits.

---

## 7. Tool Selection Rationale

| Tool | Alternative | Reason for selection |
|---|---|---|
| `?do=export_raw` + pandoc dokuwiki | `?do=export_xhtml` + html2text | Raw markup is the actual source; no HTML rendering artifacts; pandoc has a native DokuWiki parser |
| `sitemap.xml` for age filtering | Fetch each page to read embedded date | 1 HTTP request for all age data vs N requests |
| `pandoc -f dokuwiki -t gfm` | Python `html2text` | Handles DokuWiki tables, code blocks, nested lists natively; html2text is HTML-only |
| `jsdoc-to-markdown` per file | Single run across all files | Per-file produces granular named outputs; all-at-once produces one unseparated blob |
| Sparse checkout for buildroot | Full clone | Full buildroot is multi-gigabyte; sparse gets only needed subdirs |
| `openai/gpt-4o-mini` via GitHub Models | External AI API | Zero cost; uses `$GITHUB_TOKEN`; no additional secrets required |
| Root-relative paths in cross-refs | Relative paths between files | Relative paths break when files are concatenated into root-level references |
| Collect-then-apply-reverse for cross-refs | Offset tracking | Offset tracking is fragile with multiple insertions; reverse application is correct by construction |
| `with open()` context managers | Bare `open().write()` | Guarantees file handles are closed on exception; prevents silent truncation |
| `git add --all` | Plain `git add` | Tracks deletions in addition to additions and modifications |

---

## 8. Error Handling and Resilience

The distinction between **fatal** and **non-fatal** failures is a first-class
design requirement:

| Category | Examples | Handling |
|---|---|---|
| **Fatal** — abort the run | git clone fails, npm install fails | `\|\| { echo "..."; exit 1; }` — fail loudly with a descriptive message |
| **Non-fatal** — skip and continue | wiki unreachable, single page fetch fails, AI rate-limited, app directory missing | `exit(0)` in Python scripts; `\|\| true` or `\|\| echo "..."` in shell |

Full error handling reference by step:

| Failure scenario | Category | Handling |
|---|---|---|
| `git clone` fails | Fatal | `\|\| { echo "Failed to clone X repo"; exit 1; }` |
| `npm install` fails | Fatal | `\|\| { echo "npm install failed"; exit 1; }` |
| jsdoc2md produces no output | Non-fatal | 15-word filter silently skips |
| jsdoc2md produces stderr | Informational | Redirect to `jsdoc.err`; not discarded to `/dev/null` |
| `sitemap.xml` unreachable or unparseable | Non-fatal | Python `exit(0)` with warning message |
| Individual wiki page fetch fails | Non-fatal | Log and continue; do not fail the step |
| AI step hits HTTP 429 | Non-fatal | Stop AI step cleanly; log files processed; continue workflow |
| `static-docs/` absent | Non-fatal | Log note; skip promotion; continue |
| App directory has < 3 source files | Non-fatal | Log warning; skip app; continue |
| No changes since last run | Non-fatal | `git commit ... \|\| echo "No changes"` |
| `git push` fails | Non-fatal | `git push \|\| echo "Push failed — Pages still deployed"` |
| `upload-pages-artifact` receives empty dirs | Informational | Directories from skipped steps are simply absent |

Every generated file includes its generation timestamp and upstream commit hash
in its metadata header, making staleness always visible to readers.

---

## 9. Shell Scripting Standards

All shell code in the workflow must conform to these requirements:

**Variable quoting:** Quote all variable expansions that expand to filenames or
directory paths, especially when used as arguments to commands like `ls`:
```bash
# CORRECT:
ls "$d"/*.md 2>/dev/null | wc -l

# WRONG — fails if $d contains spaces or special characters:
ls $d/*.md 2>/dev/null | wc -l
```

**Heredoc indentation:** Heredoc closing delimiters and content lines must be
at the same indentation column. In a GitHub Actions `run:` block indented to
column 10, the heredoc content and closing delimiter should be at column 10 or
less. Content that is further indented than the delimiter appears as literal
text in the output (see Step 3 for a detailed example).

**Tool stderr:** Never discard jsdoc2md or similar tool stderr to `/dev/null`.
Use a named file (`2>jsdoc.err`) so output is available for debugging when a
module produces unexpectedly empty output.

**Fatal vs non-fatal pattern:**
```bash
# Fatal (stops the workflow):
some_critical_command || { echo "Descriptive failure message"; exit 1; }

# Non-fatal (logs and continues):
some_optional_command || echo "Optional step failed — continuing"

# Idempotent (no changes is valid):
git commit -m "..." || echo "No changes to commit"
```

---

## 10. Python Coding Standards

All Python embedded in `run:` shell steps must conform to these requirements:

**Context managers for all file writes:**
```python
# CORRECT:
with open(fpath, "w", encoding="utf-8") as f:
    f.write(content)

# WRONG:
open(fpath, "w", encoding="utf-8").write(content)
```

**Safe dictionary access for API responses:**
```python
# CORRECT — handles unexpected response shapes:
choices = resp_json.get("choices") or []
if not choices:
    return "SKIP"
message = choices[0].get("message", {})
content = message.get("content", "")

# WRONG — crashes on unexpected shapes:
content = resp_json["choices"][0]["message"]["content"]
```

**Non-fatal Python steps** must use `exit(0)` (not `exit(1)` or `sys.exit(1)`)
when encountering recoverable failures that should allow the workflow to continue.

**Import all standard library modules at the top of each embedded script.**
Do not use `__import__()` for deferred imports of standard library modules like
`datetime`; this is needlessly obscure and harder to read.

---

## 11. What Is Intentionally Excluded

| Feature | Reason excluded |
|---|---|
| SYSTEM-PROMPT.md / concepts-glossary.md / openwrt-recipes.md generation | Requires deep judgment and many AI tokens; better generated locally |
| OpenWrt forum Q&A scraping | High value but Discourse API scraping is a separate project |
| Git commit message extraction | High value; deferred to v6 |
| Map-reduce synthesis | Exceeds GitHub Models free daily quota for a single run |
| Archive.org fallback for deleted wiki pages | Adds significant complexity; deferred |
| Version-tagged GitHub Releases | Good idea; deferred to v6 after core pipeline is validated |
