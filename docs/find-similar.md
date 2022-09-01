# Find similar digital selves

Find similar digital selves by a specific digital self id, given traits, or anything that can describe a digital self.

### API definition

```js
// @param id|traits|idOrTraits - a digital self identity or a hashmap with trait id as key and trait score as value
// @param options - the options to filter the returning result
// @param traitsFilter - a delegate function to filter whether the traits are reached to the criteria
// @return - an array of digital selves that similar to a specific one
async function findDigitalSelves(digitalSelf: DigitalSelf, options: DigitalSelfOptions)
async function findDigitalSelves(digitalSelfvs: DigitalSelf[] ,options: DigitalSelfOptions)
```

### Example 1: find similar digital selves by a specified traits
Find similar digital selves by a specified digital self.

<!-- tabs:start -->

#### **API**

```json
# method
POST

# path
/api/1/parmeus/digitalSelves/singleMatch

# request body
{
    "digitalSelf": {
        "addresse": "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
        "traits": [
            [ 20, 34, 56, 43, 43, 32, 99 ],
            [ 34, 33, 22, 34, 33, 34, 88 ],
            [ 56, null, 78, 44, 67, 45, 78 ]
        ]
    },
    "options": {
        "sort": "desc",
        "count": 20,
        "similarityMatrix": true
    },
    "filter": {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
}
```

#### **JavaScript**

```js
let matchedDigitalSelves = await findDigitalSelves(
    "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
     {
        "sort": "desc",
        "count": 20,
        "similarityMatrix": true
    },
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

#### **Python**

```python
matchedDigitalSelves = findDigitalSelves(
    "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
     {
        "sort": "desc",
        "count": 20,
        "similarityMatrix": True
    },
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

#### **Go**

```go
var matchedDigitalSelves = findDigitalSelves(
    "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
     {
        "sort": "desc",
        "count": 20,
        "similarityMatrix": True
    },
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

<!-- tabs:end -->



### Example 2: Get the similarity matrix about a set of digital selves.
Get the similarity matrix about a set of digital selves.

<!-- tabs:start -->

#### **API**

```json
# method
POST

# path
/api/1/parmeus/digitalSelves/teamMatch

# request body
{
    "digitalSelves": [
        "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
        "0xFD6724B4b3e8eca764F0DD07ccd903aD348D70F8",
        ... // 20 addresses
        "0x87d3F0acF7e35E2400C782225Dd5f7c7ecF1369b"
    ],  
    "options":{
        "heatmap": false,
        "heatmapOptions":{ 
            "annotate": true
        }
    } ,
    "filter": {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
}
```

#### **JavaScript**

```js
let matchedDigitalSelves = await findDigitalSelves(
    [
        "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
        "0xFD6724B4b3e8eca764F0DD07ccd903aD348D70F8",
        ... // 20 addresses
        "0x87d3F0acF7e35E2400C782225Dd5f7c7ecF1369b"
    ],  
    {
        "heatmap": false,
        "heatmapOptions":{ 
            "annotate": true
        }
    }, 
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

#### **Python**

```python
matchedDigitalSelves = findDigitalSelves(
    [
        "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
        "0xFD6724B4b3e8eca764F0DD07ccd903aD348D70F8",
        ... # 20 addresses
        "0x87d3F0acF7e35E2400C782225Dd5f7c7ecF1369b"
    ],  
    {
        "heatmap": false,
        "heatmapOptions":{ 
            "annotate": true
        }
    }, 
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

#### **Go**

```go
matchedDigitalSelves = findDigitalSelves(
    [
        "0xa0BcEeffDf6FA19A5e4Ac5117B97CE180Cd7039a",
        "0xFD6724B4b3e8eca764F0DD07ccd903aD348D70F8",
        ... // 20 addresses
        "0x87d3F0acF7e35E2400C782225Dd5f7c7ecF1369b"
    ],  
    {
        "heatmap": false,
        "heatmapOptions":{ 
            "annotate": true
        }
    },
    {
        "traits": [
            "critical_thinking",
            "curiosity",
            "fluid_intelligence",
            "flexibility",
            "grit",
            "initiative"
        ]
    }
);
```

<!-- tabs:end -->

