Request URL: https://uat.citivelocity.com/ReportingWebService/api/v2/packages
Request Method: POST
Status Code: 201 
Remote Address: 23.77.56.80:443
Referrer Policy: no-referrer-when-downgrade

request:
{"clientProfileId":"ASICP","appId":"CLARITY","globalSettings":{"entry":[{"key":"targetFormat","value":{"@type":"string","value":"xlf"}},{"key":"permittedFormats","value":{"@type":"string","value":"xlf"}}]},"assembly":{"report":[{"@reportName":"QA10_CUSTOM_FILTERED1","location":"5e5e0f62aadd4e51c3ae19e8","auxiliaryFilterId":"5e5e0fd4aadd4e51c3ae1a0b"}]},"id":"","name":"aaa111","description":""}

response:
{
   "@type" : "object",
   "dataAsOf" : 1583311711329,
   "expires" : 1583311711329,
   "cacheable" : false,
   "userId" : "UE179116",
   "start" : 0,
   "size" : 0,
   "totalSize" : 0,
   "page" : 0,
   "hasMore" : false,
   "generationMS" : 1636,
   "data" : {
      "@type" : "packageInfoDTO",
      "package" : {
         "name" : "aaa111",
         "itemId" : "CLARITY_ASICP_aaa111",
         "assembly" : {
            "@displayInTOC" : true,
            "@execPriority" : 0,
            "@id" : 0,
            "@includedInOutput" : true,
            "parameters" : {
               "entry" : [ ]
            },
            "report" : [ {
               "@displayInTOC" : true,
               "@execPriority" : 0,
               "@id" : 0,
               "@includedInOutput" : true,
               "@reportName" : "QA10_CUSTOM_FILTERED1",
               "parameters" : {
                  "entry" : [ ]
               },
               "auxiliaryFilterId" : "5e5e0fd4aadd4e51c3ae1a0b",
               "location" : "5e5e0f62aadd4e51c3ae19e8"
            } ]
         },
         "lastUpdated" : "2020-03-04T03:48:29.693-05:00",
         "clientProfileId" : "ASICP",
         "description" : "",
         "userId" : "UE179116",
         "appId" : "CLARITY",
         "globalSettings" : {
            "entry" : [ {
               "key" : "permittedFormats",
               "value" : {
                  "@type" : "string",
                  "value" : "xlf"
               }
            }, {
               "key" : "targetFormat",
               "value" : {
                  "@type" : "string",
                  "value" : "xlf"
               }
            } ]
         },
         "id" : "5e5f6b5d9a89421fea359e6f",
         "deleted" : false
      },
      "auxiliaryFilter" : {
         "id" : "5e5f6b5eab37161c73577755",
         "lastUpdated" : "2020-03-04T03:48:30.491-05:00",
         "packageId" : "5e5f6b5d9a89421fea359e6f",
         "resourceType" : "PACKAGE",
         "citiOwned" : false,
         "userId" : "UE179116",
         "domainName" : {
            "defaultDisplayName" : "Package"
         },
         "reportName" : {
            "defaultDisplayName" : "aaa111"
         },
         "standardReportName" : {
            "defaultDisplayName" : "aaa111"
         },
         "status" : "A",
         "inSchedule" : false,
         "reportType" : "Standard",
         "targetOutputType" : "xlf",
         "parametersType" : "Default",
         "possibleOutputTypes" : [ "XLF" ],
         "appId" : "CLARITY",
         "isDefault" : false,
         "runtimeParams" : [ ]
      }
   }
}
