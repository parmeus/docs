# Soulbound

Soulbound is a philosophy that Parmeus has implemented from start to finish. In Parmeus ecosystem, a person could have only one Parmeus ID which represents user's digital soul. All the abilities of the user to train a digital soul will represent the user's soulbound identity to travel in the world of web 3. 

On the other hand, users could bind multiple wallet addresses to this unique Parmeus ID, and these bound wallet addresses seamlessly possess the special ability of the digital soul. This makes it easy to share / identify the digital soul among all addresses of the user.

Third party projects may restrict user could only register 1 account, or want to identity and serve the user with the same account, no matter what wallet address used. This may be hard to implement before, but could be easily supported by Parmeus soulbound functions.

The following example shows how to identify a user through a wallet address.

```
const axios = require('axios');

let address = '0xE473...8bf6'; // target address to validate

// make the query
let response = await axios.get(`/api/1/identity/addresses/${address}`);

// check humanity of the user
let parmeusId = response.data.pid;
```

Then project could then use the parmeusId (instead of using the wallet address directly) as index to found account of the wallet address.