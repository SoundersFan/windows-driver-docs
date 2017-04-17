---
Description: The USBLPM tool monitors the U0/U1/U2/U3 power states of USB 3.0 ports. It can also be used to verify that transitions between U0/U1/U2 occur correctly. In addition, the tool can enable or disable U1 and/or U2 states on all devices in the system.
title: USBLPM
---

# USBLPM


The USBLPM tool monitors the U0/U1/U2/U3 power states of USB 3.0 ports. It can also be used to verify that transitions between U0/U1/U2 occur correctly. In addition, the tool can enable or disable U1 and/or U2 states on all devices in the system.

The tool is included in the [MUTT Software Package](http://msdn.microsoft.com/windows/hardware/jj590752).

## USBLPM


USBLPM is for Windows 8 only and works with the Microsoft USB 3.0 driver stack. The tool does not run as part of the batch files and scripts in this package. The tool is intended for controller, hub, and device companies to monitor the new USB 3.0 power states.

USBLPM runs in **Monitoring**, **Testing**, or **Configuring** mode.

![usb lpm tool](images/fig10-usb-lpm-tool.png)

### Monitoring

This is the default mode when the tool is run without any parameters. In this mode, the tool periodically queries each level of USB 3.0 devices and displays the current U state of the port. By default, the tool runs the query every 500 milliseconds.

In monitoring mode, the period can be changed by this command-line option:

**usblpm /PollingInterval** &lt;*time in milliseconds*&gt;

Where the time value is an integer from 1 through 100000. The **/PollingInterval** option is optional. In general, you should not change the time period.

### Testing

**To test a device or a hub:**

1.  Start the tool.
2.  Change the mode from Monitoring to Testing.
3.  Select the test device.
4.  Click **Start** to start a test run.

The test completes within 10 seconds and the results are displayed to the user.

The test tries different combinations of U0/U1/U2 states and ensures that the test device re-enters U0 successfully. That is done by sending a control transfer which queries the BOS descriptor.

To test a hub, remove all devices attached to it and run the test. Then, attach one or more devices and rerun the test. However, if one of the downstream devices does not correctly support U1/U2, the hub test fails. Therefore, before running the test on the hub, we recommend that you first run the test on devices that are downstream of the hub to ensure that they pass the test.

**Note**  Do not change the device topology while running the test. The behavior of the tool is undefined if the configuration is changed dynamically.

 

### Configuring U1/U2 states

You can use USBLPM to enable or disable U1 and U2 states for all USB devices on the system by running the following command:

**usblpm /enable|/disable U1|U2**

For example, this command disables U2:

**usblpm /disable U2**

In the Configuring mode, the tool does not display any window. The enabling or disabling will persist after the tool has been run.

### Known issues with USBLPM

Before you test selective suspend for a SuperSpeed hub, you should perform the following steps to disable selective suspend.

1.  In Device Manager, right-click on the **SuperSpeed hub** and select **Properties**.
2.  Click the **Power Management** tab.
3.  Uncheck **Allow the computer to turn off this device to save power**.

After you have finished testing with USBLPM, enable selective suspend for the hub by checking **Allow the computer to turn off this device to save power to re-enable selective suspend**.

**Note**  USBLPM currently does not test USB 2.1 LPM.

 

## Related topics


[USB test tools](usb-test-tools.md)

[Tools in the MUTT software package](mutt-software-package.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Busbcon\buses%5D:%20USBLPM%20%20RELEASE:%20%281/26/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



