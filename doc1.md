# CLOUD DATA OBJECT API SPECIFICATION
Progress is committed to delivering market-leading technology innovations that empower our partners and customers to dramatically improve the development, deployment, integration and management of their business applications. The Cloud Data Object brings data management features normally found in Systems of Records to client applications in the cloud, specifically web and mobile apps. 

Samples in this specification use JavaScript on the client where the Cloud Data Object is referred to as a JavaScript Data Object (JSDO) and OpenEdge ABL on the server. In reality any client or server language can be used to implement this specification. 

## Contents
## Introduction
Mobile applications often communicate with a server for data and business logic. This specification introduces the _Cloud Data Object_ (CDO), a client-side object that manages transactional data updates and access to server-side business logic.

A _Cloud Data Service_ (CDS) defines the API for one or more server-side resources. Each resource provides access to a logical schema and its related business logic, which for the purposes of this document will be referred to as a Business Entity. The supported schemas are a single table or a dataset which contains one or more tables where the tables may be related. A Business Entity is implemented using a standard set of built-in operations to read and modify data on the backend. A Business Entity can also provide additional (customized) methods, so the resource will also provide access to these non-standard methods.

A CDO provides client access to the data and operations of a single resource. Client code can call methods on a CDO to execute the mapped server-side operations on the backend. The data for these operations is serialized between the Client and the Server. 
For information on the CDO Catalog file, please refer to the document [Cloud Data Object Catalog Specification](https://github.com/Andrey-I/CloudDataObject_API_WIKI/wiki/Cloud-Data-Object-Catalog-Specification).

![](https://raw.githubusercontent.com/Andrey-I/CloudDataObject_API_WIKI/master/images/img1.png)

_The figure above provides an overview of how a CDO accesses a resource which works the same for a given CDO regardless of the type of client or type of backend._


## Classes to support the Cloud Data Object
* [CloudDataRecord](#clouddatarecord-class)
* CloudDataObject
* CloudSession
* request

## CloudDataRecord Class
_CloudDataRecord_ is a record instance for any table stored in the local memory of an associated class instance (CDO).

#### _Properties_

| Member        | Brief description (See also the reference entry)    | 
|-------------|-------------|
| _errorString property |A string value available on the _data_ property of every _CloudDataRecord_ object in CDO memory that is set as part of before-image data for the record and provides descriptive information about any record change error on the server following a Mobile create, update, delete, or submit operation.|
| _id property |A string value available on the data property of every CloudDataRecord object in CDO memory that provides a unique internal ID for the record.|
| data property |The data (field values) for a record associated with a CloudDataRecord object.|

#### _Methods_
| Member | Brief description (See also the reference entry)| 
|-------------|-------------|
| acceptRowChanges( ) method|Accepts changes to the data in CDO memory for a specified
record object.|
|assign() method (CDO class)|Updates field values for the specified CloudDataRecord object in CDO memory.|
|getErrorString() method |Returns any before-image error string in the data of a record object referenced in CDO memory that was set as the result of a Mobile create, update, delete, or submit operation.|
|getId() method|Returns the unique internal ID for the record object referenced in CDO memory.|

#### _Events_
This object has no events.

#### _Example_

The following example assumes that a CDO is referenced by the cdo variable. The example creates a new record object along with a message with credit information using properties of the record object:

```javascript
function addRecord() {
    var record = cdo.add( {Balance: 10000, State: 'MA'} ); 
    alert( 'Record ID: ' + record.getId( ) + ' CreditLimit: ' + record.data.CreditLimit );
}
```

#### _Notes_
Using the add(), find(), findById(), or foreach() method, or the record property, on a given CDO and table reference, a CloudDataRecord instance returns a working record for the table referenced in CDO memory. You can then use properties and methods of the CloudDataRecord to update, delete, or display the specified record from the CDO.

