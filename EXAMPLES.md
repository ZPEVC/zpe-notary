# Worked examples

Three cases, each one a file whose hash is in a record here. The point of an example is that you can follow it to
the end without trusting anyone's summary.

## 1. An audit whose "before" matters

A site audit claims "we added the map pages and the map queries went from 33 clicks to N". The claim is only worth
something if the 33 predates the change.

- The before-state is `seo-baseline-2026-11-09.md`, read from Search Console for 10 October to 6 November 2026.
- Its SHA-256 is in `records/2026-11-10T07-55-18Z.json`.
- The commit that put it there is the timestamp.

Anyone can now check the file they were given against the row, and see the record predates the change. What it does
not prove is that the audit is correct; that is a separate argument with its own evidence.

## 2. A disclosure with a date

The date of a security notice is often the whole argument: who knew, and when.

- Write the notice as a text file. Hash it. Publish the hash the day you send it.
- When the dispute arrives, produce the file. The hash matches, the record is older than the reply.

Nothing is revealed by the notary, because it holds a hash and never the text. If the text itself must be provable
later, publish the file too and hash the file; a hash alone proves sameness, not content.

## 3. A price or a promise you do not want retold

"We quoted 900 for this on 9 November." A screenshot is not evidence; anyone can make one.

- Put the quote as a PDF. Hash it. Publish the hash in the same record as the timestamp.
- If a buyer says the number changed, the comparison is two hashes, not two memories.

## What every example has in common

The notary never holds the document. It holds a fingerprint, a date, and a signature. Everything else is done by
whoever is checking, with tools they already have: `sha256sum` and `ssh-keygen`, both of which ship with their
machine.
