# Task 2 - Upload Source File to OSS

> **Important:** These instructions are specific to Postman V10. If you are using a newer version of Postman, you may notice slight differences in the interface or steps, but the basic procedure should remain similar.

The Object Storage Service (OSS) is a generic Cloud Storage Service that is part of the Data Management API. In this task, you upload a zip file (*Stapler.zip*) containing an Inventor Assembly and Part files to OSS. While you can use any model, we recommend that you use the model we provide. 

## Create a Bucket

In this walkthrough, you will use a Postman environment variable named `ossBucketKey` to hold the Object Key of the Bucket that contains your files in the cloud. If you already have a bucket (from a previous walkthrough), set the `ossBucketKey` variable to the Object Key of that bucket by following step 1, and ignore the rest of the steps in this section.

1. Specify a value for the Bucket Key in the Postman Environment Variable named `ossBucketKey`:

    1. Click the **Environment quick look** icon (the eye icon) on the upper right corner of Postman.

    2. In the **CURRENT VALUE** column, in the **ossBucketKey** row, specify a name for the Bucket that stores your files.

        **Notes:**  
        - The Bucket name needs to be unique throughout the OSS service. If a Bucket with the name you specified already exists, the system returns a `409` conflict error in step 5. If you receive this error, change the value of this variable and try again.

        - The Bucket name must consist of only lower-case characters, numbers 0-9, and the underscore (_) character.

    3. Click the **Environment quick look** icon to hide the variables.

4. In the Postman sidebar, click **Task 2 - Upload Source File to OSS > POST Create a Bucket**. The request loads.

5. Click the **Body** tab, and verify that the `bucketkey` attribute has been set to the variable `ossBucketKey`.

5. Click **Send**. If the request is successful, you should see a screen similar to the following image.

    ![Successful Bucket Creation](../images/tutorial_06_task_1_create_a_bucket.png "Successful Bucket Creation")
    
## Obtain Signed URL

Before you upload a file to OSS, you must obtain a signed upload URL for the file. To obtain a signed upload URL:

1. In the Postman sidebar, click **Task 2 - Upload Source File to OSS > GET Obtain Signed URL**. The request loads.

   Note the use of `ossBucketkey` and `ossSourceFileObjectKey` as URI parameters.

2. Click the **Environment quick look** button and set the Postman environment variable `ossSourceFileObjectKey` to `Stapler.zip`, which you will use as the Object Key.

   ![Set Object key](../images/tutorial_06_task_2_obtain_signed_url_01.png "Set Object Key")

3. Click **Params** tab, and note the `minutesExpiration` parameter is defined as 5 minutes.

   ![Minutes expiration](../images/tutorial_06_task_2_obtain_signed_url_02.png "Minutes expiration")

4. Click **Send**. A script in the **Tests** tab updates the following Postman environment variables:

   | Variable Name              | Description                                                                                 |
   |----------------------------|---------------------------------------------------------------------------------------------|
   | UploadKey | The upload key assigned to the file you want to upload.                                                      |
   | ContentUploadSignedURL | The signed upload URL you must use to upload the zip file                                       |
   
You should see a screen similar to the following image:
   
   ![Signed url](../images/tutorial_06_task_2_obtain_signed_url_03.png "Signed url")
   
## Upload the file

Now that you have obtained a signed upload URL, you can go ahead and upload the zip file to OSS.

1. Download the file *Stapler.zip* from the [*walkthrough_data* folder of this tutorial](../walkthrough_data).

2. In the Postman sidebar, click **Task 2 - Upload Source File to OSS > PUT Upload the File**. The request loads.

   Note the use of `ContentUploadSignedURL` as the URI.

3. Click the **Body** tab.

4. Click **Select File** and select the file *Stapler.zip*, which you downloaded in step 1.

   ![Select file button](../images/tutorial_06_task_2_upload_a_file.png "Select file button")
   
5. Click **Send** to upload the file.


## Finalize Upload

Although you uploaded the source file in one go, it is possible to split a file into chunks and upload the file one chunk at a time. Once all the chunks are uploaded you must inform OSS that the upload operation is complete. Even though you uploaded the file in one go, you must finalize the upload by informing OSS that the upload is done. To finalize the upload:

1. In the Postman sidebar, click **Task 2 - Upload Source File to OSS > POST Finalize Upload**. The request loads.

   Note the use of `ossBucketkey` and `ossSourceFileObjectKey` as URI parameters.

2. Click the **Body** tab, and verify that the `uploadKey` attribute has been set to the variable `UploadKey`.

   ![Body attribute](../images/tutorial_06_task_2_finalize_upload_01.png "Body attribute")

3. Click **Headers** tab. Notice the `Authorization` Header is already defined.

   ![Task headers](../images/tutorial_06_task_2_finalize_upload_02.png "Task headers")

4. Click **Send** to finalize the upload. A script in the **Tests** tab updates the following Postman environment variables:

   | Variable Name              | Description                                                                                 |
   |----------------------------|---------------------------------------------------------------------------------------------|
   | t6_ossSourceFileObjectKey  | Object Key of the source file. Should be `Stapler.zip`.                                         |
   | t6_ossSourceFileURN        | Value of the `objectId` attribute in the JSON response. This is the URN of the source file. |
   | t6_ossEncodedSourceFileURN | The URN of the source file, converted to a Base64-encoded URN.                              |


    You should see a screen similar to the following image:

    ![Finalize upload](../images/tutorial_06_task_2_finalize_upload_03.png "Finalize upload")

[:rewind:](../readme.md "readme.md") [:arrow_backward:](task-1.md "Previous task") [:arrow_forward:](task-3.md "Next task")
