# Humanity

Parmeus provides the ability to grand user with soulbound badges during the process of playing, training, growing and unlocking achievements. Users could mint these badges as PSBT (short for Parmeus Soulbound Token) according to their own wishes. These PSBTs will serve as future passes to third-party projects.

`Humanity` is such a useful PSBT. Parmeus could identify whether the user is `Humanity` through user's recent decentralized behavior in the Parmeus ecosystem. Using the PSBT could help 3rd party projects and airdrop to reach real users more effectively.

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

Then the isHumanity variable could be used by application to determine if the user could get some access right.