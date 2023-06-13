---
title:  Activity monitoring (preview)
description: Learn how to monitor the activity or consumption of your AI models.
author: jekom1
contributors:
  - jekom1
  - v-aangie
ms.topic: conceptual
ms.custom: 
ms.date: 05/31/2023
ms.author: jelenak
ms.reviewer: angieandrews
---

# Monitor model activity (preview)

[!INCLUDE[cc-beta-prerelease-disclaimer](./includes/cc-beta-prerelease-disclaimer.md)]

As you use your AI models, you might need to access data to monitor the activity or consumption of your AI models.

> [!IMPORTANT]
>
> - [!INCLUDE[cc_preview_features_definition](includes/cc-preview-features-definition.md)]
>
> - This feature might not be available in your region yet.

The **AI Builder activity** section of the Power Automate portal provides tables and graphs to monitor AI models and the data processed by the AI models, as well as track AI credits consumption.

:::image type="content" source="media/activity-monitoring/activity-monitoring-legend.png" alt-text="Screenshot of the AI Builder activity (preview) screen.":::

Legend:

1. **Data processed:** Contains the text input of the AI model predict action for text processing models, **Image**, or **Document** for other models.
1. **Data type:** Data type processed by the AI model: **Text**, **Jpeg**, **Png**, **Bmp**, **Pdf**, or **Unknown**.
1. **Date:** Processing date.
1. **Model:** The name of the AI model used. If the model has been deleted, you see **Deleted**.
1. **Status:** Processing status: **Processing**, **Processed**, or **Failed**.
1. **Processed by:** Name of the person who did the predict. This is typically the Power Automate flow owner, or the person who executed the Power Apps app.
1. **AI Credits:** Number of credits consumed for this AI predict action.

## View AI Builder activity

The **AI Builder activity** screen contains AI models activity, including activity generated in [Power Apps](/power-apps/powerapps-overview).

1. Sign in to [Power Automate](https://make.powerautomate.com).
1. On the left navigation panel, select **Monitor** > **AI Builder activity (preview)**.
1. (Optional) Customize how the data appears by applying a filter for timeframe or by model. Do this by selecting the relevant heading.

    By default, data displays for all AI models for the last seven (7) days.

1. (Optional) To display more data, select **See more**.

## Monitoring data for makers and admins

The AI Builder activity section is helpful for makers who want to get monitoring on their AI models usage. It's also helpful for environment admins who want to monitor all activity in an environment.

> [!NOTE]
>
>- The monitoring data is stored in the **AI Event** table in your Microsoft Dataverse. It persists in the table even if the model/flow/app are deleted.
>
>- The **AI Event** Dataverse table contains input of the AI model predict actions for text scenarios only.

The data you can display depends on your role.

|Role |What you can display |
|---------|---------|
|System Administrator     |  All activity for all AI models.       |
|System Customizer     | All activity for all AI models.        |
|Basic User    |Only your own activity of the AI models you have access to.     |
|Environment Maker     |  Only your own activity of the AI models you have access to.          |

## Manage AI Builder activity monitoring data

Effective management of historical data generated by your Power Automate Flows, Power Apps or other Power Platform products can ensure that your Dataverse environments remain efficient and cost-effective. By implementing data retention policies and utilizing features like [bulk record deletion of Dataverse](/power-platform/admin/delete-bulk-records) and the [Power Platform admin center](https://admin.powerplatform.microsoft.com/), you can proactively manage the accumulation of historical data.

To create bulk-delete jobs in Dataverse, you need to have the **Bulk Delete** privilege in at least one of the roles that have been assigned to you.

Later in this article, you learn how to purge historical AI Builder activity monitoring data from your environment using Dataverse's built-in bulk-delete feature. This feature allows you to quickly and easily [remove large amounts of data](/power-apps/developer/data-platform/delete-data-bulk) from your environment in compliance with your specific data retention policies. This ensures efficient data storage and performance management. In addition to ad-hoc bulk-delete jobs, you can schedule recurrent bulk-delete jobs that will find and delete records in a table that are, for example, `OlderThanXDays`.

You'll also learn how to:
- Identify the AI Builder activity monitoring data that could be purged.
- Create a bulk delete job to delete the data.

> [!CAUTION]
> 
> When you delete Dataverse data, it's permanently deleted from your environment. There's no way to recover individual records once they've been deleted.

### Export a Dataverse table

The following table shows an AI Builder activity monitoring Dataverse table with potentially large data volumes/

|Display name|System name|Details|
|--------|--------|--------|
|AI Event|Msdyn_aievent|The **AI event** table stores activity data about AI models activity (*predicts*), such as the processed data type, processed data info for text scenarios, processing date, processing status, and credits consumed.|

As the data is stored in your **AI Event** Dataverse table, you can export it in a CSV format. To learn how to export, go to [Export data](/power-apps/maker/data-platform/data-platform-import-export#export-data0).

:::image type="content" source="media/activity-monitoring/export.png" alt-text="Screenshot of how to export data from a Dataverse table.":::

### Delete AI Builder activity monitoring data

To delete AI Builder activity monitoring data, you need to create a bulk-delete job. To bulk-delete data in Dataverse, follow the steps in this section.

Before performing bulk delete operations, thoroughly test and review your filter results. Bulk-delete operations are irreversible.

1. Sign in to the [Power Platform admin center](https://admin.powerplatform.microsoft.com/).
1. On the left navigation pane, select **Environments** > select your environment > **Settings** (on the top menu bar).
1. Select **Data management** > **Bulk deletion**.
1. From the **All Bulk Deletion System Jobs** grid, select **New** on the command bar. This will open the **Bulk Deletion Wizard**, which allows you to define a query for the records you want deleted.
1. Select **Next**.
1. In the **Look for** list, select the **AI Events** table.
1. In the search criteria area, add the filter that should return the records that you want to be deleted. Here’s an example that finds all AI Builder models activity that is older than six (6) months:

    :::image type="content" source="media/activity-monitoring/search.png" alt-text="Screenshot of search criteria.":::

1. Select **Next**.
1. In the **Name** text box, type a name for the bulk deletion job (for example, **Bulk-delete of AI models monitoring data older than 6 months**).
1. In the **At scheduled time** section, select a date and time for the job start time. Select a time when users aren't typically online.
1. Select the **Run this job after every** checkbox.
1. In the **days** list, select the frequency you want the job to run.
1. If you want a notification e-mail sent, select the **Send an email to me (email@domain.com) when this job is finished** checkbox.
1. Select **Next**.
1. In the **Review and Submit Bulk Deletion Details** screen, review the bulk deletion job, and then select **Submit** to create the recurring job.



