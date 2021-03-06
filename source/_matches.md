
# Matches

Matches records are created every time players complete a game session. Each Match
contains high level information about the game session, including info like
duration, gameMode, and more.  Each Match has two Rosters.   


## Rosters

```json
{
  "type": "roster",
  "id": "eca49808-d510-11e6-bf26-cec0c932ce01",
  "attributes": {
    "stats": {
      "acesEarned": 2,
      "gold": 32344,
      "etc..."
    }
  },
  "relationships": {
    "team": {
      "data": {
        "type": "team",
        "id": "753d464c-d511-11e6-bf26-cec0c932ce01"
      }
    },
    "participants": {
      "data": [
        {
          "type": "participant",
          "id": "eca49a7e-d510-11e6-bf26-cec0c932ce01"
        },
        "etc..."
      ]
    }
  }
}
```

Rosters track the scores of each opposing group of Participants. If players entered
matchmaking as a team, the Roster will have a related Team.  Rosters have many Participants
objects, one for each member of the Roster. Roster objects are only meaningful
within the context of a Match and are not exposed as a standalone resource.

## Participants

```json
{
  "type": "participant",
  "id": "ea77c3a7-d44e-11e6-8f77-0242ac130004",
  "attributes": {
    "actor": "*Hero009*",
    "stats": {
      "assists": 4,
      "crystalMineCaptures": 1,
      "deaths": 2,
      "farm": 49.25,
      "etc..."
    }
  }
}
```
Participant objects track each member in a Roster.  Participants may be
anonymous Players, registered Players, or bots. In the case where the Participant
is a registered Player, the Participant will have a single Player relationship.
Participant objects are only meaningful within the context of a Match and are
not exposed as a standalone resource.

## Get a collection of Matches

```shell
curl -g "https://api.dc01.gamelockerapp.com/shards/na/matches?sort=createdAt&page[limit]=3&filter[createdAt-start]=2017-02-27T13:25:30Z&filter[playerNames]=<playerName>" \
  -H "Authorization: Bearer <api-key>" \
  -H "X-TITLE-ID: semc-vainglory" \
  -H "Accept: application/vnd.api+json"
```
```java
//There are a variety of Java HTTP libraries that support query-parameters.
```
```python
import requests

url = "https://api.dc01.gamelockerapp.com/shards/na/matches"

header = {
    "Authorization": "<api-key>",
    "X-TITLE-ID": "semc-vainglory",
    "Accept": "application/vnd.api+json"
}

query = {
    "sort": "createdAt",
    "filter[playerNames]": "<playerName>",
    "filter[createdAt-start]": "2017-02-28T13:25:30Z",
    "page[limit]": "3"
}

r = requests.get(url, headers=header, params=query)
```
```ruby
```
```javascript
```
```go
q := req.URL.Query()
q.Add("sort", "createdAt")
q.Add("filter[playerNames]", "<playerName>")
q.Add("filter[createdAt-start]", "2017-02-27T13:25:30Z")
q.Add("page[limit]", "3")
req.URL.RawQuery = q.Encode()
res, _ := client.Do(req)
```
> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "type": "match",
      "id": "02b90214-c64d-11e6-9f6b-062445d3d668",
      "attributes": {
        "createdAt": "2017-01-06T20:30:08Z",
        "duration": 1482195372,
        "gameMode": "casual",
        "patchVersion": "1.0.0",
        "region": "na",
        "stats": "acesEarned: 3, etc..."
      },
      "relationships": {
        "rosters": {
          "data": [{
            "type": "roster",
            "id": "ea77c2eb-d44e-11e6-8f77-0242ac130004"
          }, {
            "type": "roster",
            "id": "dc2c14b4-d50c-11e6-bf26-cec0c932ce01"
          }]
        }
      }
    }
  ]
}
```

This endpoint retrieves data from matches. Bulk scraping matches is prohibited.

### HTTP Request

`GET https://api.dc01.gamelockerapp.com/shards/na/matches`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page[offset] | 0 | Allows paging over results
page[limit] | 50 | The default (and current maximum) is 50.  Values less than 50 and great than 2 are supported.
sort | createdAt | By default, Matches are sorted by creation time ascending.
filter[createdAt-start] | 3hrs ago | Must occur before end time.  Format is iso8601  Usage: filter[createdAt-start]=2017-01-01T08:25:30Z
filter[createdAt-end] | Now | Queries search the last 3 hrs. Format is iso8601 i.e. filter[createdAt-end]=2017-01-01T13:25:30Z
filter[playerNames] | none | Filters by player name. Usage: filter[playerNames]=player1,player2,...
filter[playerIds] | none | Filters by player Id. Usage: filter[playerIds]=playerId,playerId,...
filter[teamNames] | none | Filters by team names. Team names are the same as the in game team tags. Usage: filter[teamNames]=TSM,team2,...
filter[gameMode] | none | filter by gameMode Usage: filter[gameMode]=casual,ranked,...

<aside class="success">
Remember — a happy match is an authenticated match!
</aside>

## Get a single Match

```shell
curl "https://api.dc01.gamelockerapp.com/shards/na/matches/<matchID>" \
  -H "Authorization: Bearer <api-key>" \
  -H "X-TITLE-ID: semc-vainglory" \
  -H "Accept: application/vnd.api+json"
```
```java
//There are a variety of Java HTTP libraries that support URL parameters
```
```python
```
```ruby
```
```javascript
```
```go
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "type": "match",
    "id": "02b90214-c64d-11e6-9f6b-062445d3d668",
    "attributes": {
      "createdAt": "2017-01-06T20:30:08Z",
      "duration": 1482195372,
      "gameMode": "casual",
      "patchVersion": "1.0.0",
      "region": "na",
      "stats": "acesEarned: 3, etc..."
    },
    "relationships": {
      "rosters": {
        "data": [{
          "type": "roster",
          "id": "ea77c2eb-d44e-11e6-8f77-0242ac130004"
        }, {
          "type": "roster",
          "id": "dc2c14b4-d50c-11e6-bf26-cec0c932ce01"
        }]
      }
    }
  }
}
```

This endpoint retrieves a specific match.

### HTTP Request

`GET https://api.dc01.gamelockerapp.com/shards/na/matches/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the match to retrieve
