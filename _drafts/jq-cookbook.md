---
layout: post
title: jq Cookbook
---

## Draft stage!

Don't both reading just yet. :) 

## Introduction

`jq` is a pretty handy tool. Naively, it's great at formatting JSON from a `curl` command, and also filtering
out some specific keys. However, you can a serious amount of operations on JSON using `jq`. That being said,
I found examples and documentation on the internet to be a bit lacking and hard to apply to my own use-cases.
So I'm chucking this together. Hopefully it's helpful for some of you.

If you're totally new to `jq`, this probably isn't the blog post for you. There's plenty of those around
if you search for it, or you can refer to the [official documentation](https://stedolan.github.io/jq/).

## Recipes

This will be a table of contents to the rest of the blog.

Ideas:
* Formating data
  * General output
  * Converting to object
  * Converting to list
* Pipes
* Changing the keys
* Changing the values
* Defining and using variables
* Retrieving all paths from an OpenAPI file.
* Flattening data. e.g. Make a path suffixed with each HTTP method. End up with multiple paths suffixed with unique HTTP methods.
* Boatload of other interesting things.

### A thing

For this example we will do a thing.

#### Input JSON data

Contents of `data.json`:
```
{
    "some": "json"
}
```

#### (Optional if we want) Desired output JSON data

```
{
    "something": "else"
}
```

#### Command

`jq blah data.json`

