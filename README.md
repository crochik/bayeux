# bayeux
Bayeux Client Protocol implemented in Golang (as specified by Salesforce Realtime API)

Fork from zph/bayeux:

	Changes to accept both 'payload' and 'sobject'.
	All the channels (user-created or generic) should be accepted.
	Make it so user will pass chan from main function then they can close it anytime.
	User can mention replay mechanism from Channel method.

# Usage
See `examples/main.go`
```golang
package main

import (
	"fmt"

	bay "github.com/elastic/bayeux"
)

func Example() {
	out := make(chan bay.TriggerEvent)
	b := bay.Bayeux{}
	creds := bay.GetSalesforceCredentials()
	replay := "-1"
	c := b.Channel(out, replay, creds, "channel")
	for {
		select {
		case e := <-c:
			fmt.Printf("TriggerEvent Received: %+v", e)
		}
	}
}

func main() {
	Example()
}
```

See annotations in code for cases where the Salesforce implementation of Bayeux seems to differ from official spec.

Salesforce documentation on Realtime API: https://resources.docs.salesforce.com/sfdc/pdf/api_streaming.pdf

# Stability

This code or variant thereof has been steadily running in production since Nov 2016.

The API is very new. So only a few functions are exposed publicly and these can be expected to remain stable until 12/2018, pending massive changes to Salesforce API. Reasonable attempts will be made to maintain API past that deadline.
