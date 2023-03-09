# smartContractWallet
A smart contract wallet where:

- One owner may spend as they wish
- Five guardians who can change the address owner
- Each guardian can also spend up to an unathorised limit agreed upon by the other guardians


Please comment feedback and potential bugs or security issues! Love to learn :).


VARIABLES

- Owner - The wallet owner

- Guardians have the following structure:
    - An address
    - A limit to which they can spend (default is set too 1ETH but they are able to increase this with the approval of 3 / 4 of the other guardians).
    - An elected owner for the wallet
    - The guardians are mapped based on a uint 0 - 4
  
 - Limit request - responsible for increases for approved spending of the guardian
    - The submitting address
    - Requested increase
    - Votes For and Against (approved at 3 For, declined at more than 1)
    - A uint alreadyVotedCounter - number of guardians who have voted on this request
    - Mapping of this uint to the addresses (Will prevent double voting)
    - Status of request (2 for pending, 1 for declined and 0 for approved)

function deposit
- Simply increments the contracts recorded balance by msg.value

function setOwner
- Verifies msg.sender is a guardian
- Sets the new prefered owning address
- Checks for a majority - if now 3 / 5 guardians have the _newAddress as their owner it will change the contract ownership

function Withdrawal
- Allows the owner to withdraw an amount up until the contract balance
- Allows guardians to withdraw an amount approved by other guardians

function requestIncreaseSpendingLimit
- Two checks are placed before any changes are made (this was a bug in previous version
- Stores current request number in a temporary variable and then increments the request counter. This prevents malicious attackers from attempting to overwrite the attributes of a limit request by calling the function again
- Sets status of request to 2 for PENDING

function voteOnRequests
- Confirms the address hasn't already been actioned, the caller hasn't already voted, the caller is a guardian
- Records guardian as a voter and places vote on request
- Checks to see if minimum vote requirements have been met and alters status of request

function cancelRequest
- Allows submitter to withdraw / self decline a request if it has not already been actioned

function verifyGuardian
- Assisting function to the contract, returns guardianNumber (uint reference to guardian in mapping(uint => guardian) or raises an exception if msg.sender is not a guardian

functions receive and fallback:
- Call the deposit function
