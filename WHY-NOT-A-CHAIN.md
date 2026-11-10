# Why not a blockchain

The question arrives every time, and it is a fair one.

## What a timestamp actually needs

One property: nobody can backdate it. That is all. Not consensus, not a token, not a wallet.

A public commit gives that property for free: the commit time is set by a system we do not run, and every clone
carries it. If the record is force-pushed away, the clones still hold the old commit, which is exactly the evidence a
dispute needs.

## What a chain adds, and what it costs

A chain buys one more thing: anchoring where no trusted third party exists at all. In exchange it brings a token, a
wallet, gas, key management, and a UX cliff for the person who only wants to check a PDF. For a notary whose users
are freelancers and small agencies, that trade is bad.

## The middle path, if you need an anchor nobody can dispute

OpenTimestamps. `ots stamp records/<record>.json` produces a small `.ots` file that anchors the hash into Bitcoin
through public calendar servers, free, with no wallet and no account. Commit the `.ots` beside the record and a
verifier can check the anchor independently of GitHub.

That is the answer to "should this be on a chain": not our own chain, and not a token, but an OTS anchor when a
dispute would make GitHub's clock insufficient. Until that file exists beside a record, the honest sentence is
"timestamped by GitHub", never "immutable".

## When a chain would be right

If participants are anonymous and mutually hostile, if the record must be verifiable with no server at all, and if
the cost per publication can carry gas. That is a different product from this one.
