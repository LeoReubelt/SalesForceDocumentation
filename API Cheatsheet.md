#Rest API
##Needed for all api calls
**Instance Url** - Returned from Auth  
**Header** - ["Authorization": "Bearer \(User Token)"]

##Get Object List  
**URL** - \\(*Instance Url*)//services/data/v35.0/query?q=SELECT+\\(*Comma separated list of fields to fetch*)+FROM+\\(*objectName*)  
**Methdod** - GET  
**Parameters** - None  

##Get Single Object 
**URL** - \\(*Instance Url*)/services/data/v35.0/sobjects/\\(*objectName*)/\\(*id*)  
**Methdod** - GET  
**Parameters** - None 

##Get Count 
**URL** - \\(*Instance Url*)//services/data/v35.0/query?q=SELECT+count()+FROM+\\(*objectName*)   
**Methdod** - GET  
**Parameters** - None   

##Get API Limits 
**URL** - \\(*Instance Url*)//services/data/v35.0/limits   
**Methdod** - GET  
**Parameters** - None  

##Get Image Attachment 
**URL** - \\(*Instance Url*)/services/data/v35.0/sobjects/Attachment/\(*id*)/Body  
**Methdod** - GET  
**Parameters** - None  

##Create Object 
**URL** - \\(*Instance Url*)/services/data/v35.0/sobjects/\\(*objectName*)
**Methdod** - POST  
**Parameters** - Fields as a dictionary  
eg.  ["FirstName":"Lemmy", "LastName":"Kilmister"]

##Create Attachment 
**URL** - \\(*Instance Url*)/services/data/v35.0/sobjects/Attachment
**Methdod** - POST  
**Parameters** - ["Body":fileData, "ParentId":parentObjectID, "Name":fileName]

##Update Object 
**URL** - \\(*Instance Url*)/services/data/v35.0/sobjects/\\(*objectName*)\\(*id*)   
**Methdod** - PATCH   
**Parameters** - Fields as a dictionary  
eg.  ["FirstName":"Lemmy", "LastName":"Kilmister"]
  
##Request Refreshed Token 
**URL** - https://login.salesforce.com//services/oauth2/token HTTP/1.1  
**Methdod** - POST  
**Parameters** - ["grant_type":"refresh_token", "client_id":*Client Id*, "client_secret":*Client Secret*, "refresh_token":*User Token*]
  
    
#Bulk API
##Needed for all api calls
**Instance Url** - Returned from Auth
**Job EndPoint** - \\(*Instance Url*)/services/async/35.0/job

##Create Query Job
**URL** - \(*Job Endpoint*)
**Methdod** - POST  
**Parameters** - None  
**Header** - ["X-SFDC-Session" : *token*, "Content-Type":"application/xml", "charset":"UTF-8"]  
**Body(XML)** -  
 `<?xml version="1.0" encoding="UTF-8"?>`  
`  <jobInfo xmlns="http://www.force.com/2009/06/asyncapi/dataload"> `   
`  <operation>query</operation>`   
`  <object>\(*objectName*)</object>`  
`  <contentType>CSV</contentType> `   
`  </jobInfo>`
  
##Create Query Batch
**URL** - \(*Job Endpoint*)/\(*jobID*)/batch
**Methdod** - POST  
**Parameters** - None  
**Header** - ["X-SFDC-Session" : *token*, "Content-Type":"text/csv", "charset":"UTF-8"]  
**Body(XML)** - SELECT \(*Comma separated list of fields to fetch*) FROM \(*objectName*)


##Check All Batches Status
**URL** - \(*Job Endpoint*)/\(*jobID*)/batch/
**Methdod** - Get  
**Parameters** - None  
**Header** - ["X-SFDC-Session" : *token*]  
**Body(XML)** - None

##Get Result IDs For Batch
**URL** - \(*Job Endpoint*)/\(*jobID*)/batch/\(*batchID*)/result
**Methdod** - Get  
**Parameters** - None  
**Header** - ["X-SFDC-Session" : *token*]  
**Body(XML)** - None

##Get Results For Result Id
**URL** - \(*Job Endpoint*)/\(*jobID*)/batch/\(*batchID*)/result/\(*resultID*)
**Methdod** - Get  
**Parameters** - None  
**Header** - ["X-SFDC-Session" : *token*]  
**Body(XML)** - None