# Qualification
 
Parmeus supports a rich assortment of PSBTs as an important component of the Digital Soul. PSBTs include proof of achievement, proof of attendance, or Parmeus Soulbound tokens that represent characteristics including personality, abilities, and soft skills. Benefiting from the non-transferrable nature of Soulbound tokens, PSBTs work perfectly for qualification validation.

A DAO may validate the qualifications of applicants upon entrance. For example, a photography DAO may require some achievement in photography, and qualities such as working well in a team could easily be included as requirements. DAOs could also use the qualifications for organization optimization and candidate selection.

College or university courses could set attendance requirements, with a minimum number of attendance PSBTs collected over a period of time. A professional or industry association DAO could require a minimum threshold of industry engagement or professional development activities: tracked by PSBTs that represent engagement at industry events, skills development, or community participation.


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
