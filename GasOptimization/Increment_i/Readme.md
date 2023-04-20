## The increment in for loop post condition can be made unchecked
(This is only relevant if you are using the default solidity checked arithmetic.)

Consider the following generic for loop:

for (uint i = 0; i < length; i++) {
    // do something that doesn't change the value of i
}
In this example, the for loop post condition, i.e., i++ involves checked arithmetic, which is not required. This is because the value of i is always strictly less than length <= 2**256 - 1. Therefore, the theoretical maximum value of i to enter the for-loop body is 2**256 - 2. This means that the i++ in the for loop can never overflow. Regardless, the overflow checks are performed by the compiler.

Unfortunately, the Solidity optimizer is not smart enough to detect this and remove the checks. One can manually do this by:

for (uint i = 0; i < length; i = unchecked_inc(i)) {
    // do something that doesn't change the value of i
}

function unchecked_inc(uint i) returns (uint) {
    unchecked {
        return i + 1;
    }
}
Note that it’s important that the call to unchecked_inc is inlined. This is only possible for solidity versions starting from 0.8.2.

Gas savings: roughly speaking this can save 30-40 gas per loop iteration. For lengthy loops, this can be significant!
