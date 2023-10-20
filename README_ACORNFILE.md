# Text Embeddings Inference Acorn

Acorn for a blazing fast inference solution for text embeddings models.

## (Optional) Set model ID

If you'd like to specify the model ID that the inference server should load, select "Advanced Options" in the Acorn UI and hit next. You'll be able to input your preferred model ID on the next screen.

The `Model Id` is the name of the model you want to load. Can be a model as listed on <https://hf.co/models> like `thenlper/gte-base`. 
Or it can be a local directory containing the necessary files as saved by `save_pretrained(...)` methods of 
transformers


## Text Embeddings Inference API

After successfully deploying this Acorn, you'll have access to a set of endpoints that allow you to get embeddings for a given text.

E.g.
```bash
curl https://still-shadow-3cd9d4dd.qactc6.on-acorn.io/embed \
    -X POST \
    -d '{"inputs":"What is Deep Learning?"}' \
    -H 'Content-Type: application/json'
``````

Or if you want an OpenAI embeddings formatted response:
```bash
curl https://still-shadow-3cd9d4dd.qactc6.on-acorn.io/openai \
    -X POST \
    -d '{"input":"What is Deep Learning?"}' \
    -H 'Content-Type: application/json'
```

To check what model your Acorn is using, you can use the following endpoint:
```bash
curl -X GET "https://withered-bush-002b4532.qactc6.on-acorn.io/info"
```

---

## Endpoints

### `POST /embed`

**Description**: Get Embeddings

**Request Body**:
```json
{
  "inputs": "string or array of strings",
  "truncate": "boolean (optional, default: false)"
}
```

**Responses**:
- `200 OK`: Embeddings
- `413 Payload Too Large`: Batch size error
- `422 Unprocessable Entity`: Tokenization error
- `424 Failed Dependency`: Embedding Error
- `429 Too Many Requests`: Model is overloaded

---

### `POST /openai`

**Description**: OpenAI compatible route

**Request Body**:
```json
{
  "input": "string or array of strings",
  "model": "string (optional)",
  "user": "string (optional)"
}
```

**Responses**:
- `200 OK`: Embeddings
- `413 Payload Too Large`: Batch size error
- `422 Unprocessable Entity`: Tokenization error
- `424 Failed Dependency`: Embedding Error
- `429 Too Many Requests`: Model is overloaded

---

### `GET /health`

**Description**: Health check method

**Responses**:
- `200 OK`: Everything is working fine
- `503 Service Unavailable`: Text embeddings Inference is down

---

### `GET /info`

**Description**: Text Embeddings Inference endpoint info

**Responses**:
- `200 OK`: Served model info

---

### `GET /metrics`

**Description**: Prometheus metrics scrape endpoint

**Responses**:
- `200 OK`: Prometheus Metrics

