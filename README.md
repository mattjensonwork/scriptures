# Scripture Embedding and Search Repository

This repository contains scripts to embed scriptures and search them.

## Prerequisites

Ensure you've exported your `OPEN_API_KEY` environment variable prior to running:

```bash
export OPEN_API_KEY=your_api_key_here
```

## Embedding Scriptures

If you want to do your own embeddings, clone the following repository:

```bash
git clone https://github.com/bcbooks/scriptures-json
```

For each book you want to embed, type:

```bash
./embed book.json
```

For the Doctrine and Covenants, which has a unique structure, just type:

```bash
./embed-dandc
```

Note that this will create the Chroma database in whatever directory you issue the command in. The Chroma database will be named `scriptures_db`.

## Using Pre-embedded Scriptures

If you want to skip the embedding steps/cost, just download http://dugg.in/s.zip and unzip it:

```bash
unzip s.zip
```

The file is approximately 450 MB.

## Running Searches

To run any of the searches, make sure you are in the same directory as the `scriptures_db` directory, and just type:

```bash
./search am I a child of God
```

It will combine all the words on the command line into the query. No quotes are neeed. Pay attention to not using special 
shell characters.

If you want to use special characters, like ?, put it in quotes:

```bash
./search "am I a child of God?"
```

Alternatively, you can just type `./search` and enter the terms on stdin followed by `CTRL-D`.

## Combine Search Methods

The `combine` command does all the different methods and overwrites `output.xlsx` with the results for comparison.

### Supported Search Methods

- `search` - normal similarity search
- `search-with-mmr` - max marginal relevance search, should have more diverse matches
- `search-with-ai` - uses AI to refine your search terms
- `search-with-languages` - embeds in English, Spanish, and Mandarin and uses the average embedding to search


# Pinecone DB
All of the above commands also work against a pinecone database. To make this work ensure your Pinecone API 
key is exported to PINECONE_API_KEY:

```bash
export PINECONE_API_KEY=your_pinecone_api_key_here
```

If you are creating the embeddings, create the index first. You can do it in python or in 
the console. Name it scriptures and set the dimension to 1536.

After it has been created and populated (or if you have an API key to one that someone else has created) you can simply issue
all of the above search commands with a p prepended:

### Supported Search Methods

- `psearch` - normal similarity search
- `psearch--with-mmr` - max marginal relevance search, should have more diverse matches
- `psearch-with-ai` - uses AI to refine your search terms
- `psearch-with-language` - embeds in English, Spanish, and Mandarin and uses the average embedding to search

This version should be much faster and can be horizontally scaled.

