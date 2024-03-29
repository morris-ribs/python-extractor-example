Azure IOT Hub Extractor
=============

This sample extractor consumes messages from an event hub compatible IOT hub

## Running locally

First, you will need `poetry` installed. You should then be able to run

```
poetry run iot_hub_extractor <config file>
```

from the command line.

To run the extractor with the provided example config, start by setting the
following environment variables for CDF:

 * `COGNITE_PROJECT`
 * `COGNITE_API_KEY`
 * `COGNITE_BASE_URL` (can be omitted if your project is hosted at
   `https://api.cognitedata.com`)

Environment variables can be set for IOT hub details as well:
 * `EVENTHUB_COMPATIBLE_ENDPOINT`
 * `EVENTHUB_COMPATIBLE_PATH`
 * `IOT_SAS_KEY`

See [Read device-to-cloud messages from the built-in endpoint](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-messages-read-builtin) for more details around consuming messages from Azure IOT Hub.

To add configure the IOT connection details update the `azureiothub` section in
`example_config.yaml`, as such:

``` yaml
azureiothub:
    # Event Hub-compatible endpoint
    # az iot hub show --query properties.eventHubEndpoints.events.endpoint --name {your IoT Hub name}
    eventhub_compatible_endpoint: ${EVENTHUB_COMPATIBLE_ENDPOINT}
    # Event Hub-compatible name
    # az iot hub show --query properties.eventHubEndpoints.events.path --name {your IoT Hub name}
    eventhub_compatible_path: ${EVENTHUB_COMPATIBLE_PATH}

    # Primary key for the "service" policy to read messages
    # az iot hub policy show --name service --query primaryKey --hub-name {your IoT Hub name}
    iot_sas_key: ${IOT_SAS_KEY}
    
    # Asset to attach new time series to
    iot_root: iot-root
```
