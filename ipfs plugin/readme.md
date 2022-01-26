# Moralis Pinata IPFS Plugin

This plugin enables interaction with the Pinaata IPFS API (https://www.pinata.cloud/). <br>

## Get started

Grab a free api key here: https://www.pinata.cloud/

<br/>

## Functions

<br/>

### Pin JSON to IPFS

Description: Send a file to Pinata for direct pinning to IPFS.

```ts
interface PinJSONDto {
  body: object;
}
```

```js
await Moralis.Plugins.ipfs.pinJson(PinJSONDto);
```

</br>

### Pin File or Folder to IPFS

Description: Read from a location on your local file system and recursively pin the contents to IPFS.

Both individual files, as well as directories can be read from.

```ts
interface PinFileDto {
  path: string;
}
```

```js
await Moralis.Plugins.ipfs.pinFile(PinFileDto);
```

</br>

```ts
interface PinFolderDto {
  path: string;
}
```

```js
await Moralis.Plugins.ipfs.pinFolder(PinFolderDto);
```

</br>

### Get Pin List

Description: Retrieve pin records for your Pinata account.

```js
await Moralis.Plugins.ipfs.pinList();
```
