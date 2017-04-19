[![Build Status - Master](https://travis-ci.org/IBM-Bluemix/swift-helloworld.svg?branch=master)](https://travis-ci.org/IBM-Bluemix/swift-helloworld)
![macOS](https://img.shields.io/badge/os-macOS-green.svg?style=flat)
![Linux](https://img.shields.io/badge/os-linux-green.svg?style=flat)

# Swift HelloWorld App Overview
This project contains a simple Swift hello world application that can be deployed to Bluemix or run locally on your [macOS](http://www.apple.com/osx/) or [Ubuntu Linux](http://www.ubuntu.com/download) system.  This sample application creates a basic server that returns an HTML greeting to the client.  Please note that this is not a production-ready application.  Instead, it is for educational purposes to learn about the types of applications you can develop using the Swift programming language.

## Application Requirements
To compile and run this sample application on your system, you need to install the [Swift compiler](https://swift.org/download/) for your platform. Please note that the Swift language is evolving and changing rapidly. The latest version of this Swift application works with the `3.1` version of the Swift binaries. You can download this version of the Swift binaries by following this [link](https://swift.org/download/).

If you are interested in manually deploying the application to Bluemix, you'd need to install the Bluemix [command line](http://clis.ng.bluemix.net/ui/home.html) on your system.  Once it is installed, you can use it to [authenticate and access](https://console.ng.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started) your Bluemix organization(s) and spaces.  You can find further details on how to deploy this sample application to Bluemix in the following sections.

## Run the app locally
Once you have installed the Swift compiler and cloned this Git repo, you can now compile and run the application. Go to the root folder of this repo on your system and issue the following command:
```
$ swift build
```
You should see an output similar to the following:
```
Compile Swift Module 'LoggerAPI' (1 sources)
Compile Swift Module 'Socket' (3 sources)
Compile Swift Module 'HeliumLogger' (2 sources)
Compile Swift Module 'Configuration' (7 sources)
Compile Swift Module 'CloudFoundryEnv' (5 sources)
Compile Swift Module 'HerokuConfig' (1 sources)
Compile Swift Module 'CloudFoundryConfig' (2 sources)
Compile Swift Module 'AmazonConfig' (1 sources)
Compile Swift Module 'Utils' (2 sources)
Compile Swift Module 'Server' (1 sources)
Linking ./.build/debug/Server
```
Once the application is successfully compiled, you can run the executable that was generated by the Swift compiler:
```
$ .build/debug/Server
```
You should see an output similar to the following:

```
Server is listening on port: 8080
```

To connect to the server, you can use the browser of your preference (e.g. Firefox, Chrome, etc.) to point to the following URL: `http://<hostname>:8080/`, where `<hostname>` is the hostname or the IP address of the system where you are running the sample app.  If the browser is running on the same system, you can use localhost as the value for the hostname.  After you access the server, the browser should render an HTML page with the following message:

```
Hello from Swift on Linux!
```

Below the greeting message, you should also see an HTML table that displays the environment variables for the app.

## Running the app on Bluemix
### Using the magical button
Click the magical button below to automatically deploy this sample application to Bluemix.

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy)

When automatically deploying to Bluemix, the manifest.yml file [included in the repo] is parsed to obtain the name of the application.  For further details on the structure of the manifest.yml file, see the [Cloud Foundry documentation](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest).

### Using the Bluemix command line
You can also manually deploy the app to Bluemix.  Though not as magical as using the Bluemix button above, manually deploying the app gives you some insights about what is happening behind the scenes.  Remember that you'd need the Bluemix [command line](http://clis.ng.bluemix.net/ui/home.html) installed on your system to deploy the app to Bluemix.

Using the Bluemix command line you can get a list of the buildpacks (along with their versions) that are installed on Bluemix.

```
bluemix cf buildpacks
```

Executing the above command should result in output similar to the following:

```
Getting buildpacks...

buildpack                               position   enabled   locked   filename
liberty-for-java                        1          true      false    buildpack_liberty-for-java_v3.7-20170118-2046.zip
sdk-for-nodejs                          2          true      false    buildpack_sdk-for-nodejs_v3.10-20170119-1146.zip
dotnet-core                             3          true      false    buildpack_dotnet-core_v1.0.10-20170124-1145.zip
swift_buildpack                         4          true      false    buildpack_swift_v2.0.4-20170125-2344.zip
java_buildpack                          5          true      false    java-buildpack-v3.6.zip
ruby_buildpack                          6          true      false    ruby_buildpack-cached-v1.6.16.zip
nodejs_buildpack                        7          true      false    nodejs_buildpack-cached-v1.5.11.zip
go_buildpack                            8          true      false    go_buildpack-cached-v1.7.5.zip
python_buildpack                        9          true      false    python_buildpack-cached-v1.5.5.zip
php_buildpack                           10         true      false    php_buildpack-cached-v4.3.10.zip
xpages_buildpack                        11         true      false    xpages_buildpack_v1.2.2-20170112-1328.zip
staticfile_buildpack                    12         true      false    staticfile_buildpack-cached-v1.3.6.zip
binary_buildpack                        13         true      false    binary_buildpack-cached-v1.0.1.zip
liberty-for-java_v3_4_1-20161030-2241   14         true      false    buildpack_liberty-for-java_v3.4.1-20161030-2241.zip
liberty-for-java_v3_6-20161209-1351     15         true      false    buildpack_liberty-for-java_v3.6-20161209-1351.zip
xpages_buildpack_v1_2_1-20160913-103    16         true      false    xpages_buildpack_v1.2.1-20160913-1038.zip
dotnet-core_v1_0_1-20161005-1225        17         true      false    buildpack_dotnet-core_v1.0.1-20161005-1225.zip
sdk-for-nodejs_v3_9-20161128-1327       18         true      false    buildpack_sdk-for-nodejs_v3.9-20161128-1327.zip
swift_buildpack_v2_0_3-20161217-1748    19         true      false    buildpack_swift_v2.0.3-20161217-1748.zip
```

Looking at the output above, we can see that the Swift buildpack (v2.0.4) is installed on Bluemix.  This will allow a seamless deployment of the starter application to Bluemix. After you have cloned this Git repo, go to its root folder on your system and issue the following command:

```
bluemix app push
```

Executing the Bluemix push command will parse the contents of the `manifest.yml` file and upload the application to Bluemix. The following is example output from executing the `bluemix app push` or `bx app push` command on the Swift `3.0.2` version of this application:

```
Using manifest file /Users/olivieri/git/swift-helloworld/manifest.yml

Creating app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
OK

Creating route swift-helloworld-nontanning-typhoon.stage1.mybluemix.net...
OK

Binding swift-helloworld-nondirectional-schizogamy.eu-gb.mybluemix.net to swift-helloworld...
OK

Uploading swift-helloworld...
Uploading app files from: /Users/olivieri/git/swift-helloworld
Uploading 13.3K, 15 files
Done uploading               
OK

Starting app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
Downloading swift_buildpack...
Downloaded swift_buildpack
Creating container
Successfully created container
Downloading app package...
Downloaded app package (12.9K)
Staging...
-----> Buildpack version 2.0.4
-----> Default supported Swift version is 3.0.2
-----> Configure for apt-get installs...
-----> Writing profile script...
-----> Copying deb files to installation folder...
-----> No Aptfile found.
-----> Getting swift-3.0.2
       Cached swift-3.0.2
-----> Unpacking swift-3.0.2.tar.gz
-----> Getting clang-3.8.0
       Cached clang-3.8.0
-----> Unpacking clang-3.8.0.tar.xz
-----> .ssh directory and config file not found.
-----> Skipping cache restore (new swift signature)
-----> Fetching Swift packages and parsing Package.swift files...
       Cloning https://github.com/IBM-Swift/CloudConfiguration
       HEAD is now at ccaedb3 Merge pull request #13 from IBM-Swift/scaling
       Resolved version: 1.1.2
       Cloning https://github.com/IBM-Swift/Swift-cfenv.git
       HEAD is now at dff3a5d Updated visibility modifiers for certain properties.
       Resolved version: 3.0.0
       Cloning https://github.com/IBM-Swift/LoggerAPI.git
       HEAD is now at 1e6f08e Perf: Use autoclosures to prevent String construction (#18)
       Resolved version: 1.6.0
       Cloning https://github.com/IBM-Swift/Configuration
       HEAD is now at 0b41b36 Change load functions to log errors instead of throwing
       Resolved version: 0.2.0
       Cloning https://github.com/IBM-Swift/BlueSocket.git
       HEAD is now at b0dcf15 Merge pull request #54 from skreutzberger/master
       Resolved version: 0.12.31
       Cloning https://github.com/IBM-Swift/HeliumLogger.git
       HEAD is now at a6ea950 Regenerated API documentation
       Resolved version: 1.6.0
-----> Skipping installation of App Management (debug)
-----> Installing system level dependencies...
-----> Installing curl_7.35.0-1ubuntu2.10_amd64.deb
-----> Installing libcurl3_7.35.0-1ubuntu2.10_amd64.deb
-----> Installing libcurl4-openssl-dev_7.35.0-1ubuntu2.10_amd64.deb
-----> Installing libicu-dev_52.1-3ubuntu0.4_amd64.deb
-----> Installing libssl1.0.0_1.0.1f-1ubuntu2.21_amd64.deb
-----> Installing libssl-dev_1.0.1f-1ubuntu2.21_amd64.deb
-----> Installing openssl_1.0.1f-1ubuntu2.21_amd64.deb
-----> Building Package...
-----> Build config: release
       Compile Swift Module 'LoggerAPI' (1 sources)
       Compile Swift Module 'Socket' (3 sources)
       Compile Swift Module 'HeliumLogger' (2 sources)
       Compile Swift Module 'Configuration' (7 sources)
       Compile Swift Module 'CloudFoundryEnv' (5 sources)
       Compile Swift Module 'HerokuConfig' (1 sources)
       Compile Swift Module 'AmazonConfig' (1 sources)
       Compile Swift Module 'CloudFoundryConfig' (2 sources)
       Compile Swift Module 'Utils' (2 sources)
       Compile Swift Module 'Server' (1 sources)
       Linking ./.build/release/Server
-----> Copying dynamic libraries
-----> Copying binaries to 'bin'
-----> Cleaning up build files
-----> Clearing previous swift cache
-----> Saving cache (default):
-----> - Packages
-----> Optimizing contents of cache folder...
Exit status 0
Staging complete
Uploading droplet, build artifacts cache...
Uploading droplet...
Uploading build artifacts cache...
Uploaded build artifacts cache (2.8M)
Uploaded droplet (82.5M)
Uploading complete
Destroying container
Successfully destroyed container

0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App swift-helloworld was started using this command `Server`

Showing health and status for app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
OK

requested state: started
instances: 1/1
usage: 128M x 1 instances
urls: swift-helloworld-nondirectional-schizogamy.eu-gb.mybluemix.net
last uploaded: Mon Feb 27 17:29:14 UTC 2017
stack: cflinuxfs2
buildpack: swift_buildpack

     state     since                    cpu    memory       disk         details
#0   running   2017-02-27 11:31:38 AM   0.0%   1M of 128M   1.3M of 1G
```

Once the sample application is pushed to Bluemix, you can access it using its route. You can log on to your [Bluemix account](https://console.ng.bluemix.net) to find the route of your application or you can inspect the output from the execution of the `bx app push` command.  The string value (e.g. swift-helloworld.mybluemix.net) shown next to the urls should contain the route.  Use that route as the URL to access the sample server using the browser of your choice.  The browser should render an HTML page with the following message at the top:

```
Hello from Swift on Linux!
```

## Using a different version of Swift on Bluemix for your application
If you look closely at the output above returned by the `bx app push` command, you will notice that `3.0.2` was the Swift version used for compiling and running the sample app on Bluemix.  If you have a Swift application that compiles with a different version of the Swift binaries, say `DEVELOPMENT-SNAPSHOT-2016-08-30-a`, you'd need to update the contents of the `.swift-version` file to:

```
DEVELOPMENT-SNAPSHOT-2016-08-30-a
```

After updating the `.swift-version` file, you can run the `bx app push` command to push your application to Bluemix and use the specified version of the Swift binaries for compiling and running your application.

For a complete list of the Swift versions currently supported and cached by the Swift buildpack for Bluemix, see the buildpack's [manifest](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) file.  If you cannot find the version of the Swift binaries you are looking for in this file, then that version is not currently supported in the cache.

## Running the application in an IBM Container on Bluemix
This sample application can also be run in an IBM Container in Bluemix. For details on how to do this, see [10 Steps To Running a Swift App in an IBM Container](https://developer.ibm.com/swift/2016/02/22/10-steps-to-running-a-swift-app-in-an-ibm-container). In this blog post, you will find the necessary steps for creating an IBM Container that executes this starter application.
