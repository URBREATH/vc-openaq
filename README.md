# openaq

> Part of the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui)

## Overview

This repository contains the code for the `openaq` project, which is part of the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui). The `openaq` project is designed to interact with the OpenAQ API to retrieve and display air quality data.

## Features

- Fetches air quality data from the OpenAQ API.
- Processes and displays the data in a user-friendly format.
- Integrates with the VC Map Project for enhanced visualization.

## Installation for developers

Required: **Node 20.18.0**

To install the necessary dependencies, run the following command:

```bash
npm install
```

## Installation for VC Map users

download the build code as \*.tar.gz and install it on your VC Publisher. Or for direct use in Map environment, go to your webserver to your map application and there open the plugins folder. Extract the \*.tar.gz here. In the end you should have a folder **@sensor** in your **plugins** directory and inside that a folder name **openaq**.

### configuration parameters

| Parameter   | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| chartType   | String | add here either 'bar' or 'line' to display measurement values in feature info as line chart or bar chart                                                                                                                                                                                                                                                                                                                               |
| openaqURL   | String | Enter here the proxy URL to OpenAQ API. Since OpenAQ does not allow CORS, you need to proxy the OpenAQ API through your web server and set your API Key there as well. An example of .htaccess is below. [see here: OpenAQ - API Key](https://docs.openaq.org/using-the-api/api-key). As OpenAQ Dev support states: _"... I suggest using a server-side solution which would avoid the cross-origin problem and ensure API security."_ |
|             |
| requestDays | Number | Specify the number of days, used for initially requesting measurements on clicking of a sensor position. Should be one of [1, 2, 3, 4, 5, 6, 7, 14, 30, 60, 90, 120, 180]. Be reminded, that higher numbers > 7 will initially request a lot of data. Means chart creation could take longer on launching the feature info.                                                                                                            |

### Example .htaccess Configuration

```apache
<IfModule mod_rewrite.c>
 RequestHeader set X-API-Key "22767***************************"
 RewriteRule ^(.*)$ https://api.openaq.org/$1 [P]
</IfModule>

Header set Access-Control-Allow-Origin "*"
Header set Access-Control-Allow-Methods "GET, POST, PUT, DELETE, OPTIONS"
```

### app configuration in VC Publisher

add the plugin **@sensor/openaq** to a module of your choice. Open the configuration editor of the plugin and specify the parameters as described in [configuration parameters](#configuration-parameters).

### plugin configuration in map environment on web server

open a module of your choice in directory **configs** and add in section _plugins_ the below json object. If _plugins_ sections does not exist create the plugins sections with **"plugins":[]**

```json
{
  "name": "@sensor/openaq",
  "openaqURL": "https://{your web url}}/openaqproxy/",
  "chartType": "line",
  "requestDays": 7,
  "entry": "src/index.js"
}
```

Adjust the parameters as described in [configuration parameters](#configuration-parameters).

## Usage for developers

To start the application, use the following command:

```bash
npx vcmplugin serve
```

This will launch the application and you can access it in your web browser.

## Contributing

We welcome contributions to the `openaq` project. If you would like to contribute, please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bugfix.
3. Make your changes and commit them with a clear message.
4. Push your changes to your fork.
5. Create a pull request to the main repository.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contact

For any questions or inquiries, please contact the project maintainers through the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui) repository.
