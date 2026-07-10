# PR Response Doc — CineLog Watchlist Feature

## AI Usage

<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename

**What I did:**
Renamed save_to_watchlist() to add_to_watchlist() in services/watchlist_service.py, then updated the import and call site in routes/watchlist/watchlist.py.
**How I verified:**
Used a project-wide search for save_to_watchlist and add_to_watchlist to locate every reference before editing. That search showed three matches: the function definition in services/watchlist_service.py, plus the import and the call in routes/watchlist/watchlist.py. After the rename, I reran the same search to confirm there were no remaining save_to_watchlist references and that all expected add_to_watchlist references were present.

## Comment 2 — Deduplication

**What I did:**
Added deduplication logic to add_to_watchlist() in services/watchlist_service.py using the same pattern as add_to_collection(). The function now checks WatchlistEntry for an existing row with the same user_id and film_id before creating a new entry. If it finds one, it raises AlreadyInWatchlistError instead of creating a duplicate. I also updated routes/watchlist/watchlist.py to catch that error and return a 409 response, matching the collection route pattern.
**How I verified:**
Read add_to_collection() in services/collection_service.py and confirmed its deduplication check queries for an existing CollectionEntry with the same user_id and film_id, then raises AlreadyInCollectionError when a duplicate is detected. After writing the watchlist version, I searched for AlreadyInWatchlistError and add_to_watchlist to confirm the new exception is defined, raised, imported, and handled by the route.

## Comment 3 — Missing test

**What I did:**
**How I verified:**

## Comment 4 — Default visibility

**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order

**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase

**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description

<!-- Written at the end — feature overview, design decisions, manual testing steps -->
