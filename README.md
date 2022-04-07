# Axelar contest details
- $47,500 USDC main award pot
- $2,500 USDC gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code4rena.com/contests/2022-04-axelar-network-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts April 7, 2022 00:00 UTC
- Ends April 11, 2022 23:59 UTC

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

A detailed design can be found here (will be posted soon): https://docs.axelar.dev/roles/dev/design

# Smart Contracts

The following contracts are in-scope for the audit.
The remaining code in the repo is only relevant for tests, utils, samples etc., and not in scope.

Note: Known issues posted on GitHub aren't considered valid findings: https://github.com/axelarnetwork/axelar-cgp-solidity/issues

### Interfaces

#### IAxelarGateway.sol (122 sloc)

#### IAxelarGatewayMultisig.sol (17 sloc)

#### IERC20.sol (15 sloc)

#### IERC20BurnFrom.sol (4 sloc)

#### IAxelarExecutable.sol (56 sloc)

### Contracts

#### AxelarGatewayProxy.sol (34 sloc)

Our gateway contracts implement the proxy pattern and allow upgrades.
Calls are delegated to the implementation contract below.

#### AxelarGateway.sol (477 sloc)

#### AxelarGatewayMultisig.sol (393 sloc)

The implementation contract that accepts commands signed by Axelar network's validators (see `execute`).
Different commands require different sets of validators to sign (operators vs owners).
Operators correspond to a subset of Axelar validators, whereas owners are chosen by stake and represent a larger set.

#### AdminMultisigBase.sol (134 sloc)

#### ERC20.sol (86 sloc)

#### ERC20Permit.sol (45 sloc)

#### MintableCappedERC20.sol (25 sloc)

#### BurnableMintableCappedERC20.sol (47 sloc)

#### TokenDeployer.sol (13 sloc)

#### DepositHandler.sol (22 sloc)

#### Context.sol (10 sloc)

#### Ownable.sol (18 sloc)

#### EternalStorage.sol (63 sloc)

#### ECDSA.sol (24 sloc)

# Areas to focus

We'd like wardens to particularly focus on the following:

1. General message passing: `sendToken`, `contractCallWithToken`, and `contractCall`.
2. Mints/burns for token transfers.
3. Authentication of commands: `execute` in `AxelarGatewayMultisig.sol`.
4. Transfer of owners/operators.

# Build

```bash
npm ci

npm run build

# Might need
# npm install mocha

npm run test  # Test with mocha
```

# References

Contracts repo: https://github.com/axelarnetwork/axelar-cgp-solidity

Detailed Nework Design: https://docs.axelar.dev/roles/dev/design

Network resources: https://docs.axelar.dev/resources

General Message Passing Usage: https://docs.axelar.dev/roles/dev/gmp

Example token transfer flow: https://docs.axelar.dev/roles/dev/cli/axl-to-evm

Deployed contracts: https://docs.axelar.dev/releases/mainnet
