# aas-copy-templates

## Introduction

This Java-based command-line tool provides a simple method to copy templates from one [Adobe Acrobat Sign](https://www.adobe.com/sign.html) account to another.

## Set-Up Instructions

+ Download the latest release of the `aas-copy-templates-<version>.jar` from the [Releases](https://github.com/esign-org-uk/aas-copy-templates/releases) page
+ [Download Java 1.8](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html), if you don't already have it installed on your machine
+ [IP Addresses to add to your allow list](https://helpx.adobe.com/sign/system-requirements.html#IPs), if needed

As the tool makes use of the [Adobe Sign REST API](https://secure.adobesign.com/public/docs/restapi/v6), it is necessary to [provide an integration key](https://helpx.adobe.com/sign/kb/how-to-create-an-integration-key.html) for both your source and target accounts.

To do this, follow the steps below (for each account):

1. Log in to your Acrobat Sign account (as an Administrator)
2. Click **Group** or **Account**, whichever you see at the top
3. Type "Access tokens" in the search field on the left side of the screen
4. Press the "+" icon on the right side
5. Create a key with the scope needed (only `library_read` is required for your source account, and only `library_write` is required for your target account)
6. Double-click the key you just created and copy the FULL text (it goes off-screen to the right so make sure you get it all)
7. Store the `Integration Key` for later use

## Usage

+ Open a command prompt in the directory where you have the JAR file downloaded
+ Execute the following command, replacing:
  + `<version>` with the appropriate value for the release, such as `1.0.0`
  + `<sourceIntegrationKey>` with your saved value from above
  + `<targetIntegrationKey>` with your saved value from above
  + `<outputDirectory>` with the directory which temporary files should be placed
  + `<numberOfTemplates>` (optional, defaults to 1) with the number of templates to be processed

```sh
java -jar aas-copy-templates-<version>.jar <sourceIntegrationKey> <targetIntegrationKey> <outputDirectory> <numberOfTemplates>
```

Assuming you have specified the required parameters correctly, then you should see output similar to that below:

![Sample Output](/images/example-usage.png)

To assist with diagnosing any issues, the documents in the source templates are written to the local filesystem (with a separate directory for each template).

![Sample Output Files](/images/example-output.png)

## Notes

The tool iterates through all the active templates shared with the `sourceIntegrationKey` creator.
If you have a large number of templates present this will take some time.
