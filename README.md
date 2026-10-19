# iwtl

I want to learn!

`iwtl` is a Claude Code skill. It reviews code and teaches you while it does: what the code does, which concepts are in play, what is wrong, why it matters, and how to spot it next time.

## Install

Inside a Claude Code session (version 2.1.275 or later), in one step:

```
/plugin install iwtl --marketplace thai-nm/iwtl
```

Or in two steps, which also work in your shell with `claude plugin ...`:

```
/plugin marketplace add thai-nm/iwtl
/plugin install iwtl@iwtl
```

To try it without installing, clone the repo and run `claude --plugin-dir <path to the clone>`.

## Use

```
/iwtl:iwtl                 review at the default level (medium)
/iwtl:iwtl basic           plain words, walkthrough first, 3-5 findings
/iwtl:iwtl medium          standard terms, 5-7 findings
/iwtl:iwtl advanced        tradeoffs, 7+ findings
/iwtl:iwtl basic src/app.py   level and target together
```

If you give no target, it asks what to review: this session's changes, the latest pull request, or something else.

The skill never loads on its own. You must call it.
