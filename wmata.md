---
permalink: /wmata/
---

## WMATA-GO-SDK

The Washington Metropolitan Area Transit Authority (WMATA) publishes several APIs to retrieve information about Bus and Train lines as well as active problems. These APIs follow different patterns and can be confusing to use. To help standardize this approach I built an [Go SDK](https://github.com/awiede/wmata-go-sdk) to communicate with these APIs from a GoLang application.

### Install

To install the SDK run the following command:

```bash
go get -u github.com/awiede/wmata-go-sdk
```

### Usage

This project is broken up into separate packages for each grouping of WMATA APIs. Please see more detailed information in the [Usage section](https://github.com/awiede/wmata-go-sdk/blob/master/README.md#usage) of the README for detailed usage information. 

Each API grouping is packaged as a separate service, each of which leverages a `wmata.Client`. This client requires an API key which must be obtained by registering with [WMATA](https://developer.wmata.com/).

Once you have your API key you can create a service like this:

```go
apiKey := "<your-api-key>"
client := http.Client{
    Timeout: time.Second * 60,
}
wmataClient := wmata.NewWMATAClient(apiKey, client)

// Defaults with a 30 second timeout
defaultClient := wmata.NewWMATADefaultClient(apiKey)
```

Once you have a client, you can use it to create each service like this:

```go
// Create rail info service using WMATA client in previous example
railInfoService := railinfo.NewService(wmataClient, wmata.JSON)

// Invoke the GetLines() method of the rail service to get active line info
activeRailLines, err := railInfoService.GetLines()
```

## Links

* [WMATA API Documentation](https://developer.wmata.com/docs/services/)
* [WMATA GO SDK](https://github.com/awiede/wmata-go-sdk) Project on GitHub
