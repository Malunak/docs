---
title: Malunak API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

toc_footers:
  - <a href='https://malunak.dev/'>Malunak.dev</a>
  - <a href='https://dash.malunak.dev/'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Malunak API
---

# Introduction

Welcome to the Malunak API! You can use our API to access Malunak API endpoints, which can classify images using our special machine learning models.

We have language bindings in Shell (using cURL)! You can view code examples in the dark area to the right, and, as soon as more SDKs are available, you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "X-Malunak-Token: [client-id]:[client-secret]"
```

> Make sure to replace `[client-id]` and `[client-secret]` with your project's credentials.

Malunak uses API keys to allow access to the API. You can register a new project and get Malunak client ID and secret at our [developer portal](https://kolas.pkasila.net/).

Malunak expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-Malunak-Token: [client-id]:[client-secret]`

<aside class="notice">
You must replace <code>[client-id]:[client-secret]</code> with your personal client ID and secret.
</aside>

# AI Image Detection (Kupala)

## Predict

```shell
curl -X 'POST' \
  'https://kupala.pkasila.net/predict' \
  -H 'X-Malunak-Token: [client-id]:[client-secret]' \
  -H 'Content-Type: multipart/form-data' \
  -F 'files=@example0.jpeg;type=image/jpeg' \
  -F 'files=@example1.png;type=image/png'
```

> The above command returns JSON structured like this:

```json
{
  "predictions": [
    {
      "artificial": 0.9524049758911133,
      "human": 0.047595005482435226
    },
    {
      "artificial": 0.2845001816749573,
      "human": 0.7154998183250427
    }
  ]
}
```

This endpoint predicts whether image(s) is created by human or artificial intelligence.

### HTTP Request

`POST https://kupala.pkasila.net/predict`

### Multipart Form Data

| Field | Description                                                     |
|-------|-----------------------------------------------------------------|
| files | 1 or more image files in JPEG/PNG/WebP formats to be classified |

### Response Object

| Field                      | Description                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| `predictions`              | an array of predictions (classifications) ordered in the files order in the query |
| `predictions[].artificial` | the prediction for `artificial` class                                             |
| `predictions[].human`      | the prediction for `human` class                                                  |

<aside class="success">
Remember — a nice request is an authenticated request!
</aside>
