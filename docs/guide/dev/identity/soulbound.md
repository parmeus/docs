# Soulbound

Soulbound tokens (SBTs) are non-transferable non-fungible tokens (NFTs) that are linked to a digital wallet or identity. They can be used to represent achievements, certifications, awards, credentials or markers of identity. They can also be used to represent individual characteristics or traits based on digital behavior, preferences or other unique attributes. Users can earn and collect SBTs to create their own unique digital identity.

In the Parmeus ecosystem, a person could have only one Parmeus ID which represents the user's Digital Soul. Everything a user does to train a Digital Soul will form their soulbound identity across web3.
 
Users can, however, bind multiple wallet addresses to this unique Parmeus ID, and these bound wallet addresses seamlessly inherit all the properties of the Digital Soul. This makes it easy to share the Digital Soul among all addresses of the user. It also enables users to use on-chain data from multiple wallets to enrich their Digital Soul.

Third party projects may want to restrict users to registering a single account, or want to identify and serve the user with the same account, no matter what wallet address is used. This may have been difficult to implement using only wallet addresses, but could be easily supported by Parmeus soulbound functions.

The following example shows how to identify a user through a wallet address.

```
const axios = require('axios');

let address = '0xE473...8bf6'; // target address to validate

// make the query
let response = await axios.get(`/api/1/identity/addresses/${address}`);

// check humanity of the user
let parmeusId = response.data.pid;
```

The project could then use the parmeusId (instead of using the wallet address directly) as an index to find the account of the wallet address.
