+++
title = 'Hid Exception'
date = 2024-08-24T23:25:15+02:00
draft = false
+++


# Troubleshooting QMK Console HID Device Access on Linux

If you're getting the error `HIDException: unable to open device` when trying to open a QMK console on Linux, it's likely due to a lack of permissions to access the HID device. Here’s how you can resolve the issue step-by-step.

## Identify the Vendor and Product IDs

First off, we need to identify the vendor and product IDs of your HID device. You'll usually see this ID in the error message:
```
Could not connect to <vendor-name> <device-name> (:<vendor-id>:<product-id>:1): HIDException: unable to open device
```
Alternatively, you can check this by running the following command in the terminal:
```bash
lsusb
```
Look for an entry that relates to your device—for instance, something labeled "Keyboard" or "Mouse." The result will look something like:
```
Bus 001 Device 005: ID <vendor-id>:<product-id>
```
Note down the vendor and product IDs from this output.

## Create a udev Rule File

Next, we're going to create a udev rule file to grant permissions for your HID device. Open a terminal and type:
```bash
sudo nano /etc/udev/rules.d/70-qmk-hid.rules
```
>The name `70-qmk-hid.rules` follows the udev rules naming convention (`<order>-<name>.rules`). The `70-` ensures the rule is loaded after the default udev rules, and `qmk-hid` indicates that the rule is related to QMK and HID devices. The name can be arbitrary as long as it follows the convention.

## Add the udev Rule

In the file you just created, add the following line. Replace `xxxx` with your vendor ID and `yyyy` with your product ID:
```bash
SUBSYSTEM=="hidraw", ATTRS{idVendor}=="xxxx", ATTRS{idProduct}=="yyyy", TAG+="uaccess"
```

## Apply the udev Rule

1. Save the file and exit the text editor.
2. Reload the udev rules by entering:
    ```bash
    sudo udevadm control --reload-rules
    ```
3. **Unplug and replug your HID device** to apply the new rule. This step is crucial and often overlooked.

After following these steps, you should be able to access the HID device and open the QMK console without running into any permission issues.

## Troubleshooting

If you’re still encountering problems, you can try adding the `MODE="0666"` option to the udev rule. This grants read and write permissions to all users:
```bash
SUBSYSTEM=="hidraw", ATTRS{idVendor}=="xxxx", ATTRS{idProduct}=="yyyy", TAG+="uaccess", MODE="0666"
```
Remember, you'll need to reload the udev rules and reconnect the device after making any changes to the rules file.

By following these steps, you should be able to troubleshoot and resolve the `HIDException` error. If you hit any snags, don't hesitate to search for help in the QMK or Linux communities—they're usually pretty resourceful!