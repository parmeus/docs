

# RESTful API

## Recommendation of Similarities
This API is used for generating similarity recommendations for a specific Digital Soul.

### Structure

The endpoint URL for the API:

```
POST /api/1/recommendation/similarities
```

#### Request Body

Requested body shall have Content-Type of application/json. It could have the following fields

| Field       | Type    | Description                                                  |
| ----------- | ------- | ------------------------------------------------------------ |
| digitalSelf | DigitalSoul | The DigitalSoul which is specified by a concrete address or traits specification |
| options     | HashMap | The options for the recommendation query. It could support subfields like sort, count etc. |
| filter      | HashMap | The filter option to specify inputs for the recommendation engine. |

The `DigitalSoul` type is a HashMap with either an address field or a traits field.

| Field   | Type                    | Description                                                  |
| ------- | ----------------------- | ------------------------------------------------------------ |
| address | String                  | Wallet address which represents a digitalSoul user. |
| traits  | HashMap<String, Number> | A traits specification with trait id as key and score (0 ~ 100) as value, which represents a virtual digitalSoul. |

The `option` field could have the following subfields:

| Field            | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| sort             | String  | How to sort result similarities. It could be "desc" (sort by similarity descend order) or "asc" (sort by similarity ascend order). |
| count            | Integer | How many results are expected.                               |
| similarityMatrix | Boolean | Whether to return similarityMatrix. It is the orthogonal matrix of the requested digitalSoul and result digitalSouls. The matrix represents the similarity of each digitalSoul to others. |

The `filter` field could have the following subfields:

| Field  | Type         | Description                               |
| ------ | ------------ | ----------------------------------------- |
| Traits | List<String> | A list of trait ids that works as a filter. Only those specified traits of digitalSouls will be used during recommendation calculation. |

#### Response Body

The response body is still application/json. It could have the following fields:

| Field            | Type                            | Description                                                  |
| ---------------- | ------------------------------- | ------------------------------------------------------------ |
| result           | List<DigitalSoulRecommendation> | A list of recommend digitalSouls based on similarity.                   |
| similarityMatrix | List<List<Number>>              | The orthogonal matrix about similarity of all digitalSouls (the requested digitalSoul and result digitalSouls). The matrix represents the similarity of each digitalSoul to others. |

The `DigitalSoulRecommendation` is a HashMap with the following fields:

| Field      | Type   | Description                                                  |
| ---------- | ------ | ------------------------------------------------------------ |
| address    | String | Wallet address which represent a digitalSoul user. |
| similarity | Number | A float number from 0 (included) to 1 (included) that represents the similarity of the digitalSoul to the requested digitalSoul. |

### Example

Here is an example of querying similarity recommendation of specific traits combination.

```
{
  "digitalSelf": {
      "address": "0xE473e96F1380d0D3a785492f7337263663548bf6"
  },
  "options": {
      "sort": "desc",
      "count": 3,
      "similarityMatrix": true
  },
  "filter":{
      "traits": [
          "creativity",
          "critical_thinking",
          "inhibitory_control",
          "initiative"
      ]
  }
}
```

It could get the following 3 digitalSouls that are most similar with the requested one. The API will also return the similarityMatrix for those 4 digitalSouls (requested one as first, and along with 3 recommendations).

```
{
    "result": [
        {
            "address": "0x73eAb58D155dd81e530e0F0A3527E7d1b47612d8", 
            "similarity": 0.9977684184341823
        },
        {
            "address": "0xeBeD0BF2701e905b4C576B3dC943D797bAc226ed",
            "similarity": 0.9960226259398527
        },
        {
            "address": "0x8f244389cb752e763b615658e175cfbb5542a8ec",
            "similarity": 0.9947335705758
        }
    ],
    "similarityMatrix": [
        [
            1,
            0.9977684184341823,
            0.9960226259398527,
            0.9947335705758
        ],
        [
            0.9977684184341823,
            1,
            0.9901924197446268,
            0.9935279040880195
        ],
        [
            0.9960226259398527,
            0.9901924197446268,
            1,
            0.9901181504244867
        ],
        [
            0.9947335705758,
            0.9935279040880195,
            0.9901181504244867,
            1
        ]
    ]
}
```

## Get Similarity Matrix of DigitalSouls

This API is used for getting the similarity matrix from a set of DigitalSouls.

### Structure

The endpoint URL for the API:

```
POST /api/1/recommendation/similarityMatrix
```

#### Request Body

Requested body shall have Content-Type of application/json. It could have the following fields

| Field        | Type              | Description                                                  |
| ------------ | ----------------- | ------------------------------------------------------------ |
| digitalSelves | List<DigitalSoul> | The set of digitalSouls for similarity matrix calculation.       |
| options      | HashMap           | The options for the similarity matrix calculation. (It is empty for now) |
| filter       | HashMap           | The filter option to specify inputs for recommendation engine. |

The `DigitalSoul` type is a HashMap with either an address field or a traits field.

| Field   | Type                    | Description                                                  |
| ------- | ----------------------- | ------------------------------------------------------------ |
| address | String                  | Wallet address which represent a digitalSoul user. |
| traits  | HashMap<String, Number> | A traits specification with trait id as key and score (0 ~ 100) as value, which represents a virtual digitalSoul. |

