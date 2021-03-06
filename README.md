# Biscoito vs Bolachaha (inspired by Parallel Piper)

This project was developed based on [Parallel Piper](https://github.com/splunk/parallel-piper) project and adjusted to be presented at VTEX Splunk Meetup using a contest againt the correct use name of `Biscoito` vs `Bolacha`.

## Dashboard Sample

Here is the dashboard sample used to demonstrate user usage and iteraction

![image](https://user-images.githubusercontent.com/938045/65654486-64090000-dfef-11e9-9c30-dbd8d5b51a2d.png)

## Build

1) Install NPM deps
```
npm install
```

2) Run webpack build

Run `build.sh` in the source directory.

```
$ sh build.sh
```

The following environment variables need to be defined for specifying the Splunk 
server running the HTTP input. 

- `PP_SPLUNK_HOST` (default is `"localhost"`)
- `PP_SPLUNK_PORT` (default is `8088`)
- `PP_SPLUNK_SSL` (default is `false`)
- `PP_SPLUNK_TOKEN` (required) token for the HTTP input (See Splunk Setup below.)

Then run the webpack build:

```
PP_SPLUNK_TOKEN=cafecafecafecafe \
PP_SPLUNK_HOST=my.host.com \
./node_modules/webpack/bin/webpack.js -p
```

This generates all the page, JS and all the static content in the `dist` directory. Simply
copy it to a webserver-exposed folder.

# Splunk Setup

To enable the splunk HTTP Event Collector and create a token follow the instructions posted here:
	
http://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector 


Once you have your token make sure you update your `PP_SPLUNK_TOKEN` in the previous section.

Parallel Piper makes use of cross-origin resource sharing which requires you to enable CORS on the HTTP event collector.  

To do this edit your `$SPLUNK_HOME/etc/system/local/server.conf` and add the following.

```
[httpServer]
crossOriginSharingPolicy = *
```

If you wish to restrict cors calls to a specific domain replace the asterix with the domain name your are hosting 
Parallel Piper on. 

# Deploy on gh-pages
 - just run `npm run deploy`
