## Google Cloud SDK

This project comes with the following tools and libraries to enable you to easily create and manage resources on Google Cloud Platform:

- App Engine SDKs for:
  - Python
  - Java
  - Go
  - PHP
- Command Line Tools for:
  - Cloud DNS Admin
  - Cloud SQL
  - Big Query
  - Cloud Storage
  - Compute Engine
  - Preview

This project does not provide a managed VM environment.

### Components

The installation of Google Cloud SDK for this project is equivalent to running:

```
cd ~/home/nitrous/
# Install the basic Google Cloud SDK
curl https://sdk.cloud.google.com | bash
# Install additional components
gcloud components update pkg-go pkg-python pkg-java preview app
```

Additional Python, Java and Go packages and Preview components have been pre-installed for you. If you run `gcloud components list` in the console, you can see the full list of pre-installed components.

More information on working with the Google Cloud SDK can be found [here](https://cloud.google.com/sdk/).
