# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos: 
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted. 

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Contest setup

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [ ] Name of each contract and:
  - [ ] source lines of code (excluding blank lines and comments) in each
  - [ ] external contracts called in each
  - [ ] libraries used in each
- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [ ] Identify any areas of specific concern in reviewing the code
- [ ] Add all of the code to this repo that you want reviewed
- [ ] Create a PR to this repo with the above changes.

---

# Axelar contest details
- $47,500 USDC main award pot
- $2,500 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-04-axelar-network-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts April 7, 2022 00:00 UTC
- Ends April 11, 2022 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

# Contest Scope

The contest will focus on Axelar's gateway smart contracts that are deployed on EVM chains
that process messages generated from the Axelar network (such as minting a certain token),
and accept messages/token deposits from users/applications.

# Protocol overview

Axelar is a decentralized interoperability network connecting all blockchains, assets and apps through a universal set of protocols and APIs.
It is built on top off the Cosmos SDK. Users/Applications can use Axelar network to send tokens between any Cosmos and EVM chains. They can also
send arbitrary messages between EVM chains.

Axelar network's decentralized validators confirm events emitted on EVM chains (such as deposit confirmation and message send),
and sign off on commands submitted (by automated services) to the gateway smart contracts (such as minting token, and approving message on the destination).

A detailed design can be found here: https://docs.axelar.dev/roles/dev/design

# Areas to focus

We'd like wardens to particularly focus on the following:

1. General message passing: `sendToken`, `contractCallWithToken`, and `contractCall`.
2. Mints/burns for token transfers.
3. Authentication of commands: `execute` in `AxelarGatewayMultisig.sol`.

Note: `AxelarGatewaySinglesig.sol` can be ignored as it's the same as `AxelarGatewayMultisig.sol` but designed to work with a single signature (when using threshold signature schemes).

# References

Contracts repo: https://github.com/axelarnetwork/axelar-cgp-solidity

Detailed Nework Design: https://docs.axelar.dev/roles/dev/design

Network resources: https://docs.axelar.dev/resources

General Message Passing Usage: https://docs.axelar.dev/roles/dev/gmp

Example token transfer flow: https://docs.axelar.dev/roles/dev/cli/axl-to-evm

Deployed contracts: https://docs.axelar.dev/releases/mainnet
