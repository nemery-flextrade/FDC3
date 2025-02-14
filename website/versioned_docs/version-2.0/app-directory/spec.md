---
id: version-2.0-spec
sidebar_label: API
title: App Directory API 2.0
original_id: spec
---

View the [full specification](/schemas/2.0/app-directory) in [OpenAPI v3.0](https://www.openapis.org/) format (generated with [ReDoc](https://github.com/Redocly/redoc/)).

## Endpoints

 Endpoint           | Method | Description
 ------------------ | ------ | -----------
 `/v2/apps`         | GET    | Retrieve all application definitions
 `/v2/apps/{appId}` | GET    | Retrieve an application defintion
 `/v1/apps`         | POST   | (deprecated v1 API version) Create a new application definition
 `/v1/apps/{appId}` | GET    | (deprecated v1 API version) Retrieve an application defintion
 `/v1/apps/search`  | GET    | (deprecated v1 API version) Retrieve a list of applications

App Directory implementations MAY extend the list of endpoints to provide other necessary functionality. However, FDC3 Desktop Agent implementations that connect to app direcotries MUST support connection to app directories that only provide the minimum endpoints listed here.

## App Directory Standard Compliance

An FDC3 Standard compliant App Directory implementation **MUST**:

* Implement the specified `/v2` endpoints for retrieving app definitions as defined in the [app directory OpenAPI specification](/schemas/2.0/app-directory#tag/Application/paths/~1v2~1apps~1{appId}/get):
  * `/v2/apps` (GET)
  * `/v2/apps/{appId}` (GET)
* Ensure that `appId` field values assigned to applications are unique within the directory.
* Ensure that app directory records served meet the minimum requirements specified in the [app directory OpenAPI specification](/schemas/2.0/app-directory#tag/Application/paths/~1v2~1apps~1{appId}/get)
* Support retrieval of app directory records via either the raw `appId` (e.g. `myAppId`) or fully-qualified appId (e.g. `myAppId@host.domain.com`) as defined in the [app directory overview](overview#shrinking-the-uri).

An FDC3 Standard compliant App Directory implementation **SHOULD**:

* Support authentication (where required) via the HTTP Authorization header and Bearer authentication schema (implemented via JWT tokens)
* Select any `categories` field values from the recommended list.
* Encourage the use of the `lang` and `localizedVersions` fields in appD records to support localisation and accessibility.

An FDC3 Standard compliant App Directory implementation **MAY**:

* Support filtering of application records returned by user entitlement, where authentication is enabled.
* Implement the deprecated `/v1` endpoints provided for backwards compatability with prior version of the standard:
  * `/v1/apps` (POST)
  * `/v1/apps/{appId}` (GET)
  * `/v1/apps/search` (GET)
* Extend the implementation with additional endpoints.
