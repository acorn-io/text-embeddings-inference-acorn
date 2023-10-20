<div align="center">

# Text Embeddings Inference Acorn

<a href="https://github.com/huggingface/text-embeddings-inference">
  <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/huggingface/text-embeddings-inference?style=flat&logo=github&label=GH Repo">
</a>
<a href="https://huggingface.github.io/text-embeddings-inference">
  <img alt="Swagger API documentation" src="https://img.shields.io/badge/API-Swagger-informational">
</a>

Acorn for a blazing fast inference solution for text embeddings models.
</div>

## Usage

```bash
acorn run index.docker.io/sanjay920/text-embeddings-inference:cpu --model_id MODEL_ID
```

* Where `MODEL_ID` is the name of the model you want to load. Can be a MODEL_ID as listed on <https://hf.co/models> like `thenlper/gte-base`. 
          Or it can be a local directory containing the necessary files as saved by `save_pretrained(...)` methods of 
          transformers

## Deploy the Inference Server

You can deploy the inference server on the Acorn SaaS platform with the following simple steps:

1. Login into the [Acorn SaaS Platform](https://beta.acorn.io/) using the Github Sign-In option with your Github user.
2. Select the "Create Acorn" option.
3. Choose the source for deploying your Acorns
  * Select "From Acorn Image" to deploy the inference server and select its Image
  * Provide any random name such as `embedding-inference-server` and keeping Project's default Region, type in the below Acorn image and choose Create 
    ```bash
    docker.io/sanjay920/text-embeddings-inference:cpu
    ```
    * If you'd like to specify the model ID as mentioned [here](#Usage), select "Advanced Options" in the Acorn UI and hit next. You'll be able to input your preferred model ID on the next screen.
4. Now the embedding inference server is provisioned on Acorn SaaS Platform and is available for 2hrs. Upgrade to pro account to keep it running longer.
5. Once the Acorn is running, you can call the inference server's endpoints to get embeddings.

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
