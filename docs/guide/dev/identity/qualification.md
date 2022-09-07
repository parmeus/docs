# Qualification
 
As important assets of digitalSoul, Parmeus supports rich kind of PSBTs. Some of them are proof of achievement, some are proof of attendence, and there are parmeus featured proof of personality, abilities, soft skills. Benefits from the non transferrable nature of SoulBoundToken, PSBT works perfectly for Qualification validation.

A DAO may validate qualification of applicants at entrance. For example, A photographic DAO may require some achievement in photograhic, and some qualifications such as good-teamworker, eager-to-share as requirements. DAO could also use the qualification for organization optimization, and candidates selecting.

The following example shows how to integrate PSBT validation functions in node

```
const axios = require('axios');

const psbtType = 'eager-to-share'; // the psbt type for Eager-To-Share
let address = '0xE473...8bf6'; // target address to validate

// make the query
let response = await axios.get(`/api/1/identity/addresses/${address}/psbts/${psbtType}`);

// check if the user owns the badge
let isCertificated = response.data.badge && response.data.badge.unlocked;
```

Then the user could use the `isCertificated` for application.