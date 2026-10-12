# jah-databases-books-shard-1 — Full-Novel Shard

Companion data shard for **The Signature Book Depository Database** (JAH Databases network).
Property of Justin Addam Higgins (JAH).

## Contents

- **Range:** JAH-BOOK-000001 → JAH-BOOK-001000 (1,000 books)
- **What:** the COMPLETE full-length novel for each book — 40,000+ words, 20–24 chapters,
  full four-act arc (setup, rising action, climax, resolution), every chapter complete text.
- **Generator:** `jahdb-books-2.0` (deterministic — seed = book number; regenerating from the
  seed reproduces the stored text byte-for-byte; every record passed `validate()` including
  the independent seed-rebuild checksum before it was written here).
- **Labeling:** every record carries `src: "signature"` and `origin: "signature"`.
  No website references anywhere in the records.

## Layout

- `data/volumes/full-cNNNNN.json.gz` — 10 volumes, 100 full novels each
  (chunk c holds books (c−1)*100+1 … c*100)
- `data/index/full-books.idx.json.gz` — light index: `[{id, t (title), g (genre), w (words), ch (volume)}]`

## Verification

- 1,000 unique IDs, zero duplicates, all in JAH-BOOK-000001…001000
- every novel ≥ 40,000 words (genuinely counted from chapter text)
- every novel: 20+ chapters, all four arc phases present, chapter titles unique,
  no unresolved template tokens
- served over GitHub Pages with CORS enabled; fetched by the database page at
  `…/jah-databases/db/books/` for books 1–1000 (falls back to on-demand generation,
  which reproduces the same text deterministically)
