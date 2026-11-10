# zpe-notary

An append-only public record of hashes. Git's commit timestamp is the third party: we cannot change the time a
commit was made, so a hash published here can be shown to have existed at that moment.

## What it attests

1. **These bytes existed at this time.** The record carries a SHA-256 per artifact and the commit carries the date.
2. **Nothing was rewritten quietly.** Each record names the hash of the record before it, so the file chain is
   checkable end to end, and git's own history is the backstop for the chain itself.
3. **Someone with a key stood behind it.** Records are signed with an SSH key; `allowed_signers` is in this repo, so
   verification needs no trust in our machine.

## What it does not attest

- **Not truth.** A notary says the paper was filed, not that the claim on it is right.
- **Not identity beyond the key.** Whoever holds the private key can publish; the signature says the same key signed
  both records, not that a particular person did.
- **Not deletion-proof.** Git history can be rewritten by force-push. The defence is that copies exist: every clone
  and every fork keeps the old commit. If a record ever disappears from `main`, the disappearance is the evidence.

## Check a record yourself

```sh
git clone https://github.com/ZPEVC/zpe-notary && cd zpe-notary
ssh-keygen -Y verify -f allowed_signers -I zpe-evidence -n evidence \
  -s records/<record>.json.sig < records/<record>.json
sha256sum <your copy of the file>    # must equal the row's sha256
```

## Records

`index.json` lists every record with its own hash and how many rows it carries. Records live in `records/`, one file
per publication, with a detached `.sig` beside it.

## Submitting your own

The contract is a pull request: add `records/<UTC-stamp>-<slug>.json` shaped as `zpe.notary.record/1`, sign it with
your own key, and add your key to `allowed_signers` under your own identity. A record is accepted when it verifies
against the key it names. The timestamp that matters is the merge commit's.

## Who runs it

ZPE. The first record covers our own sites, because a notary that only ever notarises other people is a marketing
page.

## Verification commands used to produce the first record

```
POST https://zpe.vc/audit/api/crawl {"url": "https://motohorek.life", "email": "<recipient>"}
GET  https://zpe.vc/audit/s/112410dd5b91.json
google-search-console-cli query "sc-domain:motohorek.life" --start-date 2026-10-10 --end-date 2026-11-06 \
  --data-state final --dimensions query --row-limit 250 --all
```
