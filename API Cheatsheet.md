#Rest API
##Needed for all api calls
**Instance Url** - Returned from Auth  
**Header** - "Authorization": "Bearer *\<token>*"

##Get Object List  
**URL** - *\<Instance Url>*//services/data/v35.0/query  
**Methdod** - GET  
**Parameters** - q: SOQL Query  

##Get Single Object 
**URL** - *\<Instance Url>*/services/data/v35.0/sobjects/*\<objectName>*/*\<id>*   
**Methdod** - GET  
**Parameters** - None 

##Get API Limits 
**URL** - *\<Instance Url>*//services/data/v35.0/limits   
**Methdod** - GET  
**Parameters** - None  

##Get Image Attachment 
**URL** - *\<Instance Url>*/services/data/v35.0/sobjects/Attachment/*\<id>*/Body  
**Methdod** - GET  
**Parameters** - None  

##Create Object 
**URL** - *\<Instance Url>*/services/data/v35.0/sobjects/*\<objectName>*
**Methdod** - POST  
**Parameters** - Fields as Field Name and value 


##Create Attachment 
**URL** - *\<Instance Url>*/services/data/v35.0/sobjects/Attachment
**Methdod** - POST  
**Parameters** - {"Body":*\<File Data>*, "ParentId":*\<Parent Object Id>*, "Name": *\<File Name>*}

##Update Object 
**URL** - *\<Instance Url>*/services/data/v35.0/sobjects/*\<objectName>*/*\<id>*   
**Methdod** - PATCH   
**Parameters** - Fields as Field Name and value  
  
##Request Refreshed Token 
**URL** - https://login.salesforce.com//services/oauth2/token HTTP/1.1  
**Methdod** - POST  
**Parameters** - {"grant_type":"refresh_token", "client_id":*\<Client Id>*, "client_secret":*\<Client Secret>*, "refresh_token":*\<token>*}
  
    
#Bulk API
##Needed for all api calls
**Instance Url** - Returned from Auth  
**Job EndPoint** - *\<Instance Url>*/services/async/35.0/job  
**Header** - "X-SFDC-Session" : *\<token>*

##Create Query Job
**URL** - *\<Job Endpoint>*  
**Methdod** - POST  
**Parameters** - None  
**Header** - {"Content-Type":"application/xml", "charset":"UTF-8"}  
**Body** -  
<pre><code>\<?xml version="1.0" encoding="UTF-8"?>
\<jobInfo xmlns="http://www.force.com/2009/06/asyncapi/dataload">
\<operation>query\</operation>
\<object>*\<objectName>*\</object>
\<contentType>CSV\</contentType>
\</jobInfo>
</code></pre>
  
##Create Query Batch
**URL** - *\<Job Endpoint>*/*\<jobID>*/batch  
**Methdod** - POST  
**Parameters** - None  
**Header** - {"Content-Type":"text/csv", "charset":"UTF-8"} 
**Body** - SOQL Query


##Check All Batches Status
**URL** - *\<Job Endpoint>*/*\<jobID>*/batch  
**Methdod** - Get  
**Parameters** - None    
**Body(XML)** - None

##Get Result IDs For Batch
**URL** - *\<Job Endpoint*>/*\<jobID>*/batch/*\<batchID>*/result  
**Methdod** - Get  
**Parameters** - None   
**Body(XML)** - None

##Get Results For Result Id
**URL** - *\<Job Endpoint>*/*\<jobID>*/batch/*\<batchID>*/result/*\<resultID>*
**Methdod** - Get  
**Parameters** - None   
**Body(XML)** - None