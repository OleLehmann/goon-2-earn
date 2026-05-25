<img width="1270" height="754" alt="Screenshot 2026-05-25 at 2 09 03 PM" src="https://github.com/user-attachments/assets/bc90632f-5bea-4413-bf93-a186c6bf6a52" />


**Automate rewarding contributors with a slice of ownership over a project and its earnings, when pull requests are merged. Welcome to Goon 2 Earn.**

## Install

1. [Install Goon 2 Earn](https://github.com/OleLehmann/goon-2-earn/installations/new/) Github app on one or more repositories  
2. Initialize the app for each repo on [g2e.slice.so](https://g2e.slice.so) by following the [setup process](#setup-process)

### Setup process

Goon 2 Earn (G2E) relies on:

- A [Slicer](https://slice.so), to split the project's ownership and earnings among multiple contributors;
- A [Gnosis Safe](https://gnosis-safe.io/app), typically owned by the project's maintainers, to execute rewards distributions.

The setup process is carried out on [g2e.slice.so](https://g2e.slice.so) by someone who is both owner of the repo and the safe related to the project. It consists in:

1. Delegating G2E to propose transactions on the appointed safe;
2. Creating a slicer to represent the project.

## How it works

When a pull request is opened:

- A comment is automatically posted with instructions on how to request a slice reward;
- The G2E bot keeps updating the scheduled slice distribution in the PR discussion, as new requests are made;
- The PR owner can edit the scheduled distribution anytime, for example as new commits are made or after discussing with the reviewer.

When a PR is merged:

- G2E proposes on the project's Gnosis Safe a transaction to mint the agreed amount of slices;
- Once maintainers sign and submit the transaction, the contributors receive the reward. As a result they will receive a proportional share of earnings related to the project's Slicer from that moment onward, directly on [slice.so](https://slice.so).

> See it in action on this [Demo PR](https://github.com/slice-so/merge-to-earn/pull/4)

<details>
<summary>G2E first comment and instructions (click to expand)</summary>
<img src='/public/main.png'/>
</details>

<details>
<summary>Example scenario (click to expand)</summary>

- A project starts with 1000 slices to each of its 5 creators, for their initial work. The creators share equal ownership over the project's slicer, and those who act as maintainers are also owners of the Gnosis Safe which approves new slice distributions.

  > Any payment sent to the slicer at this stage will be split equally between creators (20% each).

- A new contributor opens a PR and asks for 500 slices for its work. Once the PR is merged and the transaction is submitted on the safe, slices are minted to its wallet.  
  > Any payment sent to the slicer at this stage will be split: ~9% to the contributor, ~18% to each project creator

As a result, **contributors are rewarded proportionally to their work and receive earnings based on when their PRs were merged.**

Everything is handled transparently on-chain, while Github settings and permissions can be used to customize what happens between opening and merging a PR.

</details>

## Notes

- Each PR has a pinned G2E comment showing the scheduled slice distribution.
- Contributors can manage their slices and withdraw any earnings on [slice.so](https://slice.so). Slices are ERC1155 tokens so they can also be managed on the owner's ETH wallet and can be freely transferred (learn more on [slice.so](https://slice.so)).
- If a PR is merged while previous mint proposals haven’t been executed, **a new transaction will be proposed which includes all pending queued mints under the same nonce**. It is thus possible to combine multiple proposals in a single transaction by executing the latest transaction proposed by G2E on a safe for each nonce.
- When a slicer is created on [g2e.slice.so](https://g2e.slice.so), the appointed Gnosis Safe becomes its controller and is able to **mint or burn new slices** or sell products on the slicer's decentralized store.
- The max total number of slices that can be created for a project is 4B. See below the suggestion on [how to quantify slices as reward](#how-many-slices-to-give-when-merging-prs).

## Suggestions for maintainers

<details>
<summary>Define in advance how slice rewards are calculated</summary>

- We suggest rewarding 1 slice for 1$ value of work, or something like that. This greatly facilitates estimating how many slices to give to initial and future contributors.

</details>

<details>
<summary>Add reward tags to issues and PRs</summary>

- To incentivise and prioritise contributions, you can add tags to issues and PRs to signal the potential reward for contributors.

</details>

## Gas cost considerations

Goon 2 Earn requires executing transactions on the Ethereum blockchain in the following instances:

- Setting up a project: The setup process involves creating a slicer for a project. Costs around **400k gas**, around $4-8*
- Executing a safe transaction after merging PRs: Gas costs are variable and generally amount to **100k gas per transaction**, around $1-2* (note that multiple PRs can be batched into a single transaction, see notes section)

> *Based on an ETH price of $1000 and a gas price of 10–20 gwei

## Addressing security concerns

Goon 2 Earn projects can be considered safe against attackers attempting to steal earnings by compromising Github accounts or ETH wallets.

In fact, compromising a project is not worth for an attacker as it:

- Requires satisfying hard requirements;
- Yields low rewards;
- Can be easily and quickly mitigated by project owners.

#### Github account compromised

Let's consider the case where an attacker gains access to a maintainer's Github account. In this case, **they would be able to merge fake PRs and propose malicious transactions to the project's multisig** to reward themselves with slices.

However, **nothing would happen until the quorum of multisig owners execute the malicious transaction**. If maintainers are aware an attack has happened, or just check the accuracy of the transactions to be executed (as it's always advised to) this scenario is highly unlikely to happen.

Even if maintainers mistakenly execute a malicious transaction, they still have time to revert the outcome. In this case the attacker only captures a small window of earnings between execution and rollback.

#### Gnosis Safe compromised

A more advanced attack would involve gaining control of enough multisig keys to execute transactions autonomously.

Even then, the attacker cannot retroactively steal past earnings—only future ones after compromise. To mitigate this, project owners can reinitialize G2E with a new slicer and multisig, restoring normal distribution within minutes.

## Learn more

- [Goon 2 Earn - website](https://g2e.slice.so)
- [Slice protocol](https://slice.so)
- [Support (Discord)](https://discord.gg/c7puDHjgMU)

## Contributing

This project uses Goon 2 Earn to reward contributors with a piece of the [Goon 2 Earn slicer](https://slice.so/slicer/23) and its earnings, when pull requests are merged.
