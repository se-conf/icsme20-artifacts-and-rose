Deja Vu is built to interface with the [iTrace](http://www.i-trace.org/) eye tracking community infrastructure. iTrace Core is optional, but is required for collecting eye tracking gaze data.

## Installing iTrace Core and Plugins
iTrace Core and Plugins can be acquired from the iTrace website http://www.i-trace.org/downloads/. Installation files and instructions can be found on the website.  For this example you will need iTrace Core and iTrace Visual Studio Plugins to follow along with the example in the Readme. However, the same process is followed if you choose to use the iTrace Eclipse plugin.

## Installing Deja Vu
To run Deja Vu, download the zip file and extract it. Deja Vu is split into two applications, DejaVu Record.exe (which performs the Recording stage) and DejaVu Replay.exe (which performs the Replaying stage). Both applications are contained within the zip.

## Simple Installation Test
The simplest way to test your Deja Vu installation is to:
1. Make sure the computer is running a single monitor setup.
1. Run Record.exe
   1. Click the Record button. Deja Vu recording process has started.
   1. Interact with the computer by moving the mouse around.
   1. End the recording by clicking the Record button again.
1. Run Replay.exe
   1. Click on the Replay button
   1. Deja Vu should now be replaying the same computer interactions, slower.
   1. Once replay is done, close out of Replay.

## Pre requisites (if needed)
If Deja Vu does not run, it may be because your computer is missing the necessary .NET Redistributables. Deja Vu is built with .NET version 4.6.1, which can be acquired from [https://dotnet.microsoft.com/download/dotnet-framework/net461](https://dotnet.microsoft.com/download/dotnet-framework/net461) .
