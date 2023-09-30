# @good-i-deer/node-red-contrib-chromadb

[![platform](https://img.shields.io/badge/platform-Node--RED-red)](https://nodered.org)
[![npm version](https://badge.fury.io/js/@good-i-deer%2Fnode-red-contrib-chromadb.svg)](https://badge.fury.io/js/@good-i-deer%2Fnode-red-contrib-chromadb)
[![GitHub license](https://img.shields.io/github/license/GOOD-I-DEER/node-red-contrib-chromadb)](https://github.com/GOOD-I-DEER/node-red-contrib-chromadb/blob/main/LICENSE)

This module provides a node that connects and operates with ChromaDB in Node-RED.

These nodes require node.js version 18.16.1 and Node-RED version 3.1.0.

<hr>

## Description

This node is part of the Facial Recognition with AI package.  
If you would like to see the entire package, please go to the link.
[@good-i-deer/node-red-contrib-vision-ai](https://www.npmjs.com/package/@good-i-deer/node-red-contrib-vision-ai)

ChromaDB is the open-source embedding database. ChromaDB makes it easy to store and query embedded values. This node makes it possible to run ChromaDB operations(create/delete collection, insert/query/delete embedding) in Node-RED.

<hr>

## Pre-requisites

The Node-Red-Contrib-ChromaDB requires [Node-RED](https://nodered.org) to be installed and requires a running [Chroma-DB](https://github.com/chroma-core/chroma) server.

If necessary, you can install and run the chromaDB server on local. Please refer to [Getting Started](https://docs.trychroma.com/getting-started).

<hr>

## Install

```
cd ~/.node-red
npm install @good-i-deer/node-red-contrib-chromadb
```

Restart your Node-RED instance.

<hr>

## Input

Single Embedding

- The input could be an embedding value in the form of an array of real numbers.
- Used for input of **insert** or **query** operation.

Embedding Array

- The input could be embedding values in the form of an array of real number arrays.
- Used for input of **insert** or **query** operation.

ID Array

- The input could be one or more ids in the form of an array of string.
- Used for input of **delete** operation.

<hr>

## property

![image](https://github.com/GOOD-I-DEER/node-red-contrib-chromadb/blob/main/img/properites.png)

Name

- The name of the node displayed on the screen.

Host

- The addreess where ChromaDB server is running.

Port

- The port number where ChromDB server is running.

Operation

- The operation that want to run on ChromaDB.

- Operation Types

  - list: list all collections in ChromaDB server.

  - create: create collection. Does not create if the collection with same name already exists.

  - insert: insert embedding value(s) into the collection.

  - query: query the N nearest distance embeddings.

  - delete: delete embedding with id.

  - drop: drop collection.

DB Name

- The name of DB(collection) that you want to create, delete, or apply the operation.

Dist Method

- The distance method for calculating distances between embeddings.

- You can set the distance method when you create DB.

Result Count

- The number of result you want to get when you run query operation.

- Query operation return N(=result count) nearest distance for each embedding.

<hr>

## Output

Collection list

- After list operation, collection list in the form of a string array are passed within _msg.payload_.

ID Array

- After inserting embeddings, IDs in the form of a string array are passed within _msg.result_.

Query Response

- After querying embeddings, the query response, which contains IDs, distances, metadatas, and documents in the form of an object, is passed within _msg.payload_.

Result

- After create, drop operation, the result explaining success of operation in the form of a string is passed within _msg.result_.

<hr>

## Examples

The following are example flows using Good ChromaDB.

![image](https://github.com/GOOD-I-DEER/node-red-contrib-chromadb/blob/main/img/example.png)

### JSON

```
[
    {
        "id": "1e6ef671efdf6e7b",
        "type": "tab",
        "label": "ChromaDB",
        "disabled": false,
        "info": "",
        "env": []
    },
    {
        "id": "4792f9f4b8190c2f",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "",
        "props": [],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "x": 290,
        "y": 320,
        "wires": [
            [
                "a8efe2228a20081d"
            ]
        ]
    },
    {
        "id": "c6332d85335a6f9f",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Result",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "result",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 750,
        "y": 320,
        "wires": []
    },
    {
        "id": "1d56935af7702c2d",
        "type": "comment",
        "z": "1e6ef671efdf6e7b",
        "name": "Good I Deer ChromaDB",
        "info": "",
        "x": 320,
        "y": 200,
        "wires": []
    },
    {
        "id": "d667ed331e78790d",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "Embeddings",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "[[1.2, 2.4, 4.5], [2.2, 4.4, 4.5]]",
        "payloadType": "jsonata",
        "x": 310,
        "y": 380,
        "wires": [
            [
                "c203de7681166255"
            ]
        ]
    },
    {
        "id": "e778da936ae795f4",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Result",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "result",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 750,
        "y": 380,
        "wires": []
    },
    {
        "id": "6ae163d47c1f45cf",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "Embeddings",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "[[1.2, 2.4, 4.5], [2.2, 4.4, 4.5]]",
        "payloadType": "jsonata",
        "x": 310,
        "y": 440,
        "wires": [
            [
                "5f7cd9e19723b46e"
            ]
        ]
    },
    {
        "id": "32ea1864d84fdb4e",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Payload",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 760,
        "y": 440,
        "wires": []
    },
    {
        "id": "8c25f32070d63b87",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "IDs",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "payload": "[\"id-1\", \"id-2\"]",
        "payloadType": "jsonata",
        "x": 290,
        "y": 500,
        "wires": [
            [
                "cf75be103178217a"
            ]
        ]
    },
    {
        "id": "67946cfb0b10bac5",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Result",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 750,
        "y": 500,
        "wires": []
    },
    {
        "id": "4acb518fd1eb8271",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "",
        "props": [],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "x": 290,
        "y": 260,
        "wires": [
            [
                "603eb6e696d796f2"
            ]
        ]
    },
    {
        "id": "63358d81ceaa24de",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Payload",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 760,
        "y": 260,
        "wires": []
    },
    {
        "id": "624f10863faede9f",
        "type": "inject",
        "z": "1e6ef671efdf6e7b",
        "name": "",
        "props": [],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "x": 290,
        "y": 560,
        "wires": [
            [
                "30f9b81713d706aa"
            ]
        ]
    },
    {
        "id": "796b026101abc5f9",
        "type": "debug",
        "z": "1e6ef671efdf6e7b",
        "name": "Result",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "result",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 750,
        "y": 560,
        "wires": []
    },
    {
        "id": "a8efe2228a20081d",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "Create Collection",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "create",
        "nResults": "1",
        "x": 530,
        "y": 320,
        "wires": [
            [
                "c6332d85335a6f9f"
            ]
        ]
    },
    {
        "id": "c203de7681166255",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "Insert Embeddings",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "insert",
        "nResults": "1",
        "x": 530,
        "y": 380,
        "wires": [
            [
                "e778da936ae795f4"
            ]
        ]
    },
    {
        "id": "5f7cd9e19723b46e",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "Query Embeddings",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "query",
        "nResults": "10",
        "x": 530,
        "y": 440,
        "wires": [
            [
                "32ea1864d84fdb4e"
            ]
        ]
    },
    {
        "id": "cf75be103178217a",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "Delete Embeddings",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "delete",
        "nResults": "1",
        "x": 530,
        "y": 500,
        "wires": [
            [
                "67946cfb0b10bac5"
            ]
        ]
    },
    {
        "id": "30f9b81713d706aa",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "Drop Collection",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "drop",
        "nResults": "1",
        "x": 520,
        "y": 560,
        "wires": [
            [
                "796b026101abc5f9"
            ]
        ]
    },
    {
        "id": "603eb6e696d796f2",
        "type": "good-chroma-db",
        "z": "1e6ef671efdf6e7b",
        "name": "List Collections",
        "dbIp": "http://localhost",
        "dbPort": "8000",
        "dbName": "MyCollection",
        "distance": "cosine",
        "operation": "list",
        "nResults": "1",
        "x": 520,
        "y": 260,
        "wires": [
            [
                "63358d81ceaa24de"
            ]
        ]
    }
]
```

<hr>

## Discussions and suggestions

Use [GitHub Issues](https://github.com/GOOD-I-DEER/node-red-contrib-chromadb/issues) to ask questions or to discuss new features.

<hr>

## Authors

[**GOOD-I-DEER**](https://github.com/GOOD-I-DEER) in SSAFY(Samsung Software Academy for Youth) 9th

- [Kim Jaea](https://github.com/kimjaea)
- [Yi Jong Min](https://github.com/chickennight)
- [Lee Deok Yong](https://github.com/Gitgloo)
- [Lee Che Lim](https://github.com/leecr1215)
- [Lee Hyo Sik](https://github.com/hy06ix)
- [Jung Gyu Sung](https://github.com/ramaking)
<hr>

## Copyright and license

Copyright Samsung Automation Studio Team under the [Apache 2.0 license](https://www.apache.org/licenses/LICENSE-2.0)

<hr>

## Reference

- [Node-RED Creating Nodes](https://nodered.org/docs/creating-nodes/)
- [SamsungAutomationStudio Github Repository](https://github.com/Samsung/SamsungAutomationStudio)
- [ChromaDB Github Repository](https://github.com/chroma-core/chroma)
