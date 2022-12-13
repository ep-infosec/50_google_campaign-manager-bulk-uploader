**This is not an officially supported Google product. It is a reference implementation.**

# Bulk Uploader

This tool is a Python and Angular application to showcase the [Campaign Manager API](https://developers.google.com/doubleclick-advertisers) workflow. It aids in quickly launching a new set of campaigns to Campaign Manager from a simple CSV feed and a set of associated creative assets that are created and launched via the Campaign Manager trafficking APIs.

## Prerequisites

1.  Ensure Python 2.7 is installed.
2.  Download the [Google Cloud SDK](https://cloud.google.com/storage/docs/gsutil_install) for your platform.
3.  Download the [Google App Engine Python SDK](https://cloud.google.com/appengine/downloads) for your platform.
4.  Clone or download this repository to your computer:

        git clone https://github.com/google/campaign-manager-bulk-uploader

5.  For App Engine environment, a vendor lock-in is needed for the third-party tools that are used in the application. Run the following command to install those:

        pip install --no-cache-dir --upgrade --quiet --target lib --requirement requirements.txt

This will save a local copy of all the required third-party tools to a `lib` directory.

## Running the application

Now, you can choose to either run this locally for development purposes, or deploy the application to App Engine.

### For development

1.  Use `dev_appserver.py` to run the application locally:

        dev_appserver.py app.yaml

2.  Visit `http://localhost:8080` to view your application.
3.  You can also view the local App Engine dev console by visiting `http://localhost:8000`.

### Deploying to App Engine

1.  Use `gcloud` to deploy the application, you will need to specify your Project ID:

        gcloud app deploy --project=your-project-id

2.  Now, upload the indexes to Datastore:

        gcloud datastore indexes create index.yaml --project=your-project-id

3.  To view your newly deployed application running, you can open a browser with:

        gcloud app browse --project=your-project-id

On first run, you will be prompted for a username and password by HTTP basic auth. The default username is `admin` and password is `admin`.

### Credentials and settings

Once the application is running we can change a few of the defaults that have been set up by the application's initialization.

1. Open a browser and navigate to your newly locally running or App Engine deployed application. Remember, you may be prompted for a username and password by the basic auth scheme. The default username is `admin` and password is `admin`.
2. To view your application's settings page, click the menu icon (three dots) that is located in the top-right corner of the application.

Now that you are on the settings page, you can choose to change the HTTP basic auth username and password if needed. This is recommended. Take note of any changes.

The settings screen also allows us to set a `Client ID` and `config.json` for the application to use as authorization for the Campaign Manager API and Sheets API calls. To gather these credentials:

1. Create a new project in the [Google API Console](https://console.developers.google.com).
2. Click on the `+ ENABLE APIS AND SERVICES` button.
3. Find and enable the `DCM/DFA Reporting and Trafficking API`.
4. Find and enable the `Google Drive API`.
5. Go back to the APIs & Services dashboard and click the `Credentials` tab.
6. Configure a new `OAuth client ID` by clicking the `Create credentials` button.
7. If needed, configure the consent screen.
8. Choose `Web application` and pick a name for your new application.
9. Add your application's local and App Engine URLs to `Authorized JavaScript origins` and `Authorized redirect URIs`.
10. Download the JSON file, open it in a text editor, and copy its contents into the `config.json` field of the settings page.

## Additional resources

Information on App Engine:

> https://cloud.google.com/appengine

Python on App Engine:

> https://cloud.google.com/appengine/docs/python

Campaign Manager trafficking overview:

> https://developers.google.com/doubleclick-advertisers/guides/trafficking_overview

Running a local server for App Engine applications:

> https://cloud.google.com/appengine/docs/standard/python/tools/using-local-server

## Samples

A sample CSV feed, and its sample assets are in the `samples` directory of this repository.

## Quick deployment with Google Cloud Shell

Click the button below to quickly deploy this application with Google Cloud Shell. Follow the on-screen instructions.

[![Quick deployment with Google Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://console.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fgoogle%2Fcampaign-manager-bulk-uploader&cloudshell_print=GOOGLE_CLOUD_SHELL.txt&cloudshell_tutorial=GOOGLE_CLOUD_SHELL.md)

## The consent screen verification

The credentials you create to authorize requests to both Drive and Campaign Manager's API need to have the consent screen properly configured. To remove the consent screen warnings the application needs to follow steps toward verification. The following messaging can be utilized to help pass verification:

    This application uses `https://www.googleapis.com/auth/dfatrafficking` to handle creative and ad trafficking tasks to Campaign Manager's API. It uses `https://www.googleapis.com/auth/drive.readonly` to access Google Sheets that are then converted to CSV format and saved to this application as a feed that tells the application how to trafficking ads.

    coconate@google.com from Customer Solutions Engineering has built this application as a reference application. See: https://github.com/google/campaign-manager-bulk-uploader

## Authors

Tony Coconate (coconate@google.com) - Google
