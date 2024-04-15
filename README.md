# cairo-checklist

Checklist for Cairo contract that can be used during Cairo smart contract security reviews or audits. 

## List

1. Integer division.

    30 / 9 = 1206167596222043737899107594365023368541035738443865566657697352045290673497 because 120...97 * 9 = 30

2. Arithmetic overflow.

    Valid values for [Felt](TODO:add link) is (-P/2,P/2) where P is prime used by Cairo, which is 252 bit number. Felts are unchecked to overflow and underflow. Multiplying of two negatives can lead to positive result.

3. State modifications in a view function.

    Compiler does not restrict modifications in @view functions. 

4. Incorrect Felt Comparison.

5. Access controls & account abstraction.

    There are no EOA addresses in StarkNet, only contract addresses. But it is still possible to interact with contracts directly. But from the perspective of the contract, the caller's address will be 0. Since 0 is also the default value for uninitialized storage, it's possible to accidentally construct access control checks that fail open instead of properly restricting access to only the intended users.

6. L1 to L2 Address Conversion.
    In Starknet, addresses are of type felt while on L1 addresses are of type uint160. Thus, in order to pass around address types during cross layer messaging, the address variable is typically given as a uint256. However, this can create an issue where an address on L1 can map to the zero address (or an unexpected address) on L2.



## Tools for Cairo security 

### [Caracal](https://github.com/crytic/caracal)

Caracal is a static analyzer tool over the SIERRA representation for Starknet smart contracts.

It has 14 detectors(2 High, 7 Medium, and 5 Low Impact) that can be used for both Cairo 1 & 2 contracts.

### [Amarna](https://github.com/crytic/amarna)

Amarna is a static-analyzer and linter for the Cairo programming language.

It has 14 Rules that can be used for linting Cairo contracts.

## Sources

1. [Cairo Contracts overview by MixBytes](https://mixbytes.io/blog/cairo-contracts-overview#rec509005895)