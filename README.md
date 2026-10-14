# Telai

<img width="1442" height="1002" alt="telai" src="https://github.com/user-attachments/assets/9c1b4384-e8d1-4338-8294-e037b6949ba3" />

Telai is a native macOS terminal for agentic development: a **SwiftUI** app with an embedded **libghostty** terminal and a **vertical-tab sidebar** built around **OpenCode**.

The philosophy of this app is simple: easy tool with few essential features for a human in the loop agentic work.

Each tab is a live terminal session running your AI agent, grouped in the sidebar for easy switching. The app watches the agent's activity — working, waiting for you, done — and surfaces it visually and with local notifications, so you always know where your attention is needed.

Each version is available on the Releases page.

## Why "Telai"

In Italian, _telaio_ is a loom. _Telai_ is its plural. A loom does one thing: it holds the threads together. The **warp** (_ordito_) is strung tight and stays still; the **weft** (_trama_) crosses it back and forth, row after row, and from that crossing a fabric — _una tela_ — comes into being. A tela is also, in Italian, a piece of work, something made through patient interweaving.

That is exactly what you do with an AI agent. You hold the intent and the structure; the agent moves back and forth across it, and what emerges — the work — belongs to neither of you alone. Telai is the loom: it doesn't write the fabric, it holds the threads so you can weave.

## Features

### Terminal sessions with vertical tabs

- One embedded **libghostty** terminal per session, kept alive across tab switches.
- **Vertical tabs in the sidebar**: sessions can sit freely or inside groups.
- Create sessions with `⌘N` or a group's `+`; create groups with `⌥⌘N` (also in the **File** menu).
- Drag a folder from the Finder onto a group to open it there.

### Groups

- Name, optional root folder, and a color.
- The root folder sets where the session's terminal starts (a group `+` opens there instead of your home folder).
- Double-click a group name to rename it inline; click the folder icon or the empty area to collapse/expand.
- Colors come from the Tailwind `-600` palette via **SwiftColors**, applied per variant depending on light/dark appearance.

### Sorting

- Reorder groups, sessions inside a group, and free sessions with native **SwiftUI drag & drop**.
- Drag a session into another group to move it, or out of a group to make it free.

### OpenCode integration

- Detects **OpenCode v1 and v2** at first launch and offers to install a bundled **TUI plugin** into your OpenCode config, adapted to the detected version.
- The plugin reports agent events so the app knows the agent's state even when the terminal still has focus.
- Sessions with an OpenCode session ID are **restored on relaunch** — quitting and reopening brings you back to the same agent session.

### Agent state, always visible

Each session shows its agent state with an SF Symbol and color:

| State       | Icon         | Meaning                               |
| ----------- | ------------ | ------------------------------------- |
| `idle`      | blue circle  | Session just started                  |
| `busy`      | yellow clock | Agent is working                      |
| `done`      | green check  | Agent finished                        |
| `needs you` | red bell     | Agent needs a permission or an answer |

When the app is not focused, a **local notification** tells you the group, folder, and state; clicking it brings the window forward and selects that session. Closing the app or window while an agent is still working shows a confirmation dialog first.

### Toolbar

When a session is selected, the window toolbar shows its `folder · branch` and two actions: open the folder in your **default editor**, or reveal it in the **Finder**. The default editor is chosen from the editors installed in `/Applications`.

### Settings

- A dedicated settings window with **App (General / Sidebar), Terminal, and Agents** sections.
- Settings live in a commented **JSONC** file (`~/.telai/settings/`) with a matching **JSON schema** for editor validation; changes to the file are picked up live.
- Configurable: appearance, window size, sidebar width, terminal font family / size / weight, and the default editor.
- Reset to defaults, Cancel, and Save in the footer.

## Built with

- **SwiftUI** + **SwiftData**
- **libghostty** (via `libghostty-spm`) for the embedded terminal
- **SwiftColors** for the color palette
- **SF Symbols** throughout
- Persistence centralized under `~/.telai`

## Developed with
- Deepseek 4.1 Flash
- GLM 5.3
- Mimo 2.6 Pro
