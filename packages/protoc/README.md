@protobuf-ts/protoc
===================

Installs the protocol buffer compiler "protoc" for you. 


Installation (not necessary if you use the [protobuf-ts plugin](https://github.com/timostamm/protobuf-ts/tree/master/packages/plugin)):

```shell script
# with npm:
npm install @protobuf-ts/protoc

# with yarn:
yarn add @protobuf-ts/protoc
```             

Now you can run protoc as usual, you just have to prefix your command with `npx`:

```shell script
npx protoc --version 
``` 

Plugins are picked up automatically. If you have a `node_modules/.bin/protoc-gen-foo`, just run:

```shell script
npx protoc --foo_out ./bar 
```

If you use yarn, you can prefix your command with `yarn` instead of `npx`:

```shell script
yarn protoc --version 
``` 



#### How it works:

After you have installed `@protobuf-ts/protoc`, it will download the latest protoc 
release for your platform and install it in your `./node_modules/@protobuf-ts/protoc/dist` 
directory. It will also provide a wrapper script in `./node_modules/.bin/protoc`. 

When you run `npx protoc`, npx will find `./node_modules/.bin/protoc` (the wrapper script) 
and run it.

The wrapper script basically just launches the downloaded protoc, but it adds the 
following behaviour: 

1. add a `--proto_path` argument that points to the `include/` directory of the 
   downloaded release
2. add a `--plugin` argument for all plugins found in `node_modules/.bin/`
3. add a `--proto_path` argument for `node_modules/@protobuf-ts/plugin` 

The package has been tested on macos, linux and windows.


#### Installing a specific version

Add the following to your package json **before** installing `@protobuf-ts/protoc`:

```
"config": {
   "protocVersion": "3.11.0"
}
``` 
