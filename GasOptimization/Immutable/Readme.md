### State variables that can be set to immutable
### Solidity 0.6.5 introduced immutable as a major feature. It allows setting contract-level variables at construction time which gets stored in code rather than storage.

### Consider the following generic example:

> contract C {
    /// The owner is set during contruction time, and never changed afterwards.
    address public owner = msg.sender;
}
### In the above example, each call to the function owner() reads from storage, using a sload. After EIP-2929, this costs 2100 gas cold or 100 gas warm. However, the following snippet is more gas efficient:

> contract C {
    /// The owner is set during contruction time, and never changed afterwards.
    address public immutable owner = msg.sender;
}
### In the above example, each storage read of the owner state variable is replaced by the instruction push32 value, where value is set during contract construction time. Unlike the last example, this costs only 3 gas.
