## Caching the length in for loops
Consider a generic example of an array arr and the following loop:

for (uint i = 0; i < arr.length; i++) {
    // do something that doesn't change arr.length
}
In the above case, the solidity compiler will always read the length of the array during each iteration. That is,

if it is a storage array, this is an extra sload operation (100 additional extra gas (EIP-2929) for each iteration except for the first),
if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first),
if it is a calldata array, this is an extra calldataload operation (3 additional gas for each iteration except for the first)
This extra costs can be avoided by caching the array length (in stack):

uint length = arr.length;
for (uint i = 0; i < length; i++) {
    // do something that doesn't change arr.length
}
In the above example, the sload or mload or calldataload operation is only called once and subsequently replaced by a cheap dupN instruction. Even though mload, calldataload and dupN have the same gas cost, mload and calldataload needs an additional dupN to put the offset in the stack, i.e., an extra 3 gas.

This optimization is especially important if it is a storage array or if it is a lengthy for loop.

Note that the Yul based optimizer (not enabled by default; only relevant if you are using --experimental-via-ir or the equivalent in standard JSON) can sometimes do this caching automatically. However, this is likely not the case in your project. Reference. Also see this.
