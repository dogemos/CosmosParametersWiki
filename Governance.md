# The `Governance` Module
The `Governance` module is responsible for on-chain proposals and voting functionality. `Governance` is active on Cosmos Hub 3 and currently has three parameters with six subkeys that may be modified by governance proposal:
1. [`depositparams`](#1-depositparams)
   - [`min_deposit`](#min_deposit) - `512000000uatom`
   - [`max_deposit_period`](#max_deposit_period) - `1209600000000000`

2. [`votingparams`](#2-votingparams)
   - [`voting_period`](#voting_period) - `1209600000000000`

3. [`tallyparams`](#3-tallyparams)
   - [`quorum`](#quorum) - `0.400000000000000000`
   - [`threshold`](#threshold) - `0.500000000000000000`
   - [`veto`](#veto) - `0.334000000000000000`

The launch values for each parameter's subkeys are outlined above, but you can [verify them yourself](#verify-parameter-values). 

If you're technically-inclined, [these are the technical specifications](#technical-specifications).

## 1. `depositparams`
### Token transfer functionality.
#### `cosmoshub-3` default: `true`

The Cosmos Hub (cosmoshub-1) launched without transfer functionality enabled. Users were able to stake and earn rewards, but were unable to transfer ATOMs between accounts until the cosmoshub-2 chain launched. Transfer functionality may be disabled and enabled via governance proposal.

### Potential implications
#### Enabling `depositparams`
Setting the `sendenabled` parameter to `true` will enable ATOMs to be transferred between accounts. This capability was first enabled when the cosmoshub-2 chain launched.

#### Disabling `depositparams`
Setting the `sendenabled` parameter to `false` will prevent ATOMs from being transferred between accounts. ATOMs may still be staked and earn rewards. This is how the cosmoshub-1 chain launched.

# Verify Parameter Values
## Genesis (aka launch) Parameters
This is useful if you don't have `gaiacli` installed and don't have a reason to believe that the parameter has changed since the chain launched.

Each parameter may be verified in the chain's genesis file, [found here](https://raw.githubusercontent.com/cosmos/launch/master/genesis.json). These are the parameters that the latest Cosmos Hub chain launched with, and will remain so, unless a governance proposal changes them. I've outlined those original values in the [Technical Specifications section](#technical-specifications).

The genesis file is text-based and large. The genesis parameter naming scheme isn't identical to those listed above, so when I search, I put one underscore between upper and lowercase characters, then convert all characters to lowercase.

For example, if I want to search for `depositparams`, I'll search the [genesis file](https://raw.githubusercontent.com/cosmos/launch/master/genesis.json) for `deposit_params`.

## Current Parameters
You may verify the current parameter values (in case they were modified via governance proposal post-launch) with the [gaiacli command-line application](/gaiacli). Here are the commands for each:
1. `depositparams` - `gaiacli q ..` --> **to do** <--

# Technical Specifications

The `Governance` module is responsible for 

The `Governance` module contains the following parameters:

| Key           | Type   | cosmoshub-3 genesis setting                                                                     |
|---------------|--------|----------------------------------------------------------------------------------------------------|
| depositparams | object | {"min_deposit":[{"denom":"uatom","amount":"10000000"}],"max_deposit_period":"172800000000000"}     |
| votingparams  | object | {"voting_period":"172800000000000"}                                                                |
| tallyparams   | object | {"quorum":"0.334000000000000000","threshold":"0.500000000000000000","veto":"0.334000000000000000"} |

## SubKeys

| Key                | Type             | cosmoshub-3 genesis setting             |
|--------------------|------------------|-----------------------------------------|
| min_deposit        | array (coins)    | [{"denom":"uatom","amount":"10000000"}] |
| max_deposit_period | string (time ns) | "172800000000000"                       |
| voting_period      | string (time ns) | "172800000000000"                       |
| quorum             | string (dec)     | "0.334000000000000000"                  |
| threshold          | string (dec)     | "0.500000000000000000"                  |
| veto               | string (dec)     | "0.334000000000000000"                  |

__NOTE__: The governance module contains parameters that are objects unlike other
modules. If only a subset of parameters are desired to be changed, only they need
to be included and not the entire parameter object structure. 