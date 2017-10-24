# HTTP Service [![Build Status](https://travis-ci.org/dcos-labs/http-service.svg?branch=master)](https://travis-ci.org/dcos-labs/http-service)

This package wraps connections managed by the `@dcos/connection-manager` package into an Observable.

## Usage
```javascript
import { request, stream } from "@dcos/http-service";

request("http://localhost:4200/payload.json")
  .retry(3)
  .subscribe({
    next: response => console.log(response),
    error: event => console.log(event),
    complete: () => console.log("complete")
  });

stream("http://localhost:4200/mesos/api/v1", {
  method: "POST",
  responseType: "text",
  body: JSON.stringify({ type: "SUBSCRIBE" }),
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  }
})
  .subscribe({
    next: data => console.log(data),
    error: event => console.log(event),
    complete: () => console.log("complete")
  });
```
