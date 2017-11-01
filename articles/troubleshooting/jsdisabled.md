# The JavaScript language service disabled warning

You may get a bar along the top of the editor with text that reads "The JavaScript language 
service has been disabled for the following project(s)", as shown below.

<img src="../../images/jslsdisabledpopup.png" width="860px"/>

The JavaScript language service is disabled when it reaches a threshold on the amount of JavaScript
code it tries to analyze. (By default, 20MB across the solution).

This limit is enabled by default to reduce the amount of memory and CPU that the JavaScript language
service in Visual Studio 2017 might consume, as loading high volumes of JavaScript code is often
unintentional, and can lead to a poor experience. 

> [!WARNING]
> The project name given in the alert is the project that happened to be being processed when
> the limit was hit. While this is most often the project that is causing problems, it is not
> guaranteed to be so.

