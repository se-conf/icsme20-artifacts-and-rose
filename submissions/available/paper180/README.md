This artifact contains the Deja Vu tool executable that implements the Deja Vu method described in the ICSME 2020 paper titled "Automated Recording and Semantics-Aware Replaying of High-Speed Eye Tracking and Interaction Data to Support Cognitive Studies of Software Engineering Tasks".

The Windows executable binaries for Deja Vu is available in DejaVu.zip and in an archival repository at [https://zenodo.org/record/3976333#.Xy4hqihKh04](https://zenodo.org/record/3976333#.Xy4hqihKh04). Deja Vu works only on Windows as it depends on the iTrace infrastructure and on Win32 for processing OS events.

Instructions on installing Deja Vu, iTrace Core, and iTrace Plugins are provided in INSTALL.md.

## Study Example

The following is an example procedure for an eye tracking study done with iTrace Deja Vu.

During the *Recording* stage, a participant is invited to perform software engineering tasks in a realistic integrated development environment. In this example, we have chosen the Visual Studio IDE. iTrace Core is used for collecting live eye tracking gaze data. Deja Vu record is used to collect this gaze data along with OS computer interactions (mouse and keyboard events).

During the *Replay* stage, after the participant has left, the full study environment is replicated and replayed slowly, using Deja Vu Replay. Because the study is replayed slowly, there is ample time for in-depth gaze analysis computations (even at very high eye tracker frequencies) to be performed with the iTrace Visual Studio plugin (iTraceVS).

The following steps will need to be done in order to record and replay a study session.

1. Recording Stage.
   1. Open Visual Studio. Ctrl+Alt+1 to apply default layout.
   1. Open iTrace Core, choose an eye tracker (or mouse tracker as a proxy to test), and calibrate it by clicking Calibrate.
   1. Open Deja Vu Record. Connect to iTrace Core.
   1. Start Tracking in iTrace Core.
   1. Start recording in Deja Vu Record.
   1. Ask participant to perform study tasks.  This is the point where the participant will perform any task you (as a researcher) have assigned to them such as a bug fix task or summarization task etc...
   1. Once finished, stop recording within Deja Vu Record.
   1. Close Record
   1. Stop tracking in iTrace Core.
1. Replaying Stage.
   1. Open Visual Studio with the iTraceVS plugin.  You can download iTraceVS plugin from [http://www.i-trace.org/downloads/](http://www.i-trace.org/downloads/). A direct link for the iTraceVS plugin is [http://www.sdml.cs.kent.edu/itrace/alpha-0_1_0/iTrace-VS-Plugin.vsix](http://www.sdml.cs.kent.edu/itrace/alpha-0_1_0/iTrace-VS-Plugin.vsix). Documentation is available at [http://www.i-trace.org/vs_doc_home_0-1-0/](http://www.i-trace.org/vs_doc_home_0-1-0/)
   1. Open Deja Vu Replay
   1. Connect iTraceVS to Replay
   1. Apply default layout again in Visual Studio.
   1. Start replay.
   1. Once finished, disconnect plugin.

**Note**
After the replaying stage, the plugins will have generated plugin output of where on the screen the participant was looking (of if you used the mouse as proxy in this test, of where the mouse was pointing because it was used as proxy for your eyes). The output consists of XML files with timing events, (x,y) coordinates, source file names, lines, columns, and any other low level data that we sample from the eye tracker.  Note that they will be blank or a -1 if not available. These XML files are not meant to be read by researchers. Rather, these output files from iTrace Core and iTraceVS can later be input into our post processing tool [iTrace Toolkit](http://www.i-trace.org/downloads/) to generate meaningful output of what source code elements the participant was looking at.

This artifact is only for the Deja Vu tool with the use case of demonstrating how it integrates with the iTrace framework.  The other tools in the iTrace framework can be found on http://www.i-trace.org/downloads/ and are not part of this documentation. 