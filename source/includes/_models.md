# Model Portfolios

## Model Portfolio Object Definition

| Name        | Type                                    | Description              |
| ----------- | --------------------------------------- | ------------------------ |
| id          | int                                     | Model Portfolio ID       |
| external_id | string                                  | Your model identifier    |
| name        | string                                  | Model Portfolio name     |
| value       | string                                  | Model Portfolio value    |
| type        | string                                  | Model Portfolio type     |
| company     | int                                     | Company ID               |
| positions[] | List of [Positions Objects](#positions) | Model Portfolio holdings |
| risk        | [Risk Object](#risk-object-definition)  | Model Portfolio risk     |

> Model Portfolio Object

```shell
{
  "id": 1,
  "external_id": "mp-1",
  "name": "80% Equities / 20% Fixed Income",
  "value": 100.0,
  "type": "Aggressive",
  "company": 1,
  "positions": [
    {
        "ticker": "AGG",
        "ticker_name": "iShares Core US Aggregate Bond",
        "value": 20.0
    },
    {
        "ticker": "SPY",
        "ticker_name": "SPDR S&P500 ETF Trust",
        "value": 80.0
    }
  ],
  "risk": {
    "start_date": "2005-01-01",
    "end_date": "2019-11-10",
    "scores": {
        "concentrated": 1,
        "tail": 8.0,
        "correlation": 8,
        "overall": 6.8,
        "volatility": 6
    },
    "top_risk_attributions": [
        {
            "ticker_name": "SPDR S&P500 ETF Trust",
            "ticker": "SPY",
            "risk": 0.9924230255643414,
            "weight": 80.0
        },
        {
            "ticker_name": "iShares Core US Aggregate Bond",
            "ticker": "AGG",
            "risk": 0.0075769744356585424,
            "weight": 20.0
        }
    ],
    "scenarios": [
        {
            "risk": 8.1,
            "name": "Global Financial Crisis",
            "end_date": "2009-2-1",
            "start_date": "2007-2-1"
        },
        {
            "risk": 7.7,
            "name": "2011 Euro Credit Crisis",
            "end_date": "2012-1-1",
            "start_date": "2010-1-1"
        },
        {
            "risk": 6.4,
            "name": "2013 Taper Tantrum",
            "end_date": "2014-6-1",
            "start_date": "2012-6-1"
        },
        {
            "risk": 6.4,
            "name": "2015-16 Market Selloff",
            "end_date": "2017-1-1",
            "start_date": "2015-1-1"
        }
    ]
  }
}
```

## List Model Portfolios

-request-type: GET

-request-url: `/models/`

> List Model Portfolios

```shell
curl "https://backend.stratifi.com/api/v1/models/" -H "Authorization: Bearer {{ access-token }}"

{
  "count": 10,
  "next": "https://backend.stratifi.com/api/v1/models/?page=2",
  "previous": null,
  "results": [
    {
      "id": 1,
      "external_id": "mp-1",
      "name": "80% Equities / 20% Fixed Income",
      "value": 100.0,
      "type": "Aggressive",
      "company": 1,
      "positions": [ … ],
      "risk": { … }
    },
    …
  ]
}
```

**Response Fields**

| Name     | Type   | Description                                       |
| -------- | ------ | ------------------------------------------------- |
| count    | int    | Total number of models                            |
| next     | string | Link to next page of models                       |
| previous | string | Link to previous page of models                   |
| results  | Object | List of [model objects](#model-object-definition) |

**Filtering Fields**

| Name        | Type   | Description           |
| ----------- | ------ | --------------------- |
| external_id | string | Your model identifier |

## Get Model Portfolio

-request-type: GET

-request-url: `/models/<id>/`

**Response:** The requested [model object](#model-object-definition).

> Get Model Portfolio

```shell
curl "https://backend.stratifi.com/api/v1/models/1/" -H "Authorization: Bearer {{ access-token }}"

{
  "id": 1,
  "external_id": "mp-1",
  "name": "80% Equities / 20% Fixed Income",
  "value": 100.0,
  "type": "Aggressive",
  "company": 1,
  "positions": [ … ],
  "risk": { … }
}
```

## Create Model Portfolio

-request-type: POST

-request-url: `/models/`

> Create Model Portfolio

```shell
curl -X POST "https://backend.stratifi.com/api/v1/models/" -H "Authorization: Bearer {{ access-token }}" \
  -d '{
    "external_id": "mp-1",
    "name": "80% Equities / 20% Fixed Income",
    "value": 100.0,
    "type": "Aggressive",
    "company": 1,
    "positions": [
      {
          "ticker": "AGG",
          "ticker_name": "iShares Core US Aggregate Bond",
          "value": 20.0
      },
      {
          "ticker": "SPY",
          "ticker_name": "SPDR S&P500 ETF Trust",
          "value": 80.0
      }
    ]
  }'

{
  "id": 1,
  "external_id": "mp-1",
  "name": "80% Equities / 20% Fixed Income",
  "value": 100.0,
  "type": "Aggressive",
  "company": 1,
  "positions": [ … ],
  "risk": { … }
}
```

**Request Parameters**

| Parameter   | Type                                    |          |
| ----------- | --------------------------------------- | -------- |
| name        | string                                  | Required |
| positions[] | List of [Positions Objects](#positions) | Required |
| value       | string                                  | Optional |
| type        | string                                  | Optional |
| company     | int                                     | Optional |
| external_id | int                                     | Optional |

**Response:** The new [model object](#model-object-definition).

## Update Model Portfolio

-request-type: PUT/PATCH

-request-url: `/models/<id>/`

**Request Parameters**

| Parameter   | Type                                    |          |
| ----------- | --------------------------------------- | -------- |
| name        | string                                  | Required |
| positions[] | List of [Positions Objects](#positions) | Required |
| value       | string                                  | Optional |
| type \*     | string                                  | Optional |
| company     | int                                     | Optional |
| external_id | int                                     | Optional |

> Update Model Portfolio

```shell
curl -X PUT "https://backend.stratifi.com/api/v1/models/1/" -H "Authorization: Bearer {{ access-token }}" \
  -d '{
    "external_id": "mp-1",
    "name": "70% Equities / 30% Fixed Income",
    "value": 100.0,
    "type": "Moderate",
    "company": 1,
    "positions": [
      {
          "ticker": "AGG",
          "ticker_name": "iShares Core US Aggregate Bond",
          "value": 30.0
      },
      {
          "ticker": "SPY",
          "ticker_name": "SPDR S&P500 ETF Trust",
          "value": 70.0
      }
    ]
  }'

{
  "id": 1,
  "external_id": "mp-1",
  "name": "80% Equities / 20% Fixed Income",
  "value": 100.0,
  "type": "Moderate",
  "company": 1,
  "positions": [ … ],
  "risk": { … }
}
```

## Model Portfolio Prism Score

-request-type: GET

-request-url: `/models/<id>/prism_score/`

> Model Portfolio Prism Score

```shell
curl "https://backend.stratifi.com/api/v1/models/11/prism_score/" -H "Authorization: Bearer {{ access-token }}"

{
  "concentrated": 4.214532742005072
  "concentrated": 4.785445142005072,
  "correlation": 6.049895392953136,
  "overall": 8.2145327985038
  "volatility": 9.224755263382502
}
```

**Response Fields**

| Name         | Type  | Description         |
| ------------ | ----- | ------------------- |
| overall      | float | Overall score       |
| concentrated | float | Concentration score |
| correlation  | float | Correlation score   |
| tail         | float | Tail score          |
| volatility   | float | Volatility score    |
