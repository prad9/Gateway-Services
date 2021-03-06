![IRD logo](../../Images/IRlogo.gif)
![Software Dev](../../Images/SoftwareDev.png)

Interest pay as you earn (IPS) Software Development Kit (SDK) for Investment Income Reporting
=======================================

Key Features:
-------------

- Business use cases
	- [Download and view](III%20-%20IPS%20-%20GWS%20business%20use%20cases.pdf)
	
- Schemas and WSDLS
	- View and download the [common xsd](../Schema%20-%20Common%20III/)
	- View and download the [Return Service common xsd](../Service%20-%20Return%20III/Latest/)
	- View and download the IPS return [xsd](ReturnIPS.v0.xsd) and [wsdl](IPSDevWsdl.wsdl) from this current directory
	
- Returns Service - Investment Income Information 
	- [Download the build pack](../Service%20-%20Return%20III/Latest/Gateway%20Services%20Build%20Pack%20-%20Return%20Service%20-%20III.pdf) to view data definitions of each operation and response status code definitions
	
- Simulating IPS filing operations
    - [Message samples](#message-samples) - positive responses
	- [Requests Matching Logic](#requests-matching-logic)
	
- Identity and Access Services
	- [How to Integrate with OAuth](../../Service%20-%20Identity%20and%20Access/Latest/OAuth%20Authentication%20-%20How%20to%20Integrate.md)
	- [Sample curl commands](../../Service%20-%20Identity%20and%20Access/Latest/OAuth%20Authentication%20-%20How%20to%20Integrate.md) - for testing the OAuth flow
	- [Message Samples](../../Service%20-%20Identity%20and%20Access/Latest/) - OAuth requests and responses
	- [Download the build pack](../../Service%20-%20Identity%20and%20Access/Latest/Build%20pack%20-%20Identity%20and%20Access%20Services.pdf) - for OAuth 2.0 implementation   

Message samples
-----------------

- Simulating IPS Returns Operations:
    - File
		- [request sample](sample%20messages/IPSFileRequest.xml)
        - [positive response sample](sample%20messages/IPSFileResponse.xml)
	- File Amendment
		- [request sample as single filer](sample%20messages/IPSFileRequestUpdate_SingleFiler.xml)
		- [request sample as multi filer](sample%20messages/IPSFileRequestUpdate_MultiFiler.xml)
        - [positive response sample](sample%20messages/IPSFileResponse.xml)
    - RetrieveStatus
	    - [request sample by period end date](sample%20messages/IPSRetrieveStatusRequest_PeriodEndDate.xml)
		- [request sample by submission key](sample%20messages/IPSRetrieveStatusRequest_SubmissionKey.xml)
        - [positive response sample](sample%20messages/IPSRetriveStatusResponse.xml)
    - RetrieveReturn
		- [request sample as single filer](sample%20messages/IPSRetrieveReturnRequest_SingleFiler.xml)
		- [request sample as multi filer](sample%20messages/IPSRetrieveReturnRequest_MultiFiler.xml)
        - [positive response sample](sample%20messages/IPSRetrieveReturnResponse.xml)
            
Requests Matching Logic
-----------------------

- ReadMe Page - (default) port 8080 of root path of Welcome Page
- Authentication mappings - (default) port 8443 of following paths:
    - /ms_oauth/oauth2/endpoints/oauthservice/authorize
    - /oam/server/auth_cred_submit
    - /ms_oauth/oauth2/endpoints/oauthservice/tokens
- Returns Service Mappings - (default) port 8080 of path "/gateway/GWS/Returns":
    - /gateway/GWS/Returns?wsdl - wsdl is not available, returning http 200 only
    - /gateway/GWS/Returns - Authentication validation will be performed at first:
        - if fail then return Authentication Errors
        - if pass then:
            - XML validation will be performed:
                - if fail then return XML Validation Errors
                - if pass then return positive responses
- Default Mapping - Very last matching logic to handle all other requests by returning 404 error when no matching found