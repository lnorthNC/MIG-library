# MIG-library
MIG library 
This project generates all the domain objects for the integration with the MIG healthcare gateway (for talking to primary and social care). 

Build 
To build run as a maven build with the following goals: 'clean package install'.
This will create a jar under the target folder that can be added to the main Nervecentre project lib. 

Domain model
On build it'll generate all the class files we need to send and read responses. So far it only supports the DCR v.2 and Extended patient trace features.
To support more you'll have to update the wrapper.xsd file to include references to the xsds to include. 
The generated files are all added in one big package under com.nervecentre.mig.lib

Updating domain model
To update the domain model simply replace the schema docs and update any references to them in the wrapper. 
When doing so it might be worth checking the XSD alterations section below.
Please update the version number of the jar on update. 

Dependencies 
There are a few included dependencies in the pom, to update them simply change the value in the dependency or the pom property if its filled with a reference to one. 

Other classes
The source also includes some generic helpers for working with MIG. These are all pretty simple, objects to store data to make building and reading neater, some exception classes
and a class with some constants and simple methods for reading and writing out URNs

XSD alterations 
To get this all generating I had to fiddle with a few of the xsds.
The Webservices/MIG.Standard.Message.v1-0.xsd was added. This provides the Message component common to the request and response. 
The response and request xsds in the webservice folder were updated to use the above (to prevent clashes in the generated code a both use the same elements). 
The Payload MIG.PL.PatientTraceService.PatientTrace.v1-0.xsd file was changed PatientTrace.Query was updated to PatientTrace.QueryObj in order to prevent it internally clashing with query elsewhere in the same xsd. 