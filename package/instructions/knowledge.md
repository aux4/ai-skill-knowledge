# Knowledge Base Skill

A knowledge base in `aux4/kb` is your durable, searchable memory of decisions, facts, and how-things-work — shared with whoever (human or agent) reads it next. This is the method for keeping it high-signal. You run every operation yourself with `aux4 kb` (`add`, `search`, `view`, `list`, `update`, `remove`); this skill is the *discipline*, not a wrapper.

The goal: every entry is findable later and trusted when found. A messy kb is worse than none — it costs reads and returns stale answers.

## Commands: use these exact forms

The title is a positional argument — not a flag. Use these forms verbatim (run `aux4 kb <cmd> --help` only if you need more):

```
aux4 kb search "<query>"                                  # find first — ALWAYS before adding
aux4 kb list                                              # skim what exists
aux4 kb view "<title>"                                    # read one entry in full
aux4 kb add "<title>" --content "<markdown>" --tags a,b   # create (title is positional)
aux4 kb update "<title>" --content "<markdown>"           # CHANGE an existing entry (never add a duplicate)
```

If `add` reports `Entry already exists`, you meant `update`. Verify each write succeeded (look for `Added:`/`Updated:`) before trusting it — a silent error means it was NOT saved.

## Organize: structure and granularity

- **One topic per entry.** An entry answers one question or describes one thing. If you can't write a single sharp title for it, it's two entries.
- **Split vs merge.** Split when an entry grows multiple unrelated sections, or when part of it would be searched for on its own. Merge when two entries always show up together and neither stands alone — duplication is the real cost, not entry count.
- **Use folders for domains, not for single entries.** Group by area the reader thinks in (`auth`, `deploy`, `api`). A folder with one entry is premature; a folder with 40 mixed entries needs sub-grouping. Let structure emerge from volume.
- **Right-size each entry.** Big enough to stand alone without its neighbors; small enough that a reader gets the answer without scrolling past unrelated material. Distill — record the conclusion and the why, not the transcript.

## Standardize: make every entry the same shape

A reader (especially an agent) trusts a kb when entries are predictable. Hold this format:

- **Title** — a specific, searchable claim or noun phrase, not a vague label. Prefer `"deploy: tfstate is local, no remote backend"` over `"deployment notes"`. The title is the strongest search signal — front-load the distinguishing words.
- **Tags** — consistent, lowercase, reused. Pick from tags already in the kb before inventing new ones (`aux4 kb list` to see them). Tag by domain + the few terms a future search would use. 3–6 tags; tags are how cross-cutting topics are found across folders.
- **Content sections** — open with a one-line summary of the takeaway, then supporting detail (decision + why, constraints/gotchas, where things live, what was tried and failed). State conclusions, not narration. Code/paths/commands in backticks so they survive search and copy cleanly.

Standardized entries make `search` precise and `update` safe.

## Link: connect related entries

- **Cross-reference by exact title.** When an entry depends on, supersedes, or contrasts with another, name that entry's title in the content (e.g. `See "auth: oauth web-login design"`). Titles are stable handles; reference them so a reader can `kb view` the linked one.
- **Mark supersession explicitly.** When new knowledge replaces old, say so in both: the new entry notes what it supersedes; the old entry gets a one-line `SUPERSEDED by "<title>"` rather than being silently left to mislead. Never leave two entries that quietly disagree.
- **Shared tags are soft links.** Entries that should be discovered together should share at least one tag, so one search surfaces the whole cluster.

## Search: find before you add, query well

- **Always search before adding.** `aux4 kb search` (and skim `aux4 kb list`) first. If a near-match exists, `update` it instead of creating a near-duplicate. Duplicates are the main way a kb rots.
- **Query strategy:** start specific (the distinctive noun/error/decision), then broaden by dropping qualifiers if you get nothing. Try the term you'd have *titled* it with — that's why titles and tags must be consistent. Search by tag to pull a whole domain cluster.
- **`search` to locate, `view` to read.** `search` returns matches/summaries cheaply; `view` the few that look right for full content. Don't `view` everything — read the top candidates only.
- **No match is information.** A clean miss means it's genuinely new — that's your cue to `add` (well-titled and tagged so the next search finds it).

## Rules

- Search before you add; update over duplicate.
- One topic per entry; sharp, searchable title; reuse existing tags.
- Distill to the conclusion and the why — not a play-by-play.
- Link and mark supersession explicitly; never leave two entries that contradict.
- Keep it lean and high-signal: noise costs every future reader a real read.
- Run `aux4 kb` yourself — this skill is the method, not a tool that calls the LLM for you.
