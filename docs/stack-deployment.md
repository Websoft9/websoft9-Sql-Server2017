# Deployment

**Deployment is to copy the SqlServer pre-packaged online to your Cloud Server**. For example, after the user subscribe SqlServer on the Cloud Platform, the Platform will automatically copy the SqlServer to the corresponding Cloud Server.

- If SqlServer has been deployed, go to [Initial Installation](/zh/stack-installation.md) to complete the operation.
- If SqlServer is not deployed, you need to deploy SqlServer to your cloud server first.

We offer two deployment SqlServer scenarios (the deployment results are the same):

## Deploy by Image

**Deploy by Image** means starting instance from SqlServer images. **SqlServer Image** provide OS and software environment needed for SqlServer.

For users with experience with cloud servers, Deploy by Image equated with "one-click deployment".

Websoft9 published [SqlServer image](https://apps.websoft9.com/sqlserver) on Cloud Platform, three methods for your deployment:

* When **Create New Instance** , select the SqlServer image as the system boot template.
* When **Subscribe SqlServer** on Marketplace, the system will promote you to create a new instance for this image at the same time.
* When **Re-install OS** for you instance, you can replace the existing image with a SqlServer image.

## Deploy by Script

**Deploy by Script** means running a script on your cloud instance to pull the pre-packages online to your instance and configure it at the same time.

Websoft9 provide the [SqlServer ansbile automation script](https://github.com/Websoft9/ansible-sqlserver) on Github. If you are familiar with Ansible, you can deploy the SqlServer to the instance automaticly.

## Comparison

Although the results of the **deploy by image** are consistent with the results of **deploy by script**, what is the difference between the two deployment methods?

Suggest you read the document [Deploy by Image vs Deploy by Script](https://support.websoft9.com/docs/faq/bz-product.html#deployment-comparison)