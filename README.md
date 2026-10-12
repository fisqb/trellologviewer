<div align="center">

**Read Trello card change history in your browser.**

Paste a card export, see who changed the description, when, and what exactly changed. No install, no server, no build step. Everything runs locally from a single HTML file.

[![Made with vanilla JS](https://img.shields.io/badge/JavaScript-vanilla-f7df1e?labelColor=1b2550)](index.html)
[![No dependencies](https://img.shields.io/badge/dependencies-none-4ade80?labelColor=1b2550)](.)
[![License: MIT](https://img.shields.io/badge/license-MIT-4ade80?labelColor=1b2550)](LICENSE)

[**Open the viewer**](https://fisqb.github.io/trellologviewer/) · [Features](#features) · [Quick start](#quick-start) · [How it works](#how-it-works) · [Getting a card export](#getting-a-card-export) · [Contributing](#contributing)

</div>

> [!NOTE]
> **This project is a small utility, not an official Trello product.** It reads Trello card JSON exports you provide. Bug reports and fixes are welcome.

```
Input:  a Trello card JSON export
Output: every description change, with author's ID, date, and a line-by-line diff
```

## Quick start

Open the viewer: **[fisqb.github.io/trellologviewer](https://fisqb.github.io/trellologviewer/)**.

Or run it locally - clone the repo and open `index.html` in a browser. The project is a single file:

| File | Role |
| --- | --- |
| `index.html` | Page structure, styles, and all logic |

No build step, no server, no dependencies. Just open `index.html`.

```sh
git clone https://github.com/fisqb/trellologviewer.git
cd trellologviewer
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

The interface has three parts:

| Part | What it does |
| --- | --- |
| **Import panel** | Load a JSON file from disk, or paste JSON manually and press Load pasted JSON |
| **Search and filters** | Search inside diffs, add filter chips for keywords or `author:ID` |
| **Change list** | Every description change as an expandable card with author, date, and diff |

Everything you change is applied live. Click a change header to expand or collapse its diff.

## Features

- **Diff view.** Unified diff of old and new description. Added lines, removed lines, and context.
- **Meaningful vs formatting.** Each change is tagged as a real content change or a whitespace / comma-only edit.
- **Search.** Case-insensitive search inside every diff line and inside the author's ID. Matches are highlighted.
- **Filters.** Add any keyword as a filter chip. Combine multiple keywords. Use `author:ID` to filter by a Trello member ID.
- **Clickable badges.** Click a tag badge or an author badge on any change to add or remove it as a filter.
- **Dark and light theme.** Switch in the header.
- **Help modal.** A short in-app guide for loading, searching, filtering, and reading the diff.

## How it works

Trello card exports contain an `actions` array. Each action has a `type`, a `date`, an `idMemberCreator`, and a `data` object. Description changes show up as `updateCard` actions with `data.old.desc` and `data.card.desc`.

The viewer:

1. Filters `actions` down to `updateCard` entries where the description actually changed.
2. Builds a unified diff between `old.desc` and `card.desc`.
3. Tags each change as meaningful or formatting-only.
4. Renders everything as expandable cards, sorted newest first.

## Getting a card export

1. Open the card in Trello.
2. Use the share menu to export the card as JSON, or open the card JSON URL directly in your browser.
3. Copy the contents, or save the file.
4. Paste it into the viewer, or load the file from disk.

## Contributing

Found a bug, or want to fix one? Both are welcome.

- **Report a bug:** open an issue with the JSON export that reproduces it, or a minimal snippet of the relevant `actions`.
- **Fix a bug:** reproduce it first, fix the cause, then keep the reproduction as an example.
- **Open a pull request:** branch from `main`, keep it to one fix or feature, and say what you tested and on which browser.

The project has no build step, no dependencies, and no test runner. If you can open `index.html` in a browser, you can develop it.

## License

MIT. See [LICENSE](LICENSE).
