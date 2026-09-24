I don’t have a configured repository to edit, so here’s a copy-ready rewrite based on the README text you provided.

# openaq

**Provided by:** VC Map Project (virtualcitySYSTEMS)

## Description

`openaq` is a plugin for the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui) that retrieves air quality measurements from the OpenAQ API and displays them in feature information charts. It supports line and bar charts.

## Installation Prerequisites

- **For development:** Node.js `20.18.0`.
- **For deployment:** VC Publisher or a deployed VC Map application.
- An OpenAQ API proxy configured on your web server. OpenAQ does not allow direct cross-origin requests, so the plugin needs to access the API through a server-side proxy.

## Installation Instructions

1. Obtain the built `*.tar.gz` package.
2. Install it using VC Publisher, or for direct use in a map application, extract it into the application’s `plugins` directory. The resulting path should be `plugins/@sensor/openaq`.
3. Add the `@sensor/openaq` plugin to a module and configure it as described under [Additional Information](#additional-information).

## Built Image Registry

Not specified in the current README.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## External technical resources

- [OpenAQ API](https://api.openaq.org/)
- [OpenAQ API key documentation](https://docs.openaq.org/using-the-api/api-key)

## User Guide References

No user guide or FAQ links were included in the current README.

## Additional Information

### Configuration parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `chartType` | String | Set to `bar` or `line` to display measurement values as a bar or line chart in feature information. |
| `openaqURL` | String | URL of the server-side proxy to the OpenAQ API. Configure the API key on the proxy server, not in the client-side plugin. |
| `requestDays` | Number | Number of days of measurements to request when a sensor position is clicked. Supported values: `1`, `2`, `3`, `4`, `5`, `6`, `7`, `14`, `30`, `60`, `90`, `120`, and `180`. Larger values can result in more data being requested and slower chart loading. |

### Example `.htaccess` proxy configuration

Replace the placeholder API key with your own. Configure the proxy on your web server; do not expose the key in the map application’s client-side configuration.

```apache
<IfModule mod_rewrite.c>
 RequestHeader set X-API-Key "YOUR_OPENAQ_API_KEY"
 RewriteRule ^(.*)$ https://api.openaq.org/$1 [P]
</IfModule>

Header set Access-Control-Allow-Origin "*"
Header set Access-Control-Allow-Methods "GET, POST, PUT, DELETE, OPTIONS"
```

### Configuration in VC Publisher

Add the `@sensor/openaq` plugin to a module of your choice. Open the plugin’s configuration editor and set the parameters described in [Configuration parameters](#configuration-parameters).

### Configuration in a map application

In the web server’s `configs` directory, open a module configuration and add the plugin object to its `plugins` array. If the `plugins` section does not exist, create it as `"plugins": []`.

```json
{
  "name": "@sensor/openaq",
  "openaqURL": "https://your-web-host/openaqproxy/",
  "chartType": "line",
  "requestDays": 7,
  "entry": "src/index.js"
}
```

Adjust the values as described in [Configuration parameters](#configuration-parameters).

### Developer setup and usage

Install the dependencies:

```bash
npm install
```

Start the development server:

```bash
npx vcmplugin serve
```

### Contributing

Contributions are welcome:

1. Fork the repository.
2. Create a branch for your feature or bug fix.
3. Make your changes and commit them with a clear message.
4. Push the branch to your fork.
5. Open a pull request.

### Contact

For questions or inquiries, contact the project maintainers through the [VC Map Project](https://github.com/virtualcitySYSTEMS/map-ui) repository.
