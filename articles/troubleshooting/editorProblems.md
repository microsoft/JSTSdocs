# Editor Problems

> [!NOTE]
> This page attempts to explain that the "why" as well as the "how", as investigations are
> often more fruitful when the underlying mechanics and the reason for changes are understood.
> Many of the details below may be skipped over if not useful or interesting.

## No IntelliSense, formatting, refactoring, etc.

If the language service for JavaScript & TypeScript doesn't appear to be working at all, basic
installation, configuration, and operation should be verified first.

### Installation

 - Under the VS installation folder, ensure the language service files are present. For a default
 installation of the Enterprise Edition, this would be under
a path similar to `"C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\TypeScript"`
Some files to specificially look for are: `Microsoft.CodeAnalysis.TypeScript.EditorFeatures.dll` and `Microsoft.VisualStudio.LanguageServices.TypeScript.dll`,
 - Ensure the TypeScript SDK is also present. For a default installation, this would be under a path
 similar to `"C:\Program Files (x86)\Microsoft SDKs\TypeScript\2.5"` (Or the `"2.3"` folder, if on an earlier
release than Visual Studio 2017 Update 5).
Some files to look for here are: `build\TypeScript.Tasks.dll` and `tsserver.js`
 - In Visual Studio itself, open the `Help / About` menu, and ensure that `"TypeScript Tools"` is listed.

If an installation failure is still suspected, the setup log files may prove useful. These are located
under the `%TEMP%` folder, with names starting with `"dd_setup_"`. Locate the files with `"TypeScript"`
in the name, and ensure the log contains a line near the end with text such as `"Installation completed successfully"`
or `"Package executed successfully. Return code: 0"`.

If the above and below investigations don't help, try repairing Visual Studio. This is done by launching the `"Visual Studio installer"` application, selecting the `"More"` drop-down, and choosing `"Repair"`.

### Configuration

 - On the Visual Studio menu, open `"Tools / Extensions and Updates"`, and navigate to the `"Installed"` node.
 Search for `"TypeScript"` and ensure the TypeScript Tools are listed, and are not disabled. Do the same for the
 `"Visual Studio extension for TextMate grammars"` (which is used to provide syntax highlighting).

 > [!NOTE]
 > Currently there is also a bug whereby if the `"Azure Functions and Web Jobs Tools"` extension is
 > disabled, then this can break the JavaScript & TypeScript language service. Please check this also.

 - Check the activity log at `"%APPDATA%\Microsoft\VisualStudio\15.0_<ID>\ActivityLog.xml"`. (Open this in
  Internet Explorer for easiest viewing). Look for any errors that mention `"TypeScript"` or `"CodeAnalysis"`.
 - On occassion, the MEF cache can become corrupt. Delete the MEF cache files in
 `"%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_<ID>\ComponentModelCache"`, and then from a Developer Command
 Prompt run `"devenv.exe /updateConfiguration"` to recreate it.
 - If after clearing & recreating the MEF cache as shown above, there are still issues, check the MEF cache error
 log at `"%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_9c557bbb\ComponentModelCache\Microsoft.VisualStudio.Default.err"`.
 The file can contain lots of noise (i.e. benign errors), but can also point to problematic failures.
 - Check that another editor isn't configured to handle JavaScript and TypeScript files, by looking to see if
 there are any custom mappings in `Tools / Options / Text Editor / File Extensions`.
 - Even for a clean install of Visual Studio, some settings may have roamed from other installations, and
 may be the cause of issue. Visual Studio uses a private registry hive, so examining this is a little involved.
     1. Run `regedt32.exe` and select the `HKEY_LOCAL_MACHINE` key.
     2. Select `File / Load Hive...` from the menu and open the file at `%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_<ID>\privateregistry.bin` (where `<ID>` is unique per install). Give
     the new key a name such as `VSprivate`. The settings may now be browsed and edited (with great caution).
     3. To save the data (e.g. for sharing for analysis), select the new `VSprivate` key and choose `File / Export` from
     the menu. Give the file a name such as `"VSprivate.reg"`.
     4. When finished, with the `VSprivate` key selected, choose `File / Unload Hive` from the menu, and
     close the Registry Editor.

### Operation

 - With a JavaScript or TypeScript file open, check Task Manager to see if the Node.js process is running.
 To do this, use `"Ctrl+Shift+Esc"` to open Task Manager, click `"More Details"` on the bottom left (if present),
 go to the `"Details"` tab, right click on the column headings and select the `"Command Line"` column, and
 locate the `node.exe` process which is running the `"tsserver.js"` script. If this is not present, the language
 service is not starting, (or failing), for some reason.
 - You can enable detailed logging by setting an environment variable. From a Developer Command Prompt, set the
 `"TSS_LOG"` environment varaible using something like `"SET TSS_LOG=-file C:\temp\logs\tsserver.log -level verbose"`
 and restart Visual Studio. (Note: The folder given for the log file location should already exist on disk). After
 attempting to edit a JavaScript of TypeScript file, see if this file is present. If it is, look for any errors
 or exceptions that are happening internally.

### Language service is disabled

For performance reasons, there is an upper limit on the amount of JavaScript that can be analyzed for a single solution.
More details are availabe [here](https://aka.ms/jsls-disabled).