# Deletes all topics in An Azure service bus

## Prerequisites:

1. **Azure CLI Installed**: Ensure you have Azure CLI installed on your system. You can download and install it from [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

2. **Azure Account**: You'll need an active Azure account. If you don't have one, you can sign up for a free trial [here](https://azure.microsoft.com/en-us/free/).

3. **Access to Azure Service Bus**: You must have access to the Azure Service Bus namespace and the necessary permissions to delete topics.

## Steps to Setup and Usage:

1. **Authenticate with Azure**: Run `az login` command to authenticate with your Azure account.

2. **Set Variables**: Set the `resource_group` and `namespace` variables in the script to match your Azure Service Bus namespace details.

3. **Save the Script**: Save the script with a `.sh` extension, for example, `delete_servicebus_topics.sh`.
```bash
resource_group=your_rg
namespace=your_namespace

topics=$(az servicebus topic list --resource-group $resource_group --namespace-name $namespace)

ids=""

for i in $(seq 0 $(echo "${topics}" | jq '. | length'))
do
   ids="$ids $(echo "${topics}" | jq ".[$i].id")"
done

az servicebus topic delete --resource-group $resource_group --namespace-name $namespace --ids $ids
```
## Usage
1. **Make the Script Executable**: Run `chmod +x delete_servicebus_topics.sh` to make the script executable.

2. **Run the Script**: Execute the script by running `./delete_servicebus_topics.sh`.

---
---

# Alternative

**Using `--query` global parameter**\
Uses JMESPath query string. See [Here](http://jmespath.org/) for more information and examples.

```bash
#!/bin/bash

usage() {
  echo "Usage: $0 -g <resource_group> -n <namespace> [-y]"
  exit 1
}

confirm_deletion=true

while getopts ":g:n:y" opt; do
  case ${opt} in
    g )
      resource_group=$OPTARG
      ;;
    n )
      namespace=$OPTARG
      ;;
    y )
      confirm_deletion=false
      ;;
    \? )
      echo "Invalid option: $OPTARG" 1>&2
      usage
      ;;
    : )
      echo "Invalid option: $OPTARG requires an argument" 1>&2
      usage
      ;;
  esac
done
shift $((OPTIND -1))

if [ -z "$resource_group" ] || [ -z "$namespace" ]; then
  echo "Resource group and namespace are required."
  usage
fi

echo "Fetching list of topics..."

topics=$(az servicebus topic list --resource-group $resource_group --namespace-name $namespace --query '[].{Name:name, ID:id}' -o json)

if [ -z "$topics" ]; then
  echo "No topics found in the specified resource group and namespace."
  exit 1
fi

echo "Topics to be deleted:"
echo "$topics" | jq -r '.[] | "\(.Name) (\(.ID))"'

if [ "$confirm_deletion" = true ]; then
  read -p "Are you sure you want to delete these topics? (y/n): " confirm
else
  confirm="y"
fi

if [[ $confirm =~ ^[Yy]$ ]]; then
  echo "Deleting topics..."
  ids=$(echo "$topics" | jq -r '.[].ID')
  az servicebus topic delete --resource-group $resource_group --namespace-name $namespace --ids $ids
  echo "Topics deleted successfully."
else
  echo "Deletion cancelled."
fi

```

## Usage

1. **Make the Script Executable**: Run `chmod +x delete_servicebus_topics.sh` to make the script executable.

2. **Run the Script**: Execute the script by running `./delete_servicebus_topics.sh -g <resource_group> -n <namespace> [-y]`.
    - `-g`: Takes resource group.
    - `-n`: Takes namespace.
    - `-y`: Deletes without confirmation.