# Tradebook Analyzer

A single-page tool for Zerodha F&O tradebooks. Drop in your tradebook (.xlsx or .csv) and it:

- matches each buy and sell into round trips (first in, first out)
- flags trades that broke your own rules: held overnight, added to a losing position, entered after a cutoff time, loser held too long, entered after the daily loss limit, chasing after losses
- leads with a plain-language verdict, your biggest leak, and a ranked list of which habits cost the most
- shows behavioural patterns that are often linked to worse results: the tilt curve (win rate as losses stack up during the day), bet size after losses, re-entry speed after a loss, red-day endings, and morning vs afternoon. Each card says when the pattern is absent, not only when it is present
- shows win rate, average win and loss, profit per trade, a simple edge test (it tells you when the result is a reliable loss, not just a reliable win), an equity curve with max drawdown, and P&L by day and by entry hour
- warns about contracts that were opened but never closed inside the file, which are left out of every number
- one click copies the whole report as text

Your file is read in the browser. Nothing is uploaded or stored.

## How the numbers are worked out

- **Round trips** are matched first in, first out, per contract.
- **Daily P&L, the equity curve and drawdown** book each trade on the day it closed. **P&L by entry hour** uses the hour it opened.
- **Time held** counts market hours only (09:15 to 15:30 on weekdays), so an overnight position is not treated as a slow exit. Overnight trades have their own rule.
- **Losses so far today** (the tilt curve and the "chasing" rule) counts only trades that had already closed before the new entry.
- **Open positions**: an option that expires worthless usually has no closing trade in the tradebook, so that loss is not in the numbers. The page shows a warning when it finds contracts left open. Compare the gross total with your P&L statement.

## Files

- `index.html`: the whole app (HTML, CSS and JavaScript in one file). It loads the SheetJS library from cdnjs to read .xlsx files, and two fonts from Google Fonts. A .csv file is read without SheetJS, and the page falls back to system fonts if the fonts do not load.

## Host it on GitHub Pages

1. Create a new repository on GitHub, for example `tradebook-analyzer`.
2. Add `index.html` and `README.md` to the repository (Add file, then Upload files).
3. Open the repository's Settings, then Pages.
4. Under Build and deployment, choose Deploy from a branch, select the `main` branch and the `/ (root)` folder, then Save.
5. After a minute the site is live at `https://<your-username>.github.io/<repository-name>/`.

## Using it

Open the page, drop in your tradebook, and adjust the rules at the top (cutoff time, exit time for losers in market minutes, daily loss limit). Enter your total charges from the P&L statement to see net results.

The tradebook needs these columns: Symbol, Trade Type, Quantity, Price, Order Execution Time.
