# Recommendation

Parmeus is a decentralized identity protocol. It enables individuals to connect permissionlessly, autonomously, while keeping ownership of their own data that remains portable and interoperable. Based on the Digital Souls which are created and nurtured by users, Parmeus presents a virtual social graph constructed through the network of  relationship of similarity.

Match and Recommendation (based on similarity) are the basic functions supported by the network.
* Users can easily match with people who are similar to themselves - through purposeful searches, they can connect with people who are similar to themselves, and find solutions that are more suitable for them.
* Applications can suggest connections between users based on their past experience and on-chain behavior.

The following guide shows how to integrate the single match function in node

```
const axios = require('axios');

let address = '0xE473...8bf6'; // target address to match

// try match 20 most similar addresses
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

Social applications could then prompt the user to make connections with those similar addresses; the recommendation system could compare the experiences of the similar addresses, then determine optimal recommendations for the user.
