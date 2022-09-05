

# RESTful API

## Recommendation of Similarities
This API is used for getting some similarities recommendation of specific criteria. The criteria could be an address or specific traits combination.

### Structure

The endpoint URL for the API:

```
POST /api/1/recommendation/similarities
```

#### Request Body

Requested body shall have Content-Type of application/json. It could have the following fields

| Field       | Type    | Description                                                  |
| ----------- | ------- | ------------------------------------------------------------ |
| digitalSelf | HashMap | The digitalSelf which is specified by a concrete address or a traits combination |
| options     | HashMap | The options for the recommendation query. It could support subfields like sort, count et. |
| filter      | HashMap | The filter option for the result of recommendation. It could |

The DigitalSoul type is a HashMap with either an address field or a traits field.

| Field   | Type                    | Description                                                  |
| ------- | ----------------------- | ------------------------------------------------------------ |
| address | String                  | An address of blockchain which represent a digitalSelf user. |
| traits  | HashMap<String, Number> | A HashMap with trait id as key and score (0 ~ 100) as value, which represents a virtual digitalSelf with the traits combination. |

The `option` field could have the following subfields:

| Field            | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| sort             | String  | How to sort result similarities. It could be "desc" (sort by similarity descend order) or "asc" (sort by similarity ascend order) |
| count            | Integer | How many results are expected.                               |
| similarityMatrix | Boolean | Whether return similarityMatrix. It is the orthogonal matrix of the requested digitalSoul and result digitalSouls. The matrix represents the similarity of each digitalSoul to others. |

The filter field could have the following subfields:

| Field  | Type         | Description                               |
| ------ | ------------ | ----------------------------------------- |
| Traits | List<String> | a list of trait ids that works as filter. |

#### Response Body

The response body is still application/json. It could have the following fields:

| Field            | Type                            | Description                                                  |
| ---------------- | ------------------------------- | ------------------------------------------------------------ |
| result           | List<DigitalSelfRecommendation> | An list of recommend similar digitalSelfs.                   |
| similarityMatrix | List<List<Number>>              | The orthogonal matrix about similarity of all digitalSouls (the requested digitalSoul and result digitalSouls). The matrix represents the similarity of each digitalSoul to others. |

The DigitalSelfRecommendation is a HashMap with the following fields:

| Field      | Type   | Description                                                  |
| ---------- | ------ | ------------------------------------------------------------ |
| address    | String | An address of blockchain which represent a digitalSelf user. |
| similarity | Number | An float number from 0 (included) to1 (included) that represents the similarity of the digitalSelf to the requested digitalSelf. |

### Example

Here is an example of querying similarity recommendation of specific traits combination.

```
{
  "digitalSelf": {
      "address": "0x8e...b5bc",
  },
  "options": {
      "sort": "desc",
      "count": 3,
      "similarityMatrix": true
      }
  },
  "filter":{
      "traits": [
          "creativity",
          "critical_thinking",
          ...
          "inhibitory_control",
          "initiative"
      ]
  }
}
```

It could get the following 3 digitalSelfs that are most similar with requested digitalSelf

```
{
    "result": [
        {
            "address": "0xbab2...accd",
            "similarity": 0.9977684184341823
        },
        {
            "address": "0xb08f...0863",
            "similarity": 0.9960226259398527
        },
        {
            "address": "0x562...f645",
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

This API is used for getting the similarity matrix about a set of DigitalSouls.

### Structure

The endpoint URL for the API:

```
POST /api/1/recommendation/similarityMatrix
```

#### Request Body

Requested body shall have Content-Type of application/json. It could have the following fields

| Field        | Type              | Description                                                  |
| ------------ | ----------------- | ------------------------------------------------------------ |
| digitalSouls | List<DigitalSoul> | The digitalSoul set for similarity matrix calculation.       |
| options      | HashMap           | The options for the similarityMatrix calculation. (It is empty for now) |
| filter       | HashMap           | The filter option for the result of recommendation. It could |

For definition of DigitalSoul, please refer to above sections.

#### Response Body

The response body is still application/json. It could have the following fields:

| Field       | Type               | Description                                                  |
| ----------- | ------------------ | ------------------------------------------------------------ |
| matrixData  | List<List<Number>> | The similarity matrix (List<Number>) of each DigitalSoul to all DigitalSouls. The matrix represents the similarity in each traits of corresponding result to requested digitalSelf |
| matrixIndex | List               | An list of index of each DigitalSoul. It could be String if the DigitalSoul is an address, and will be Integer if the DigitalSoul is a traits combination. |

### Example

Here is an example of querying similarity matrix of a digitalSoul set consists of a traits combination and 2 concrete addresses.

```
{
    "digitalSelves": [
        {
            "traits": {
                "learning_ability": 76.35,
                ...
                "willingness_to_try": 74.75,
                "parmeus_poc_28": 61.400846802234014
            }
        },
        {
            "address": "0xbeac...99412"
        },
        {
            "address": "0xc8e2...d415"
        }
    ],
    "filter": {
        "traits": [
            "baseball_pref",
            "basketball_pref",
            ...
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
    "0xbeac...99412",
    "0xc8e2...d415"
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
| primaryAddress | String | The primary block chain address of the digitalSoul. |

### Example

Here is an example that request parmeus identity of concrete address

```
GET /api/1/identity/addresses/0xbab2...accd
```

The response will be as follows. The primaryAddress is the same as requested address which implies it is just the primaryAddress of the digitalSoul.

```
{
  pid: "xxx",
  primaryAddress: "xxx" // Crypted address
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
| address | String | The concrete blockchain address of target digitalSoul |
| type    | String | The badge (Parmeus Soul Bound Token) type to validate |
|         |        |                                                       |

#### Response Body

The response body is application/json. It could have the following fields:

| Field | Type    | Description                                         |
| ----- | ------- | --------------------------------------------------- |
| pid   | String  | The ParmeusID of the digitalSoul                    |
| badge | HashMap | The badge information if the user own such a badge. |

The badge field could have the following subfields.

| Field       | Type    | Description                                                |
| ----------- | ------- | ---------------------------------------------------------- |
| type        | String  | The type of the badge.                                     |
| unlocked    | Boolean | If the badge has been unlocked.                            |
| unlockedAt  | String  | The DateTime string when the badge was granted to the user |
| unlockedVer | String  | The unlock version of the badge.                           |

### Example

Here is an example that request parmeus identity of concrete address

```
GET /api/1/identity/addresses/0xbab2...accd
```

The response will be as follows. The primaryAddress is the same as requested address which implies it is just the primaryAddress of the digitalSoul.

```
{
  pid: "xxx",
  primaryAddress: "xxx" // Crypted address
}
```

## 