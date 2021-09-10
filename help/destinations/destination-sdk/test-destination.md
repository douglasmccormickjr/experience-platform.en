---
description: As part of Destination SDK, Adobe provides developer tools to assist you in configuring and testing your destination. This page describes how to test your destination configuration.
title: Test your destination configuration
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
---
# Test your destination configuration {#developer-tools}

## Overview {#overview}

As part of Destination SDK, Adobe provides developer tools to assist you in configuring and testing your destination. This page describes how to test your destination configuration. For information on how to create a message transformation template, read [Create and test a message transformation template](./create-template.md).

To **test if your destination is configured correctly and to verify the integrity of data flows to your configured destination**, use the *Destination testing tool*. With this tool, you can test your destination configuration by sending messages to your REST API endpoint.

Illustrated below is how testing your destination fits into the [destination configuration workflow](./configure-destination-instructions.md) in Destination SDK:

![Graphic of where the destination testing step fits into the destination configuration workflow](./assets/test-destination-step.png)

## Destination testing tool {#destination-testing-tool}

Use this tool to test your destination configuration by sending messages to the partner endpoint you provided in the [server configuration](./server-and-template-configuration.md).

With this tool, after having configured your destination, you can:
* Test if your destination is configured correctly;
* Verify the integrity of data flows to your configured destination.

### How to use {#how-to-use}

>[!NOTE]
>
>For complete API reference documentation, read [Destination testing API operations](./destination-testing-api.md).

You can make calls to the destination testing API endpoint with or without adding profiles on the request.

If you don't add any profiles on the request, Adobe will generate those internally for you and add them to the request. If you want to generate profiles to use in this request, refer to the [Sample profile generation API reference](./sample-profile-generation-api.md). You need to generate profiles based on the source XDM schema, as shown in the [API reference](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). Note that the source schema is the [union schema](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) of the sandbox that you are using.

The response contains the result of the destination request processing. The request includes three main sections:
* The request generated by Adobe for the destination.
* The response received from your destination.
* The list of profiles sent in the request, whether the profiles were [added by you in the request](./destination-testing-api.md/#test-with-added-profiles), or generated by Adobe if [the body of the destination testing request was empty](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe may generate multiple request and response pairs. For example, if you send 10 profiles to a destination that has a `maxUsersPerRequest` value of 7, there will be one request with 7 profiles and another request with 3 profiles.

**Sample request with profiles parameter in the body**

``` shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'

```

**Sample request without profiles parameter in the body**


``` shell

curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''

```

**Sample response**

Note that the content of the `results.httpCalls` parameter is specific to your REST API.

``` json

{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}

```

For descriptions of the request and response parameters, refer to [Destination testing API operations](./destination-testing-api.md).

## Next steps

After testing your destination and confirming that it is configured correctly, use the [destination publishing API](./destination-publish-api.md) to submit your configuration to Adobe for review.