---
title: "Protobuf Node Typescript"
date: 2018-02-12
tags: 
draft: true
---
# Explain what protobufs are

Install the Protocal Compiler (protoc) compiler using Homebrew:
```bash
$ brew instsall protobuf
```
It can be installed for other platforms using the binaries here: [https://github.com/google/protobuf/releases](https://github.com/google/protobuf/releases)

Install the Javascript protobuf runtime library with npm/yarn:
```bash
$ yarn add google-protobuf
```
Install the ts-protoc-gen protoc plugin to generate TypeScript declarations:
```bash
$ yarn add -D ts-protoc-gen
```
Invoke protoc with these arguments:
```bash
$ protoc \
--plugin=protoc-gen-ts=./node_modules/.bin/protoc-gen-ts \
--js_out=import_style=commonjs,binary:. \
--ts_out=service=true:. \
gtfs-realtime.proto
```
What do these `protoc` arguments mean?
`--plugin=protoc-gen-ts=./node_modules/.bin/protoc-gen-ts`
The `--plugin` flag tells `protoc` to use a plugin named `protoc-gen-ts` whose binary is found in `./node_modules/.bin/protoc-gen-ts`

`--js_out=import_style=commonjs,binary:.`
The `--js_out` flag tells `protoc` to generate Javascript source code from the protocol buffer files. `import_style=commonjs` instructs `protoc` to use commonjs imports which allows us to do this `const stuff = require('./stuff_pb')` in our code. Specifying `binary` in `js_out` generates methods for binary serialization/deserialization. According to  the [Protocol Buffers docs](https://developers.google.com/protocol-buffers/docs/reference/javascript-generated):
- deserializeBinary(): Static method. Deserializes a message from protocol buffers binary wire format and returns a new populated message object. Does not preserve any unknown fields in the binary message.
- deserializeBinaryFromReader(): Static method. Deserializes a message in protocol buffers binary wire format from the provided BinaryReader into the provided message object. Does not preserve any unknown fields in the binary message.
- serializeBinary(): Serializes this message to protocol buffers binary wire format.
- serializeBinaryToWriter(): Serializes this message in protocol buffers binary wire format to the specified BinaryWriter. This method has a static variant where you can serialize a specified message to the BinaryWriter.

# Explain the code that gets generated. Like field accessors (Explained in docs: (https://developers.google.com/protocol-buffers/docs/reference/javascript-generated ))