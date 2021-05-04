---
title: Create a test profile
description: Learn how to create a test profile
---
# Create test profiles {#create-test-profiles}

![](../assets/do-not-localize/badge.png)

Test profiles are required when using the test mode in a journey. You can either turn an [existing profile](../building-journeys/creating-test-profiles.md#turning-profile-into-test) into a test profile, or [create a test profile](../building-journeys/creating-test-profiles.md#create-test-profiles-csv). To learn how to use the test mode, refer to [this section](../building-journeys/testing-the-journey.md).

There are different ways to create a test profile in Adobe Experience Platform. In this documentation, we focus on two methods: uploading a [csv file](../building-journeys/creating-test-profiles.md#create-test-profiles-csv) and using [API calls](../building-journeys/creating-test-profiles.md#create-test-profiles-api). You can also upload a json file in a dataset, refer to the [Data Ingestion documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/tutorials/ingest-batch-data.html#add-data-to-dataset).

Creating a test profile is similar to creating regular profiles in Adobe Experience Platform. For more information, refer to the [Real-time Customer Profile documentation](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html).

## Prerequisites{#test-profile-prerequisites}

In order to be able to create profiles, you first need to create a schema and a dataset in Adobe Experience Platform.

First, you need to **create a schema**. Follow these steps:

1. In Adobe Experience Platform, click **Schemas**, in the left menu.
    ![](../assets/test-profiles-0.png)
1. Click **Create schema**, in the top right, then select a schema type, for example **XDM Individual Profile**.
    ![](../assets/test-profiles-1.png)
1. Choose a name for your schema.
1. In the **Mixins** section, click **Add**. 
    ![](../assets/test-profiles-1-bis.png)
1. Select the appropriate mixins. Make sure you add the **Profile test details** mixin. Click **Add mixin**.
    ![](../assets/test-profiles-1-ter.png)
    The list of mixins is displayed on the schema overview screen.
    ![](../assets/test-profiles-2.png)
1. In the list of fields, click on the field that you want to define as the primary identity.
    ![](../assets/test-profiles-3.png)
1. In the **Field properties** right panel, check the **Identity** and **Primary Identity** options and select a namespace. If you want the primary identity to be an email address, choose the **Email** namespace. Click **Apply**.
    ![](../assets/test-profiles-4.png)
1. Select the schema and enable the **Profile** option in the **Schema properties**.
    ![](../assets/test-profiles-5.png) 
1. Click **Save**.

>[!NOTE]
>
>For more information on schema creation, refer to the [XDM documentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#prerequisites).

Then you need to **create the dataset** in which the profiles will be imported. Follow these steps:

1. In Adobe Experience Platform, click **Datasets**, in the left menu, then click **Create dataset**.
    ![](../assets/test-profiles-6.png) 
1. Choose **Create dataset from schema**.
    ![](../assets/test-profiles-7.png) 
1. Select the previously created schema then click **Next**.
    ![](../assets/test-profiles-8.png) 
1. Choose a name then click **Finish**.
    ![](../assets/test-profiles-9.png) 
1. Enable the **Profile** option. 
    ![](../assets/test-profiles-10.png) 

>[!NOTE]
>
> For more information on dataset creation, refer to the [Catalog Service documentation](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html#getting-started).

## Turning a profile into a test profile{#turning-profile-into-test}

You can turn an existing profile into a test profile. In Adobe Experience Platform, you can update profiles attributes in the same way as when you create a profile. 

A simpler way to do this is by using an **Update profile** action activity in a journey and change the testProfile boolean field from false to true.

Your journey will be composed of a **Read segment** and an **Update profile** activity. You first need to create a segment targeting the profiles you want to turn into test profiles. 

>[!NOTE]
>
> Since you will be updating the **testProfile** field, the chosen profiles must include this field. The related schema must have the **Profile test details** mixin. See [this section](../building-journeys/creating-test-profiles.md#test-profiles-prerequisites).

1. In Journey Optimizer, click **Segments** from the left menu, then **Create segment**, in the top right.
    ![](../assets/test-profiles-22.png) 
1. Define a name for your segment and build the segment: choose the field(s) and value(s) to target the profiles you want.
    ![](../assets/test-profiles-23.png) 
1. Click **Save** and check that the profiles are correctly targeted by the segment.
    ![](../assets/test-profiles-24.png) 

    >[!NOTE]
    >
    > Segment calculation can take some time. Learn more on segments in [this section](../segment/about-segments.md).

1. Now create a new journey and start with a **Read segment** orchestration activity.
1. Choose the previously created segment and the namespace that your profiles use.
    ![](../assets/test-profiles-25.png)
1. Add an **Update profile** action activity. 
1. Select the schema, the **testProfiles** field, the dataset and set the value to "true".
    ![](../assets/test-profiles-26.png)
1. Add an **End** activity and click **Publish**.
    ![](../assets/test-profiles-27.png)
1. In Adobe Experience Platform, check that the profiles have been correctly updated.
    ![](../assets/test-profiles-28.png)

    >[!NOTE]
    >
    > For more information on the **Update profile** activity, refer to [this section](../building-journeys/update-profiles.md).

## Creating a test profile using a csv file{#create-test-profiles-csv}

In Adobe Experience Platform, you can create profiles by uploading a csv file containing the different profile fields into your dataset. This is the easiest method.

1. Create a simple csv file using a spreadsheet software.
1. Add one column for each needed field. Make sure you add the primary identity field ("personID" in our example above) and the "testProfile" field set to "true". 
    ![](../assets/test-profiles-11.png) 
1. Add one line per profile and fill in the values for each field. 
    ![](../assets/test-profiles-12.png) 
1. Save the spreadsheet as a csv file. Make sure commas are used as separators.
1. In Adobe Experience Platform, click **Workflows**, in the left menu. 
    ![](../assets/test-profiles-14.png) 
1. Choose **Map CSV to XDM schema**, then click **Launch**.
    ![](../assets/test-profiles-16.png) 
1. Select the dataset you want to import the profiles into. Click **Next**.
    ![](../assets/test-profiles-17.png) 
1. Click **Choose files** and select your csv file. When the file is uploaded, click **Next**.
    ![](../assets/test-profiles-18.png) 
1. Map the source csv fields to the schema fields, then click **Finish**.
    ![](../assets/test-profiles-19.png) 
1. The data import begins. The status will move from **Processing** to **Success**. Click **Preview data set**, in the top right.
    ![](../assets/test-profiles-20.png)
1. Check that the test profiles have been correctly added.
    ![](../assets/test-profiles-21.png)

Your test profiles are added and can now be used when testing a journey. Refer to [this section](../building-journeys/testing-the-journey.md).
>[!NOTE]
>
> For more information on csv imports, refer to the [Data Ingestion documentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/tutorials/map-a-csv-file.html#tutorials).

## Creating test profiles using API calls{#create-test-profiles-api}

You can also create test profiles via API calls. Learn more in this [page](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html).

You must use a Profile schema that contains the "Profile test details" mixin. The testProfile flag is part of this mixin.

When creating a profile, make sure you pass the value: testProfile = true.

Note that you can also update an existing profile to change its testProfile flag to "true".

Here is an example of an API call to create a test profile:

```
curl -X POST \
'https://dcs.adobedc.net/collection/xxxxxxxxxxxxxx' \
-H 'Cache-Control: no-cache' \
-H 'Content-Type: application/json' \
-H 'Postman-Token: xxxxx' \
-H 'cache-control: no-cache' \
-H 'x-api-key: xxxxx' \
-H 'x-gw-ims-org-id: xxxxx' \
-d '{
"header": {
"msgType": "xdmEntityCreate",
"msgId": "xxxxx",
"msgVersion": "xxxxx",
"xactionid":"xxxxx",
"datasetId": "xxxxx",
"imsOrgId": "xxxxx",
"source": {
"name": "Postman"
},
"schemaRef": {
"id": "https://example.adobe.com/mobile/schemas/xxxxx",
"contentType": "application/vnd.adobe.xed-full+json;version=1"
}
},
"body": {
"xdmMeta": {
"schemaRef": {
"contentType": "application/vnd.adobe.xed-full+json;version=1"
}
},
"xdmEntity": {
"_id": "xxxxx",
"_mobile":{
"ECID": "xxxxx"
},
"testProfile":true
}
}
}'
```