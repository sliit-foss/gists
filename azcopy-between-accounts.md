# AzCopy Between Accounts
AzCopy is a command-line utility provided by Microsoft for efficiently transferring data to and from Azure Blob Storage. It's useful for migrating large volumes of data, copying data between storage accounts, and syncing data between local files and Blob Storage.

## Prerequisites

1. **Azure Subscription**: You need an active Azure subscription to use Azure Blob Storage.
   
2. **Azure Storage Account**: Create Azure Storage accounts for both the source and destination containers.

3. **AzCopy Installation**: Install AzCopy on your local machine or server. You can download AzCopy from the [official download page](https://aka.ms/downloadazcopy).

4. **Azure Blob Container**: Create Blob containers within your Azure Storage accounts for storing data.

#### Guidelines

- If you're using Microsoft Entra authorization for both source and destination, then both accounts must belong to the same Microsoft Entra tenant.

- Your client must have network access to both the source and destination storage accounts. To learn how to configure the network settings for each storage account, see [Configure Azure Storage firewalls and virtual networks](https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?toc=/azure/storage/blobs/toc.json).

- If you copy to a premium block blob storage account, omit the access tier of a blob from the copy operation by setting the ``s2s-preserve-access-tier`` to ``false`` (For example: `--s2s-preserve-access-tier=false`). Premium block blob storage accounts don't support access tiers.

- You can increase the throughput of copy operations by setting the value of the ``AZCOPY_CONCURRENCY_VALUE`` environment variable. To learn more, see [Increase Concurrency](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-optimize#increase-concurrency).

- If the source blobs have index tags, and you want to retain those tags, you'll have to reapply them to the destination blobs. For information about how to set index tags, see the [Copy blobs to another storage account with index tags](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-blobs-copy?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&bc=%2Fazure%2Fstorage%2Fblobs%2Fbreadcrumb%2Ftoc.json#copy-between-accounts-and-add-index-tags) section of this article.

## Setup

1. **Authentication**
   
   Log in to Azure using Azure CLI:
   ```bash
   az login
   ```
- Ensure proper permissions and network connectivity for accessing Azure Blob Storage.

## Usage

1. **Copy Blob**

   ```bash
   azcopy copy "https://[source_storage_account].blob.core.windows.net/[source_container]/[source_blob]?[source_SAS_token]" "https://[destination_storage_account].blob.core.windows.net/[destination_container]/[destination_blob]?[destination_SAS_token]"
   ```

2. **Copy Directory**

   ```bash
   azcopy copy "path/to/source_directory" "https://[destination_storage_account].blob.core.windows.net/[destination_container]/[destination_blob_prefix]?[destination_SAS_token]" --recursive=true
   ```

3. **Copy Entire Container**

   ```bash
   azcopy copy "https://[source_storage_account].blob.core.windows.net/[source_container]/?[source_SAS_token]" "https://[destination_storage_account].blob.core.windows.net/[destination_container]/?[destination_SAS_token]" --recursive=true
   ```

4. **Copy Entire Storage Account**

   ```bash
   azcopy copy "https://[source_storage_account].blob.core.windows.net/?[source_SAS_token]" "https://[destination_storage_account].blob.core.windows.net/?[destination_SAS_token]" --recursive=true
   ```

- Replace placeholders such as `[source_storage_account]`, `[source_container]`, `[source_blob]`, `[source_SAS_token]`, `[destination_storage_account]`, `[destination_container]`, `[destination_blob]`, and `[destination_SAS_token]` with your actual values.

- Use `--recursive=true` for recursive operations, such as copying directories or entire containers.

- By default, AzCopy will overwrite the files at the destination if they already exist. To avoid this behavior, please use the flag `--overwrite=false`.

- Refer to the [AzCopy documentation](https://docs.microsoft.com/azure/storage/common/storage-ref-azcopy) for detailed usage instructions and additional options.

---
---
