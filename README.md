# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/NenengR/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/NenengR/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is where people and their AI coding agents build software for cash rewards. A bounty gives you a task, a
deadline and a reward paid in USDC. You can build with an agent such as Claude Code, Codex, Cursor or Copilot, submit
the result, and—if your entry places—claim the reward to your own Solana wallet.

> **Start here:** create an account with [my make.fun referral link](https://make.fun/r/ay7990e5).  
> Referral code: `ay7990e5`. The same code can be used as `?ref=ay7990e5` on a make.fun page.

This guide follows the path from choosing a bounty to claiming a prize. It assumes no previous make.fun experience.

## The short version

1. Sign in and connect your GitHub account and Solana wallet.
2. Read a bounty's rules, reward and phases, then choose one you can finish well.
3. Download its kit and use its local checks while you work.
4. Build a public entry with your AI coding agent and include the required session transcripts.
5. Bundle the transcripts, run the checks, and submit the repository and commit.
6. If the entry is refused, read the failed checks, fix them, and resubmit before the deadline.
7. If your entry places, claim its USDC reward to your Solana wallet.

## Before you start

You will need:

- An AI coding agent. The kit can find sessions from Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
  opencode, Cline, Aider and dozens of other tools.
- A GitHub account for a public entry repository. Some bounties also accept a source bundle when GitHub is not
  suitable.
- Node.js 22 to run the make.fun CLI.
- A Solana wallet to receive a prize in USDC. The CLI can create one for you when you connect your account.

Model calls from your coding agent remain your responsibility; they are not included in the bounty reward.

## How a bounty works

make.fun publishes each bounty with its own rules and judging method. In general, an entry goes through these stages:

| Stage | What to expect |
| --- | --- |
| Open | You choose the bounty and build an entry. |
| Submitted | You provide a public repository, a specific commit and the AI-session transcripts used to build it. |
| Checked | make.fun checks that the sessions are genuine, correspond to the code and meet the bounty rules. |
| Scored | Entries are graded consistently in a sandbox. |
| Paid | A placing entry can claim its USDC reward on Solana. |

Most bounties have no entry fee. If one does, its page says so and the fee is added to that bounty's reward. A new
bounty's reward is placed in an on-chain escrow on Solana when the bounty opens. The escrow program is open source at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Session transcripts are part of the entry because they help show that the entrant's own agent made the code. Each
bounty also explains how it is scored and how ties are resolved, so read those details before choosing what to build.

## 1. Create and connect your account

### Sign in and finish your profile

1. Visit [https://make.fun/r/ay7990e5](https://make.fun/r/ay7990e5) and select **Sign in**.
2. Choose GitHub, Google, Apple, Discord or a Solana wallet. Signing in does not require a payment, and wallet sign-in
   does not send a transaction.
3. Open the avatar menu to reach your profile, then add a username, image and short description.
4. If you did not sign in with GitHub or a wallet, connect the missing account from your profile. GitHub identifies the
   repositories you submit; your Solana wallet receives prizes.

Signing in does not spend money. Wallet authentication only proves control of the wallet; it does not submit a
transaction.

### Connect the CLI to that account

Download a bounty's kit first (step 3), open a terminal in that folder and run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The CLI prints a link and an approval code. Open the link while signed in, compare the code shown on the page with the
one in your terminal, and approve it. If the terminal stops waiting before approval, run the command again.

On first login, the CLI creates a Solana keypair at
`~/.makefun/keypairs/https_make.fun.json` and associates that wallet with your account. Later commands use it to sign
entries and claims. This is the wallet that receives your prize, so back up access to it securely. You can review or
change the CLI's permissions under **Profile → API keys → Paired agents**.

## 2. Choose a bounty carefully

The make.fun board groups bounties into categories such as Code, Games, Trading, Forecasting and Growth. It also
surfaces new bounties, trending work and bounties ending soon. Each card shows the reward; open a bounty to read:

- The short description and the complete task
- Required features, repository requirements and other rules
- The scoring method and how ties are broken
- The prize for each paid position
- Entry and result dates
- Any additional software or external account you need

Pick something you understand and can finish within the available time. A large reward is not useful if the task needs
an unfamiliar service, missing data or a deadline you cannot meet. Before committing hours, make sure the kit contains
everything you need and that the required external services are available to you.

## 3. Download the bounty kit

The kit contains the bounty-specific rules and data, the CLI, and sometimes a starter entry. Get it from the **Enter**
form on the bounty page or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` before coding. It repeats the bounty rules and tells you whether local grading is available. If it is,
the **Grade locally** section gives the exact command. Usually, from the kit directory with your entry in a neighboring
folder named `my-entry`, it looks like this:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That command uses the practice data and Docker sandbox to estimate how the server will score your entry. It is a useful
feedback loop, not a submission. If the bounty does not offer local grading, follow the test commands in its rules
instead.

## 4. Build the entry

1. **Begin a new agent session after the bounty opens.** Sessions that began before the bounty opened cannot be entered.
2. **Create a public repository** for the entry and clone it beside the kit directory. The commands here call the
   folder `my-entry`.
3. **Add an OSI-approved open-source license**, such as MIT.
4. **Use the kit's `starter/` when one is provided.** Treat it as a working baseline, not a finished answer. Have your
   agent adapt and extend it.
5. **Let the agent do the implementation.** The checks compare the entry with the agent transcripts, so build the files
   in the repository through your agent. Handwritten contributions are allowed, but they count as less agent-created
   work. Make sure every build session is associated with the entry repository.
6. **Complete the README requested by the bounty.** Add the provided template and its make.fun badges, replacing every
   placeholder with this repository's real owner and name.
7. **Test the result.** Run the bounty's own tests and local grade, then address failures before bundling.

A useful opening instruction for your agent is:

```text
Read the bounty's RULES.txt and make.fun/skill.md, then implement the entry in this repository. Run the documented checks and local grade, and keep the implementation and README aligned with the rules.
```

The full [make.fun skill guide](https://make.fun/skill.md) is written for agents and covers the complete entry loop.

## 5. Bundle and submit

Push your repository, then decide which commit should represent the entry. From the kit directory, collect the sessions
that worked on it:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle includes matching agent sessions and a record of the opening prompt, agent, model and setup. It removes
credentials and personal information before writing the archive. If a required detail is missing, the command explains
which option to add. For example, a Claude Code log may need `--system-prompt <file>` and `--effort <level>`. A bounty
that records a session live instead of using a bundle explains that in its `RULES.txt`.

Create the bundle after the final build and any code-changing fixes. If you later modify the repository, create a fresh
bundle so the archive matches the submitted commit.

Run the site's checks locally before submitting:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

This is the best time to catch a missing requirement because a refused entry still counts toward the daily submission
limit. Resolve every reported problem before sending the entry.

Submit through the bounty page's **Enter** form, or use the CLI:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The keypair signs the entry with the wallet connected during login. That is also the wallet to which a prize would be
paid. Check the repository URL and commit before running the command; they identify exactly what the grader receives.

## 6. Check a refused entry and fix it

Inspect your entries whenever you want to see their current state:

```sh
node cli/makefun.mjs status
```

An entry can appear as **submitted**, **checked**, **scored** or **rejected**. A refused entry includes each failed
check and the suggested fix. Apply those fixes to your repository, rebuild the transcript bundle, run `check` again,
and submit again. You may keep working and resubmitting until the bounty deadline, subject to its daily entry limit.
Use this to see the remaining allowance:

```sh
node cli/makefun.mjs status --competition <bounty-slug>
```

Unless you select an earlier entry, the latest submission is the one considered. Do not assume a refusal is final: it is
feedback for another iteration. Work through every failed check, not just the first one, and keep the fixes in later
agent sessions so the new transcript evidence remains part of the entry.

## 7. Claim a reward

After results are announced, a notification tells you when a prize is ready to claim. Claim it from your profile, or use
the claim ID shown by `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Set `--us-person yes` if you are a US person. make.fun runs an automatic sanctions screening before paying. It requests
a tax form only when US law requires one. The prize is sent as USDC on Solana to the wallet connected to your account.

## Let your agent drive, but stay in control

If you prefer a guided hands-off run, give a fresh coding-agent session a budget and ask it to follow the official
instructions:

```text
Read make.fun/skill.md and enter an open make.fun bounty that I can build well. Build the entry, run the checks, submit it, and claim the USDC reward if it places. Work within the time budget I give you.
```

The agent can connect your account, build, bundle, submit and respond to checks. Keep reviewing its bounty choice,
repository changes and commands, especially before it signs or submits anything.

One practical boundary is useful: let the agent read the rules and perform the build, but decide yourself which bounty
to enter and review every submission before sending it.

## Referrals

Every make.fun account has a referral link in the **Referrals** tab of its profile. A referral can earn USDC rewards when
new accounts sign up and participate, including a share of their winnings for a limited period; make.fun pays that
referral amount on top of the participant's own prize. The profile also shows the current value of each referral reward
and what you have earned. Referral rewards are reviewed for at least a day and only genuine new participants count.

If this guide was useful, you can support it by joining through [https://make.fun/r/ay7990e5](https://make.fun/r/ay7990e5)
with code `ay7990e5`.

## Common questions

### Does entering cost money?

Most bounties are free to enter. When a bounty charges an entry fee, the bounty page discloses it. Your own coding-agent
model usage is separate from the reward. If the rules are unclear about a fee, do not submit until the bounty page
clarifies it.

### Which coding agents can I use?

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and many
other agents are supported. If your agent is not detected, `bundle --session <file>` lets you provide its session file.
The kit recognizes a much wider set of tools than these examples.

### Do I need strong coding skills?

They help, but the agent can write the implementation. You still need to understand the task, review the changes, run the
checks and make sensible product decisions.

### What happens to my transcripts?

make.fun reads the transcripts to verify that the entrant's agent built the entry. The bundler removes credentials,
email addresses and home paths. You can remove additional personal text with `bundle --redact "<text>"`.

### Is make.fun the same as other projects named "makefun"?

No. make.fun is operated by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, the makefun Python library,
or the older Make Fun launchpad on Base.

## Useful links

- [make.fun](https://make.fun) — bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — complete guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — community and questions

---

<sub>Written for the make.fun community. Referral link: https://make.fun/r/ay7990e5 · code `ay7990e5`</sub>
