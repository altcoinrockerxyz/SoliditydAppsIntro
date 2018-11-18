# SoliditydAppsIntro

These are my notes and codes on the Intro and Advanced course that I took related to Solidity with lectures on Truffle Framework and Ganache. This includes a Pet Shop dApp creation and deployment using Heroku and Infura via Rinkeby.

**Section 2: Introduction to Solidity**

**Lecture 6: Contracts, Constructors and Functions**

1.  Structure of a Solidity source file:

- Top most contains pragma (lowest version of sol supported by the contract)
- contract codes (where variables, mappings, constructors, functions, and modifiers are declared)
- We can call some other contracts within other contracts

i.e.

contract OwnedToken{ // <-- contract declaration
TokenCreator creator;
address owner; // Variable Declaration
bytes32 name; // Variable Declaration
constructor(bytes32 \_name) public { // <-- Constructor start
owner = msg.sender;
creator = TokenCreator(msg.sender);
name = \_name;
} // <-- Constructor end
}

contract TokenCreator {....}

- In the above example, the TokenCreator contract was called within the OwnedToken contract.\_

2.  Structure of a Function

function functionName (<parameter types>)
{public | [private | etc]} [pure|view|payable][returns (<return types>)] {
<function codes>
}

- Modifiers:
  Function Visibility Declarations (public | private | etc)
  Return Types - The type of variable to return
  State Mutability (pure | view | payable)

3.  Functions and Variables Visibility

- Default visibility for Functions: Public (can be called internally or externally)
- Default visibility for State Variables: Internal (can only be access internally; from within the current or contract or contracts deriving from it)
- External keyword is only applicable to functions, and these can be called from _other contracts_ and via _transactions_. Internal calls need this(dot).
- _State variables can't be external_
- Private functions can only be accessed or called inside the contract they are defined in.
- Public and External functions perform the same but functions declared as External rather than Public uses less gas and more efficient when they receive large amounts of data.
- Calling a function (declared as External) from within another function inside the same contract will throw an error if there is no (this-dot) before the name of the function.

4.  Contract Inheritance

- This means functions within C could be accessed and used by E

i.e.

contract C {
...
}

contract D {
...
}

contract E is C {
...
}

5.  State Mutability of Functions

- A View function promises _not to modify the state_
- Pure functions are derivatives of View functions but it also promises _not to read from_ state along with _not modify state_
- Payable functions can receive ether and can make operations with those ethers.

_THINGS NOT ALLOWED IN VIEW FUNCTIONS:_
a. Writing to state variables
b. Emitting events
c. Creating other contracts
d. Using selfdestruct
e. Sending Ether via calls
f. Calling any function not marked VIEW or PURE
g. Using low-level calls
h. Using inline assembly that contains certain opcodes

_ADDITIONAL THINGS NOT ALLOWED IN PURE FUNCTIONS:_
a. Reading from state variables
b. Accessing _this.balance_ or _<address>.balance_
c. Accessing any of the members of _block_, _tx_, _msg_ (with the exception of _msg.sig_ and _msg.data_)
d. Calling any function not marked _pure_
e. Using inline assembly that contains certain opcodes

_PAYABLE FUNCTION_

Requires the _payable_ keyword