The `filter` field could have the following subfields:

| Field  | Type         | Description                               |
| ------ | ------------ | ----------------------------------------- |
| Traits | List<String> | A list of trait ids that works as filter. Only those specified traits of digitalSouls will be used during recommendation calculation. |

#### Response Body

The response body is still application/json. It could have the following fields:

| Field       | Type               | Description                                                  |
| ----------- | ------------------ | ------------------------------------------------------------ |
| matrixData  | List<List<Number>> | The orthogonal matrix about similarity of all digitalSouls. The matrix represents the similarity of each digitalSoul to others. |
| matrixIndex | List               | A list of digitalSouls' index. It could be String if the digitalSoul is wallet address, and will be corresponding (integeral) index within requested data if the digitalSoul is traits specification. |

### Example

Here is an example of querying similarity matrix of a digitalSoul set consists of a traits combination and 2 concrete addresses.

```
{
    "digitalSelves": [
        {
            "traits": {
                "learning_ability": 76.35,
                "willingness_to_try": 74.75,
                "parmeus_poc_28": 61.400846802234014
            }
        },
        {
            "address": "0xeBeD0BF2701e905b4C576B3dC943D797bAc226ed"
        },
        {
            "address": "0x8f244389cb752e763b615658e175cfbb5542a8ec"
        }
    ],
    "filter": {
        "traits": [
            "baseball_pref",
            "basketball_pref",
            "inhibitory_control",
            "initiative"
        ]
    },
    "options": {
      }
    }
}
```

It could get the following similarity matrix.

```
{
  "matrixData": [
    [
        1,
        0.8913491398569237,
        0.9635199546629128
    ],
    [
        0.8913491398569237,
        1,
        0.9545923261674852
    ],
    [
        0.9635199546629128,
        0.9545923261674852,
        1
    ]
  ],
  "matrixIndex": [
    0,
    "0xeBeD0BF2701e905b4C576B3dC943D797bAc226ed",
    "0x8f244389cb752e763b615658e175cfbb5542a8ec"
  ]
}
```

## Get Parmeus Identity

The API is used to get Parmeus Identification including pid (ParmeusID), and primaryAddress.

### Structure

The endpoint URL for the API:

```
GET /api/1/identity/addresses/:address
```

#### Request Parameter

The following parameters could be used in the request

| Field   | Type   | Description                                           |
| ------- | ------ | ----------------------------------------------------- |
| address | String | The concrete blockchain address of target digitalSoul |
|         |        |                                                       |
|         |        |                                                       |

#### Response Body

The response body is application/json. It could have the following fields:

| Field          | Type   | Description                                         |
| -------------- | ------ | --------------------------------------------------- |
| pid            | String | The ParmeusID of the digitalSoul                    |
| primaryAddress | String | The wallet address that works as primary address of the digitalSoul. |

### Example

Here is an example that request parmeus identity of wallet address

```
GET /api/1/identity/addresses/0xE473e96F1380d0D3a785492f7337263663548bf6
```

The response will be as follows. The primaryAddress is the crypted for privacy consideration.

```
{
  pid: "did:parmeus:f3eb0088a8111cda71ea49b4694b2650",
  primaryAddress: "U2FsdGVkX18s4Kafo9qrOabkBIHj6JZ5M3ci8NHZfxe23uHJAX3IUNQtXMR01qoolIW9/yeLwdWrOg==" // Crypted address
}
```

## Validate Badge of User

The API is used to validate whether a user own some specific badge.

### Structure

The endpoint URL for the API:

```
GET /api/1/identity/addresses/:address/psbts/:type
```

#### Request Parameter

The following parameters could be used in the request

| Field   | Type   | Description                                           |
| ------- | ------ | ----------------------------------------------------- |
| address | String | The wallet address of target digitalSoul |
| type    | String | The badge (Parmeus Soul Bound Token) type to validate |
|         |        |                                                       |

#### Response Body

The response body is application/json. It could have the following fields:

| Field | Type    | Description                                         |
| ----- | ------- | --------------------------------------------------- |
| pid   | String  | The ParmeusID of the digitalSoul                    |
| badge | HashMap | The badge information if the user own such a badge. |

The `badge` field could have the following subfields.

| Field       | Type    | Description                                                |
| ----------- | ------- | ---------------------------------------------------------- |
| type        | String  | The type of the badge.                                     |
| unlocked    | Boolean | If the badge has been unlocked.                            |
| unlockedAt  | String  | The DateTime string when the badge was granted to the digitalSoul |
| unlockedVer | String  | The unlock version of the badge.                           |

### Example

Here is an example that requests the Parmeus identity of concrete address

```
GET /api/1/identity/addresses/0xE473e96F1380d0D3a785492f7337263663548bf6/psbts/badge_1
```

The response will be as follows. It indicate the user own badge_1 type badge which is unlocked at 2022-08-31. The badge has unlockVersion 0.1 and is currently in unlocked status.

```
{
  pid: "did:parmeus:f3eb0088a8111cda71ea49b4694b2650",
  badge: 
    {
      type: "badge_1",
      unlocked: true,
      unlockedAt: "2022-08-31",
      unlockedVer: "0.1"
    }
}
```

## 
