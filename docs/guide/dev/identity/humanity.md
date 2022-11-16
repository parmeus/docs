# Humanity

Parmeus awards the user with soulbound badges during the process of playing, training, growing and unlocking achievements. Users can mint these badges as Parmeus Soulbound Tokens (PSBTs).

PSBTs could serve as credentials to third-party projects. For example, content creators could use PSBTs to grant access to early content, exclusive events or special airdrops. They can also be used by social groups, clubs or DAOs to grant entry to real-world events. PSBT are non-transferable, so the benefits conferred cannot be transferred, traded or sold between accounts.

Proof of Humanity is an incredibly useful PSBT. Parmeus can assess Humanity through the user's recent behavior in the decentralized Parmeus ecosystem. Using the Humanity PSBT could help 3rd party projects and airdrops to reach real users more effectively, prevent bot activity, and focus on boosting engagement from real people.

The following guide shows how to integrate the validation function in node

```
const axios = require('axios');

const humanityBadgeType = 'humanity'; // the psbt type for Humanity
let address = '0xE473...8bf6'; // target address to validate

// make the query
let response = await axios.get(`/api/1/identity/addresses/${address}/psbts/${humanityBadgeType}`);

// check humanity of the user
let isHumanity = response.data.badge && response.data.badge.unlocked;
```

Then the isHumanity variable could be used by the application to determine if the user could get some access right.
