# smartContractWallet
A smart contract wallet where:

- One owner may spend as they wish
- Five guardians who can change the address owner
- Each guardian can also spend up to an unathorised limit agreed upon by the other guardians


Code summary:
VARIABLES

- Owner - The wallet owner

- Guardians have the following structure:
    - An address
    - A limit to which they can spend (default is set too 1ETH but they are able to increase this with the approval of 3 / 4 of the other guardians).
    - An elected owner for the wallet
    - The guardians are mapped based on a uint 0 - 4
  
 - Limit request - responsible for increases for approved spending of the guardian
    . The submitting address
    . Requested increase
    . Votes For and Against (approved at 3 For, declined at more than 1)
    . A uint alreadyVotedCounter - number of guardians who have voted on this request
    . Mapping of this uint to the addresses (Will prevent double voting)
    . Status of request (2 for pending, 1 for declined and 0 for approved)
