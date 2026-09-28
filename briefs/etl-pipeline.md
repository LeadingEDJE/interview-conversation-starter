# Brief — ETL pipeline

> **Marcus, ops lead, retail distributor**
>
> One of our suppliers sends us a product feed. It is not good. Every time we load it
> something's off and we find out a week later when a price is wrong on the site.
>
> The file's in the repo — `data/supplier-feed.jsonl`, one JSON object per line. Have a
> look at it, it'll tell you more than I can. Prices come through in a couple of different
> formats, some rows are missing things they shouldn't be missing, and the same product
> shows up more than once — sometimes byte-for-byte identical, sometimes not quite.
>
> Two things I really need. It can't fall over because of one bad row; last time that
> happened we lost the whole night's load. And I need to be able to run it again if I'm not
> sure it worked, without ending up with everything twice.
>
> At the end just tell me what happened. How many went in, how many didn't, what was wrong
> with the ones that didn't.

## What it needs to do

1. **Read the feed, normalise it, and load it** into a store of your choice.
2. **Running it twice leaves the data in the same state as running it once.**
3. **A bad record doesn't stop the run**, and the run prints a summary at the end saying
   what happened.

The feed is at [`../data/supplier-feed.jsonl`](../data/supplier-feed.jsonl), relative to
this brief — 150 records.

## Not in scope — please don't build these

We mean this. These are the things that turn an hour into an afternoon, and we're not
looking for them:

- An HTTP API or any endpoint over the loaded data
- Incremental or streaming loads
- A scheduler, cron, or orchestrator
- A real warehouse, if SQLite or a file on disk will do
- Retries and backoff
- Parallel or concurrent processing — 150 records does not need it
- A data-quality report beyond the run summary
- Validating anything the three requirements don't need
- A config-driven mapping layer or transformation DSL
- A UI
- Migrations, CI config, structured logging, or metrics

If you're reaching for one of these, that's the signal to stop.

## Done

When those three things work, and it runs in a container, and you can show it working —
**you are done. Stop.**
