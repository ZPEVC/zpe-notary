# The notary, in plain words

You made a claim. You have a file that proves it. Somebody will later ask whether the file is the real one, or
whether you wrote it after the fact.

This repo answers that. You put the file's fingerprint in a public list, sign the list, and push it. The day you
pushed is on GitHub's clock, not yours. Later, anyone can take their copy of the file, fingerprint it, and see
whether it matches what you published, and on what day.

## The locker analogy

A notary with a locker costs money and an appointment. This is a locker in a public corridor:

1. You drop in a sealed envelope with a fingerprint of your document written on the outside.
2. You never put the document in, only its fingerprint.
3. Anyone can look through the glass and read the fingerprint and the date.
4. If you later produce a document, that fingerprint is either the one in the locker or it is not.

## What it costs

Nothing. It is a git repository.

## What it does not do

- It does not tell anyone your document is right. Only that it is the same document, from that day.
- It does not keep secrets, because it never sees the content, only the hash.
- It does not stop you rewriting history. It makes rewriting visible to everyone who has a copy.

## Try it in one minute

```sh
sha256sum my-report.pdf
```

Take that long number. Search for it in this repository (`records/`). If it is there, note the date of the commit
that put it there. That is the whole product.
