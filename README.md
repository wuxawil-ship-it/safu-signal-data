# safu-signal-data

Machine-written data for the SAFU Signals dashboard. **Nothing here is edited by
hand.** The bot rewrites these files after each scan and on any material change
to an open position, and the four boards fetch them at run time.

| file | what it is |
|---|---|
| `dashboard/signals.json` | every published crypto signal the boards score |
| `dashboard/gold.json` | the gold engine's own rows, kept separate on purpose |

## Why this repo exists

The dashboard's code and its data used to live in one repository. The bot
rewrites the data about **30 times a day**, and the host rebuilt the whole site
on every one of those pushes — roughly **930 builds a month** against a free
allowance in the hundreds. The pipeline ran out partway through each month and
the board silently served a snapshot **17 hours old** while still reading
"Live".

A data file that changes 30 times a day must not trigger a site build. So the
data moved here and the page reads it over HTTP instead. The site is now rebuilt
only when its own code changes — about ten times a month.

## What is NOT here

The bot, its configuration, its tests and its subscriber state. Those stay in a
**private** repository and must never be made public.

These files carry trade rows only: symbol, direction, prices, timestamps and the
recorded excursions. No chat ids, no exchange UIDs, no credentials.
