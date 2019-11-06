# Rippled RPC Version Requirement

| | <div style="width:400px">Requirement</div> | Comments |
|- | --------------- | -------|
1| The API version number shall be a single unsigned integer. | Another popular version number format is the major.minor.patch format. Our single integer format only has the major number. 
2| The version number shall be increased iff we introduce breaking changes to the API. When the version number is increased, it is increased by one. | We will discuss the list of breaking changes in the design doc.
3| The lowest valid version number shall be 1. | The version number 0 is invalid
4| The rippled API shall support a range of versions with consecutive version numbers. | Currently we plan to support the range [1, 2]
5| Client requests targeting an API version that is out of the supported version range shall be rejected. | Alternatively, if the version number of a request is higher than the supported range, we could lower it’s version number to the highest supported version number to provide some forward compatibility. (I feel it might be confusing). If we use this approach, the responses must have the version number. 
6| Client requests targeting APIs with versions 2 and above shall explicitly state the version number. | As we will see in the design, gRPC will append the version number to the package name of the .proto files. The websocket and JSON-RPC requests (including the JSON-RPC requests sent by rippled command line clients)  will include the version number in the requests’ payloads.  
7| Requests without a version number shall be handled as version 1 requests. | 
8| Including the version numbers in responses shall be optional. | The corresponding requests should be identified by the id field for websocket and JSON-RPC.
9| When we use the rippled command line as a client, the request parameters shall be parsed as and later sent with the latest API version. | 
10| When a client sends multiple requests use a persistent connection (e.g. WebSockets), each request may use a different version number. |
