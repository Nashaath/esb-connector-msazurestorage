# Working with Blobs in Microsoft Azure Storage

[[  Overview ]](#overview)  [[ Operation details ]](#operation-details)  [[  Sample configuration  ]](#sample-configuration)

### Overview 

The following operations allow you to work with blobs. Click an operation name to see details on how to use it.
For a sample proxy service that illustrates how to work with blobs, see [Sample configuration](#sample-configuration).

| Operation        | Description |
| ------------- |-------------|
| [uploadBlob](#uploads-a-blob-file-into-the-storage)    | Uploads a blob file into the storage. |
| [deleteBlob](#deletes-a-blob-file-from-the-storage)      | Deletes a blob file from the storage.     |
| [listBlobs](#retrieves-information-about-all-blobs-in-a-container)    | Retrieves information about all blobs in a container. |

### Operation details

This section provides more details on each of the operations.

#### Uploads a blob file into the storage

The uploadBlob operation uploads a blob file into the storage.

**uploadBlob**
```xml
<msazurestorage.uploadBlob>
    <containerName>{$ctx:containerName}</containerName>
    <fileName>{$ctx:fileName}</fileName>
    <filePath>{$ctx:filePath}</filePath>
</msazurestorage.uploadBlob>
```

**Properties**
* containerName: The name of the container.
* fileName: The name of the file.
* filePath: The path to a local file to be uploaded.

**Sample request**

Following is a sample request that can be handled by the uploadBlob operation.

```json
{
  "accountName": "test",
  "accountKey": "=gCetnaQlvsXQG4PnlXxxxxXXXXsW37DsDKw5rnCg==",
  "containerName": "sales",
  "fileName": "sample.txt",
  "filePath": "/home/user/Pictures/a.txt"
}
```

**Related Microsoft Azure Storage documentation**

[https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage)

#### Deletes a blob file from the storage

The deleteBlob operation deletes a blob file from the storage.

**deleteBlob**
```xml
<msazurestorage.deleteBlob>
    <containerName>{$ctx:containerName}</containerName>
    <fileName>{$ctx:fileName}</fileName>
</msazurestorage.deleteBlob>
```

**Properties**
* containerName: The name of the container.
* fileName: The name of the file.

**Sample request**

Following is a sample request that can be handled by the deleteBlob operation.

```json
{
  "accountName": "test",
  "accountKey": "=gCetnaQlvsXQG4PnlXxxxxXXXXsW37DsDKw5rnCg==",
  "containerName": "sales",
  "fileName": "sample.txt"
}
```
**Related Microsoft Azure Storage documentation**

[https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage)

#### Retrieves information about all bobs in a container

The listBlobs operation retrieves information about all blobs in a container.

**listBlobs**
```xml
<msazurestorage.listBlobs>
    <containerName>{$ctx:containerName}</containerName>
</msazurestorage.listBlobs>
```

**Properties**
* containerName: The name of the container.

**Sample request**

Following is a sample request that can be handled by the listBlobs operation.

```json
{
  "accountName": "test",
  "accountKey": "=gCetnaQlvsXQG4PnlXxxxxXXXXsW37DsDKw5rnCg==",
  "containerName": "sales"
}
```
**Related Microsoft Azure Storage documentation**

[https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage)


#### Sample configuration

Following is a sample proxy service that illustrates how to connect to Microsoft Azure Storage with the init operation and use the listBlobs operation. The sample request for this proxy can be found in the listBlobs sample request.

**Sample Proxy**
```xml
<?xml version="1.0" encoding="UTF-8"?>
    <proxy xmlns="http://ws.apache.org/ns/synapse" name="listBlobs" transports="https,http" statistics="disable" trace="disable" startOnLoad="true">
     <target>
      <inSequence onError="faultHandlerSeq">
      <property name="accountName" expression="json-eval($.accountName)"/>
      <property name="accountKey" expression="json-eval($.accountKey)"/>
      <property name="containerName" expression="json-eval($.containerName)"/>
      <msazurestorage.init>
        <accountName>{$ctx:accountName}</accountName>
        <accountKey>{$ctx:accountKey}</accountKey>
      </msazurestorage.init>
      <msazurestorage.listBlobs>
        <containerName>{$ctx:containerName}</containerName>
      </msazurestorage.listBlobs>
       <respond/>
     </inSequence>
      <outSequence>
       <log/>
       <send/>
      </outSequence>
     </target>
   <description/>
  </proxy>
```