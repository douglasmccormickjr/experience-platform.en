---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;Customer AI
title: Real-time CDP B2B Edition Overview
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Overview of Real-time Customer Data Platform B2B Edition Account
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
hide: yes
hidefromtoc: yes
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
---
# Real-time Customer Data Platform B2B Edition overview

>[!IMPORTANT]
>
>Real-time CDP B2B Edition is currently in beta. The documentation and the functionality are subject to change.

Built on Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition is purpose-built for marketers operating in a business-to-business service model. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

There are improvements to a variety of Adobe Experience Platform capabilities that distinguish Real-time CDP B2B Edition from its B2C counterpart. They include improvements to the Experience Data Model (XDM) for B2B use cases, upgrades to identity resolution and profile segmentation, as well as a custom-built connector and destination for [!DNL Marketo Engage]. The [!DNL Marketo] connector allows B2B brands to connect its industry-leading B2B engagement data with behavioral information in order to nurture leads and enhance account-based marketing operations.

With Real-time CDP B2B Edition, you can:

* Combine data collected from multiple sources into a single view in order to create holistic people and account profiles.
* Enrich, segment, and export all your cross-source data from a centralized store of unified account profiles.
* Manage your data using data governance tools that are available at every step of the centralizing process to ensure that your data conforms to legal regulations and business policies.

More comprehensive details on the improvements made for Real-time CDP B2B Edition are divided into sections below. 

## XDM

Real-time CDP B2B Edition provides several new XDM schema classes, field groups, and relationship types to capture and structure your data specifically for B2B purposes. See the overview on [XDM in Real-time CDP B2B edition](./schemas/b2b.md) for a breakdown of each of these enhancements.

By using preconfigured B2B schemas, you can bring in data in a standardized, actionable structure. Many of the new schema classes map almost directly to those encountered in mainstream CRMs such as [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo], and other B2B data sources. With Real-time CDP B2B Edition, you can bring data from B2B sources into Platform in a straightforward manner and with results that are easy to audit.

These XDM enhancements allow you to better ingest and activate data via B2B-centric sources and destinations, improving data unification and presentation for more various and flexible use cases.

## Identity resolution

After schemas are defined and data has been ingested conforming to those schemas, Real-time CDP B2B Edition identifies source records that represent real-world people and businesses through a powerful, real-time identity resolution system.

The identity resolution system provides the following features:

* Combined B2B and B2C people records
* A multi-level account hierarchy
* Many-to-many, people-to-account connections
* People and account identities are resolved in real-time

The identity resolution system has been expanded to support a more multifaceted classification of people. The system allows for people to be identified as leads in business opportunities as well as customers.

Account records synchronized by the source CRM and connected via multiple paths within the system are merged together by Platform. The system brings together those people associated wth business opportunities and those recorded as customers, but is also able to preserve the distinction between them as an attribute if they are identifiable. 

Matching identifiers are used to link together and merge account records from across multiple systems. Account hierarchies are preserved throughout this process. Differentiators are used scrutinize whether a person is associated with an account or not, and provide the ability to separate them from the account if needed.

## Profiles and segmentation

Once Real-time CDP B2B Edition has ingested data and resolved identities related to people, companies, attributes, and behaviors, that data is used to construct profiles. These profiles can then be segmented into browsable audiences that can then be activated to various destinations.

When implemented correctly, the system tracks people using unique primary identifiers rather than attributes that can change, such as email addresses. This means that when someone changes jobs the system still follows them. The person is still the same entity, but instead they are linked to a new account. This native functionality offers a great vector for expansion into new accounts as the system follows these people as individuals including all of their attributes and behaviors.

## B2B sources

Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using Platform services. The [!DNL Marketo] source allows you to stream B2B data into Platform and keep this data up to date using Platform-connected applications. It supports any number of instances of [!DNL Marketo] (which is beneficial to large companies with multiple instances) and pulls into a single IMS Organization where the data is merged.

>[!NOTE]
>
>The [!DNL Marketo] source is **not** required to use Real-time CDP B2B Edition. 

See the sources in Real-time CDP B2B Edition documentation for more information on Marketo and bringing B2B data into Platform.

<!-- PLACEHOLDER [sources in Real-time CDP B2B Edition](./sources/b2b) -->

## B2B destinations

All Experience Platform destinations such as [!DNL Google], [!DNL Linkedin], or [!DNL Facebook], are available and fully supported by Real-time CDP B2B Edition. There is also a [!DNL Marketo Engage] destination which streams data out of [!DNL Marketo] or out of Platform and makes it available as audiences.

The [!DNL Marketo] destination provides a seamless and quick way to pull information from Experience Platform into [!DNL Marketo]. The destination enables marketers to push segments created in Adobe Experience Platform to [!DNL Marketo]. In [!DNL Marketo], these audiences are then available as static lists.

For companies with more than one CRM, Real-time CDP B2B Edition provides the option to configure destination connectors to separate instances of [!DNL Marketo] or CRM. If required, you can configure destination connectors to each instance and send audiences to each of the CRM instances independently. 

## Next steps

Now that you better understand the benefits for marketers offered by Real-time CDP B2B Edition, and differences between it and Real-time CDP, you can learn about how to apply these features to your own IMS Organization.

<!-- PLACEHOLDER [example use case for Real-time CDP B2B Edition]() -->

To understand how Real-time CDP B2B Edition can benefit your business-to-business service model, see the example use case for Real-time CDP B2B Edition. Alternatively you can refer to the [schemas in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md) documentation for more specific guidance on creating schemas, and defining relationships for essential B2B data entities.