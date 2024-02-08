> [!NOTE]
> Aerospike Vector Search capabilities are in an invite only Alpha stage. Please
> fill out the following [form](https://aerospike.com/lp/aerospike-vector-developer-program-sign-up/) if you are interested to try it out. 

# About Proximus
Proximus is Aerospike's vector search solution. 

This repo provides example apps for building apps using Proximus to perform vector
search. Vectors allows you to combine machine learning models, like ChatGPT, CLIP,
Llama, etc. to build applications that leverage these models AI capabilities. This means
you can encode meaning from text, images, video, etc and search across a large dataset.
This can be used for a variety of applications such as semantic search, recommendation systems,
retrieval augmented generation (RAG) apps and more. For more about leveraging Vector Embeddings
see the [OpenAI Docs about vector embedding use cases](https://platform.openai.com/docs/guides/embeddings/use-cases). 

# Getting Started
This repo provides details on how to get started using our Developer Sandbox
environment. To request a developer sandbox fill out the following [form](https://aerospike.com/lp/aerospike-vector-developer-program-sign-up/). These instructions go through setting up a
demo application that performs semantic search across an image data set using the [CLIP](https://arxiv.org/abs/2103.00020) model. 

## Pre-requisites
To get started you do not need any knowledge of Aerospike, but you do need the following.

1. Python 3.8+ and familiarity with the python programming language.
1. A URL to your private sandbox environment (this will be provided) **or**
1. Access to [aerospike.jfrog.io](https://aerospike.jfrog.io/ui/login/)

## 1. Clone Repo and setup dependencies

```
git clone https://github.com/aerospike/proximus-examples.git && \\
cd proximus-examples/prism-image-search/ && \\
python3 -m pip install -r requirements.txt
```

If you have access to [aerospike.jfrog.io](https://aerospike.jfrog.io/ui/login/) follow
[these steps instead](./prism-image-search/README.md#docker-compose).

## 2. Find an image dataset to index

The demo application works by indexing images stored on your computer, and 
generating vector embeddings that are sent to a Proximus server hosted in the cloud.
To make the experience personal, you can use your own photos on your computer, or to index
a larger dataset you can browse image datasets on [Kaggle](https://www.kaggle.com/datasets).  

[This subset](https://www.kaggle.com/datasets/ifigotin/imagenetmini-1000) of the Imagenet
dataset is a good reasonable sized one (~4000 images) if you remove the `train` folder. 

> [!NOTE]
> The images from your dataset do not leave your local environment, but the vector embeddings
> are sent to our sandbox environment. All data is destroyed when your sandbox trial expires.

Once you have a dataset of images (must be jpeg's), copy them to `prism/static/images/data`

## 3. Set environment variables
Before starting the app you need to set the PROXIMUS_HOST to your sandbox host. 

```
export PROXIMUS_HOST=<SANDBOX-HOST>
```
Depending on your dataset, you may also want to also configure concurrent threads 
for generating the image embeddings (this will put strain on your CPU).

```
export INDEXER_PARALLELISM=4
```

## 4. Start the application locally.
To start the application run.
```
cd prism && \
waitress-serve --host 127.0.0.1 --port 8080 --threads 32 prism:ap
```
You will see a progress bar as new images are read and indexed using the clip model.

## 5. Perform an image search
Depending on the size of your dataset, it will take anywhere from a few minutes, to
a few hours to index your images. Once it started open up 

# Limitations
The sandbox environment is limited to a single index. If you need to create a different
index please get in touch about getting a new sandbox environment. 

# Contributing
If you have an idea for a sample app please open a PR and we'll review. We're excited to provide more examples
of what Vector Search can do. 