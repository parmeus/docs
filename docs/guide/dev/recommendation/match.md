# Match

Parmeus is a decentralized identity protocol. It enables individuals to be truly permissionless, autonomous, and portable. Based on the Digital Souls which created and nurtured by users, Parmeus presents a virtual social graph constructed through the invisible relationship of similarity.

Match (based on similarity) is the basic functions supported by the network. 
* Users can easily match people who are similar to themselves; through purposeful searches, they can consult solutions to people who are similar to themselves, and find solutions that are more suitable for them.
* Applications can easily match similar people of specific user. Then application can then make recommendation according to similar people's experience.

The following guide shows how to integrate the single match function in node

```
const axios = require('axios');

let address = '0xE473...8bf6'; // target address to match

// try match 20 most similar addressesg
let response = await axios.get(`/api/1/recommendation/similarities`, {
  "digitalSelf": {
      "address": address,
  },
  "options": {
      "sort": "desc",
      "count": 20,
      "similarityMatrix": true
      }
  },
  "filter":{
      "traits": [
          "creativity",
          "critical_thinking",
          "inhibitory_control",
          "initiative"
      ]
  }
});

// Then we extract similar addresses of the target
let similarAddresses = response.data.result.map(i=>i.address);
```

Then social applications could prompt the user for connections to those similar addresses; recommend system could get experience of the similar Addresses, and figure out some recommendations for the user.