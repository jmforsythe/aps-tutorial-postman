# Task 3 – Translate to SVF2

> **Important:** These instructions are specific to Postman V10. If you are using a newer version of Postman, you may notice slight differences in the interface or steps. However, the process should remain similar.

To generate zone and space information while translating, you must set a few specific options in the request header and the JSON body. Generating zone and space information can cause translation time to increase. As such, these options must be specified only when you need zone and space information.

To translate a file, you must create a translation job. The job produces a manifest that lists all generated files. It also reports the progress of the translation job as a percentage while the translation job is still in progress.


## Start a translation job

1. In the Postman sidebar, click **Task 3 - Translate to SVF2 > Start a Translation Job**. The request loads.

2. Click the **Body** tab and take note of the JSON payload.

    ![Create Translation Job JSON Payload](../images/tutorial_07_task_3_svf2_start_a_translation_job_01.png "Create Translation Job JSON Payload")

    Note the use of the `generateMasterViews` attribute to instruct APS that it must generate master views for each phase of the Revit model.

3. Click the **Headers** tab and take note of the options that are specified.

   ![Create translation job - Header tab](../images/tutorial_07_task_3_svf2_start_a_translation_job_02.png "Create translation job - Header tab")

   Note the `x-ads-force` header parameter, which has been set to `true`. Setting this header parameter ensures that the derivatives produced by any previous translation job for this source file are removed. This setting is mandatory for generating master views

3. Click **Send**. If the request is successful you should see a screen similar to the following image.

    ![Successful Submission of Translation Job](../images/tutorial_07_task_3_svf2_start_a_translation_job_03.png "Successful Submission of Translation Job")

    Note the `urn` parameter in the JSON response. This parameter contains the URL-safe Base64 encoded URN of the source file. A script in the **Tests** tab, saves this value to a variable named `t7_url_safe_urn_of_source`.

## Check status of translation job

Translation jobs take time to complete. There are two ways to check if the translation job is done:

- Periodically check the status of the translation job.
- Set up a webhook to notify you when the job is done.

For this walkthrough, you will check the status of the translation job. For more information on webhooks, see the [documentation on Model Derivative webhook events](https://aps.autodesk.com/en/docs/webhooks/v1/reference/events/model_derivative_events)

1. In the Postman sidebar, click **Task 3 - Translate to SVF2 > Check Status of Job**. The request loads.

   ![Check Status of Job](../images/tutorial_07_task_3_svf2_check_status_of_translation_job_01.png "Check Status of Job")

   Notice how the URL-safe Base64-encoded URN of the source file is used as a URI parameter (by way of the `t7_url_safe_urn_of_source` variable)

2. Click **Send**. You see a screen similar to the following image.

   ![Successful Job](../images/tutorial_07_task_3_svf2_check_status_of_translation_job_02.png "Successful Job")

   Repeat this step until the `progress` attribute becomes `complete`.

[:rewind:](../readme.md "readme.md") [:arrow_backward:](task-2.md "Previous task") [:arrow_forward:](task-4.md "Next task")
