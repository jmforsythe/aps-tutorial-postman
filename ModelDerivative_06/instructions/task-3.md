# Task 3 – Translate to SVF2

> **Important:** These instructions are specific to Postman V10. If you are using a newer version of Postman, you may notice slight differences in the interface or steps. However, the process should remain similar.

For the server to extract metadata from a model, you must first translate the model to a viewer-friendly format. Because SVF2 handles larger models better, Autodesk recommends SVF2 over SVF.

To translate a file, you must create a translation job. The job produces a manifest that lists all generated files. It also reports the progress of the translation job as a percentage while the translation job is still in progress.

## Start a translation job

For this task, you use the Base64-encoded URN of the source file. In the previous task, Postman saved this URN to the variable `t6_ossEncodedSourceFileURN`, which you  use in the next request.

1. In the Postman sidebar, click **Translate to SVF2 > Start a Translation Job**. The request loads.

2. Click the **Body** tab and take note of the JSON payload.

    ![Create Translation Job JSON Payload](../images/tutorial_06_task_3_start_a_translation_job_01.png "Create Translation Job JSON Payload")

    Note the name of the Inventor assembly file in the JSON body.

3. Click **Send**. If the request is successful, you should see a screen similar to the following image.

    ![Successful Submission of Translation Job](../images/tutorial_06_task_3_start_a_translation_job_02.png "Successful Submission of Translation Job")

    Note the `urn` parameter in the JSON response. The value of this parameter is the URL-safe Base64 encoded URN of the source file. A script in the **Tests** tab, saves this value to a variable named `t6_url_safe_urn_of_source`.

## Check Status of Translation Job

Translation jobs take time to complete. There are two ways to check if the translation job is done:

- Periodically check the status of the translation job.
- Set up a webhook to notify you when the job is done.

For this walkthrough, you will check the status of the translation job. For more information on webhooks, see the [documentation on Model Derivative webhook events](https://aps.autodesk.com/en/docs/webhooks/v1/reference/events/model_derivative_events)

1. In the Postman sidebar, click **Translate to SVF2 > Check Status of Job**. The request loads.

   ![Check Status of Job](../images/tutorial_06_task_3_check_status_of_job_01.png "Check Status of Job")

   Notice how the URL-safe Base64-encoded URN of the source file is used as a URI parameter (the `t6_url_safe_urn_of_source` variable).

2. Click **Send**. A screen similar to the following image is displayed.

   ![Successful Job](../images/tutorial_06_task_3_check_status_of_job_02.png "Successful Job")

   Repeat this step until the `progress` attribute becomes `complete`, as shown in the image.


[:rewind:](../readme.md "readme.md") [:arrow_backward:](task-2.md "Previous task") [:arrow_forward:](task-4.md "Next task")