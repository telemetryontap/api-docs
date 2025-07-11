# Using the API 

### Swagger API Spec: [Swagger UI](https://docs.telemetryontap.com/swag/)

## API Specification
The Telemetry on Tap API follows REST API standards and makes OpenAPI swagger available on the ethernet interface of machines. 


To connect to swagger on your device:

http://{YOUR_DEVICE_IP_ADDRESS}/docs

Example:

http://192.168.1.100/docs

## API Format


API calls should be formatted in the following format: 

`https://telemetryontap.com/endpointName/?`

## Authorization 

No authorization is required, but it is required to connect to the interface via ethernet. 

Additional security in the form of a certificate or key authorization is available upon request. 

## Available Endpoints 

Telemetry on Tap provides API endpoints to confrigure and get the most out of your **[insert product name]** and provide your guests with great beverages.


### GET

| Endpoint Name | Description | When to Use This Endpoint |
| --- | --- |---|
| / | Used to verify the online status of a machine. | Use this endpoint to verify if a machine is online. |
| **/product_sources**| Used to check the status of a BiB (bag in ox) product. | Use this endpoint to check the status details about BiB products connected to the machine. 
| **/product_source** | Returns a list of all product sources that are registered to the machine. | Use this endpoint to return a list of product source details about products that are registered for use with the machine. 
| **/dispense** | Returns the current status of dispense. All lines and the current dispense will be included in the returned status. If there are no current dispense operations, the active sources will be returned empty. Dispense is specific to the configuration of a particular Line. | Use this endpoint to check dispense points in a Line, to determine what is currenly being dispensed from each dispense point. 
| **/reboot_system** | Sends a reboot command to the system that will attempt to restart the system. | Use this endpoint when the system needs rebooted. 
| **/abort_dispense** | Cancels all current dispense operations. | Use this endpoint to cancel dispense in the event of an emergency.

### POST

| Endpoint Name | Description | When to Use This Endpoint
| --- | --- |---|
| **/product_sources** | Used to update a single product source. | Use this endpoint to update calibration data, source name or other properties about the product source that are available via API. Additonal properties can be added upon request. 
| **/dispense** | This will start a new dispense operation, with a specified quantity of ingredients per product source. A list of product source dispense requests is passed into the request, with quanitities of each product source that will be dispensed. | Use this endpoint on machines that use multiple sources and a singple dispense point (Line). This is typically used when a 3rd party system has a recipe specification that is passed to the machine, and the system's integrated recipe system will not be used. A prodcut source can be directly activated to request a specific quanity of a product source. 
| **/dispense_continuous** | When activated, a list of requested product source ingredients and requested flow rate (by percentage) is sent to the machine. The machine will dispense and continue to dispense until a stop dispense request is made or an abort request is received. | Use this endpoint when an external system uses a ratio dispense and will continue to dispense while a user pulls a handle or pushes a button. This is prefered for user specified quantities where the desitnation container size is not known. 
| **/stop_source_dispense** | This stops dispense for a source ingredient that is currently dispensing. | Use this endpoing to stop a continuous dispense operation for a spcific source ingredient. 
| **/pull_line_tap** | This simulates a line tap pull. | Use this endpoint to signal to the system that a line tap handle or button has been pressed to trigger the activation of dispense for a Line. The currentnly selected recipe will be dispensed. 
| **/release_line_tap** | This simulates a line tap release. | Use this endpoint to signal to the system that a line tap handle or button has been released and will disable dispense for a line. The currently selected recipe will stop dispensing. 

## Frequently Asked Questions 

### What is a Line?
A line is a dispense head or dispense endpoint that can be independenly activated and dispenses from one or more product sources. 

### What is Dispense?
Dispense refers to the action of dispensing a product source to a line. 

### What is a a product source?
A product source referse to a BiB, or a list of ingredients that are used to dispense a beverage. 