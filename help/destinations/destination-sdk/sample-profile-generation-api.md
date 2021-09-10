---
description: This page lists and describes all the API operations that you can perform using the `/authoring/sample-profiles` API endpoint, to generate sample profiles to use in destination testing.
title: Sample profile generation API operations
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
---
# Sample profile generation API operations {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API endpoint**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

This page lists and describes all the API operations that you can perform using the `/authoring/sample-profiles` API endpoint. 

This API endpoint allows you to generate sample profiles to use: 
* When testing a message transformation template. Read more in [Create and test a message transformation template](./create-template.md).
* When testing if your destination is configured correctly. Read more in [Test your destination configuration](./test-destination.md).

You can generate sample profiles based on either the Adobe XDM source schema, or the target schema supported by your destination. To understand the difference between Adobe XDM source schema and target schema, read the [Message format](./message-format.md) article. 

## Getting started with sample profile generation API operations {#get-started}

Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including how to obtain the required destination authoring permission and required headers.

## Generate sample profiles based on the source schema {#generate-sample-profiles-source-schema}

You can generate sample profiles based on the source schema by making a GET request to the `authoring/sample-profiles/` endpoint and providing the ID of a destination instance that you created based on the destination configuration that you want to test. 

>[!TIP]
>
>* Get the destination instance ID that you should use here from the URL when browsing a connection with your destination.
>![UI image how to get destination instance ID](./assets/get-destination-instance-id.png)

**API format**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Query Parameter | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | The ID of the destination instance based on which you are generating sample profiles. |
| `{COUNT}` | *Optional*. The number of sample profiles that you are generating. The parameter can take values between `1 - 1000`. <br> If the count parameter is not specified, then the default number of generated profiles is determined by the `maxUsersPerRequest` value in the [destination server configuration](./destination-server-api.md#create). If this property is not defined, then Adobe will generate one sample profile. |


**Request**

The following request generates sample profiles, configured by the `{DESTINATION_INSTANCE_ID}` and `{COUNT}` query parameters.

```shell

curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \

```

**Response**

A successful response returns HTTP status 200 with the specified number of sample profiles, with segment membership, identities, and profile attributes that correspond to the source XDM schema.

>[!TIP]
>
> The response returns only segment membership, identities, and profile attributes that are used in the destination instance. Even if your source schema has other fields, these are ignored.

```json

[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]

```

| Property | Description |
| -------- | ----------- |
| `segmentMembership` | A map object which describes the individual’s segment memberships. For more information on `segmentMembership`, read [Segment Membership Details](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | A timestamp of the last time this profile qualified for the segment. |
| `xdm:status` | Indicates whether the segment membership has been realized as part of the current request. The following values are accepted: <ul><li>`existing`: The profile was already part of the segment prior to the request, and continues to maintain its membership.</li><li>`realized`: The profile is entering the segment as part of the current request.</li><li>`exited`: The profile is exiting the segment as part of the current request.</li></ul> |
| `identityMap` | A map-type field that describes the various identity values for an individual, along with their associated namespaces. For more information on `identityMap`, read [Basis of schema composition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |


## Generate sample profiles based on the target schema {#generate-sample-profiles-target-schema}

You can generate sample profiles based on the target schema making a GET request to the `authoring/sample-profiles/` endpoint and providing the destination ID of the destination configuration based on which you are creating your template.

>[!TIP]
>
>* The destination ID that you should use here is the `instanceId` that corresponds to a destination configuration, created using the `/destinations` endpoint. Refer to the [destination configuration API reference](./destination-configuration-api.md#retrieve-list).

**API format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Query Parameter | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | The ID of the destination configuration based on which you are generating sample profiles. |
| `{COUNT}` | *Optional*. The number of sample profiles that you are generating. The parameter can take values between `1 - 1000`. <br> If the count parameter is not specified, then the default number of generated profiles is determined by the `maxUsersPerRequest` value in the [destination server configuration](./destination-server-api.md#create). If this property is not defined, then Adobe will generate one sample profile. |

**Request**

The following request generates sample profiles, configured by the `{DESTINATION_ID}` and `{COUNT}` query parameters.

```shell

curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \

```

**Response**

A successful response returns HTTP status 200 with the specified number of sample profiles, with segment membership, identities, and profile attributes that correspond to the target XDM schema.

```json

[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]

```

## API error handling {#api-error-handling}

Destination SDK API endpoints follow the general Experience Platform API error message principles. Refer to [API status codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) and [request header errors](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in the Platform troubleshooting guide.

## Next steps

After reading this document, you now know how to generate sample profiles to be used when [testing a message transformation template](./create-template.md) or when [testing if your destination is configured correctly](./test-destination.md).