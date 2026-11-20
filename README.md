# Smart Notes

A tiny notes app: write notes, search them, and get an instant summary of any note.
Single file (`index.html`), no build step, no dependencies. Notes are stored in your browser (`localStorage`).

Built with an AI coding agent and verified end to end with [Kane CLI](https://www.testmuai.com/kane-cli/) in a real Chrome browser.

## Features

- Add a note (title + body). Empty title or body shows an error.
- Search notes by title or text.
- **Summarize**: picks the most important sentences (word-frequency scoring). Notes with fewer than 2 sentences show a "Too short to summarize" message.
- Word count per note, note counter, delete.
- Notes survive a page reload.

## Run it

```
npx serve .
```

Open the URL it prints (usually http://localhost:3000).
You can also just double-click `index.html`.

## Verify with Kane CLI

Install and log in once:

```
npm install -g @testmuai/kane-cli
kane-cli --tui
```

With the app running, paste each objective into Kane:

1. `Open http://localhost:3000. Click Save note without typing anything. Verify an error saying "Title is required" is shown.`
2. `Open http://localhost:3000. Type "Meeting" as the title and "The launch is on Friday. The launch needs a demo video. Lunch is at noon. The demo video must show the launch." as the note. Click Save note. Verify a note titled Meeting appears and the counter says 1 note.`
3. `Open http://localhost:3000. Add a note titled Meeting with the body "The launch is on Friday. The launch needs a demo video. Lunch is at noon. The demo video must show the launch." Click Summarize on that note. Verify a Summary appears and it is shorter than the original note.`
4. `Open http://localhost:3000. Add a note titled Meeting with some text. Type zzzz in the search box. Verify the page says No matching notes.`
5. `Open http://localhost:3000. Click Delete on every note on the page until none are left. Verify the page says No notes yet.`

## The build -> verify -> fix loop

1. The coding agent builds or changes the app.
2. Kane CLI runs the objectives above in a real browser and returns pass or fail with evidence.
3. If something fails, the failure report goes back to the agent, which fixes the app.
4. Kane runs again until every objective passes.

### What Kane found in this project

- Run 1 (real Chrome via Kane CLI): 5 of 5 objectives passed (empty-title error, add note, summarize, search with no match, delete).
- Kane keeps its own browser profile, so notes persist between runs. The delete objective was worded as "delete every note until none are left" so it passes regardless of leftover notes (a test-isolation fix, not an app bug).

## License

MIT, see `LICENSE`.
