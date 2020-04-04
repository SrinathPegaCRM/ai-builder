---
title: Use your prediction model -  AI Builder | Microsoft Docs
description: Describes how to run yor model. Provides information about the schedule feature, which allows you to automatically retrain and run your prediction model at the cadence you choose. 
author: Dean-Haas
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: 
ms.date: 04/02/2020
ms.author: rajvirk
ms.reviewer: v-dehaas
---

# Use your prediction model

After your model is trained and published, it is ready for you to use it. 

## Prediction run

To run your prediction model, just go to the model settings page and select **Run now**.

## Schedule retrain and run

The schedule retrain feature allows you to train prediction models so that performance does not degrade over time. Schedule Run allows end users to infer records based on their own conditions and application use. This helps users to use AI Builder units more effectively.

For example, if your data changes weekly, you can schedule the model to train on a weekly basis. It doesn't make sense to keep inferring the same data every day, so you'd probably schedule weekly inference to align with the training schedule.

Open the **Schedule** screen from model detail page under **Database Sync**. Alternatively, select the **Settings** tab in the menu bar on the model details page.

> [!div class="mx-imgBorder"]
> ![Schedule screen](media/schedule-screen.png "Schedule screen")

When you select on the link under **Database Sync**, the screen below lists schedule options for **Run**. Switch between the **Run** and **Retrain** tabs to view or modify their respective schedules.

> [!div class="mx-imgBorder"]
> ![elect schedule cadence](media/schedule-cadence.png "Select schedule cadence")

You can set the run or retrain cadence to daily, weekly, or mMonthly. If you don't want run prediction or retrain at this time, you might just set it to never. This is useful if you have data issues upstream and do not want impact business processes, or if you just do not want to use the model.

> [!NOTE]  
> When you schedule your model to retrain, it creates a flow to schedule the training. It is a good idea to not update the flow associated to the AI builder retrain schedule. AI Builder manages the flow through the schedule retrain experience.

If you make any changes to the AI Builder **schedule > retrain** settings, the associated flow is replaced with a new one.

## Real-time prediction

In addition to scheduled prediction inferences, AI Builder supports real-time prediction. Although scheduled prediction on a daily cadence may work for some scenarios, there are times when prediction needs to run in real time. Let's say that your retail company wants to know if an order will be delivered on time. If the order creation/fulfillment processes occur in a short time frame, you need the delivery prediction during the fulfillment process. Then, you can decide whether to use a faster shipment type. Real time prediction provides you the information at the time you need it.

AI Builder prediction models created after April 2, 2020 are enabled for real time prediction. A real-time prediction for a model is synchronous call to AI Builder. AI builder is supporting real-time prediction by value, and real-time prediction by reference. The predict operation accepts a single input observation in the request payload and returns the prediction synchronously in the response.

### What about existing models?

Prediction models created before April 2. 2020 don't support real-time prediction. Recreate any models created before this date  to use real-time prediction capability.

### How to use real-time prediction

To use real-time prediction, create a flow in Power Automate. Follow these steps to build a flow:

1. Sign in to [Power Automate](https://flow.microsoft.com/).
1. On the Flows tab, click "New" and select the type. (sample is from "Automated - from blank")
1. Select the desired trigger and then select create.
1. Configure trigger and add any additional steps to prep data.

> [!div class="mx-imgBorder"]
> ![Configure trigger](media/predict-configure-trigger.png "Configure trigger")

1. Add the "Predict" action. 
1. Complete all fields using your data, or data from previous steps in the flow.
1. Update the record with prediction output.

Congratulations! You have created a flow that uses the real-time prediction feature in AI Builder

### Related information

[Train your model](train-model.md)

[Publish your model](publish-model.md)