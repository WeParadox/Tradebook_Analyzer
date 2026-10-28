# Tradebook Analyzer

A single-page tool for Zerodha F&O tradebooks. Drop in your tradebook (.xlsx or .csv) and it:

- matches each buy and sell into round trips (first in, first out)
- flags trades that broke your own rules: held overnight, added to a losing position, entered after a cutoff time, loser held too long, entered after the daily loss limit
- shows win rate, average win and loss, profit per trade, a simple edge test, and P&L by day and by entry hour

Your file is read in the browser. Nothing is uploaded or stored.

## Files

- `index.html`: the whole app (HTML, CSS and JavaScript in one file). It loads the SheetJS library from cdnjs to read Excel files.

## Host it on GitHub Pages

1. Create a new repository on GitHub, for example `tradebook-analyzer`.
2. Add `index.html` and `README.md` to the repository (Add file, then Upload files).
3. Open the repository's Settings, then Pages.
4. Under Build and deployment, choose Deploy from a branch, select the `main` branch and the `/ (root)` folder, then Save.
5. After a minute the site is live at `https://<your-username>.github.io/<repository-name>/`.

## Using it

Open the page, drop in your tradebook, and adjust the rules at the top (cutoff time, exit time for losers, daily loss limit). Enter your total charges from the P&L statement to see net results.

The tradebook needs these columns: Symbol, Trade Type, Quantity, Price, Order Execution Time.
