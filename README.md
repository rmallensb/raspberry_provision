## Provisioning Raspberry Pi 3

### Setup Raspberry Pi

Raspberry Pi provisioning process will disable `pi` user's default password. The `roles/secure_device/files/authorized_keys` file will be copied into `pi` user's `.ssh` directory. Please update the `authorized_keys` file with your public key before provisioning or you will lose access to the device.

#### Tested on

* Raspberry Pi 3 Model B (or newer)
* Raspbian Lite (Stretch)

#### Bootstrap Raspberry Pi

* Login into pi (user: pi, password: raspberry)
* [Enable SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/)
* Jot down IP address of the host

#### Provision Raspberry Pi

* Install ansible on your laptop

    ```
    pip install ansible
    ```

* To configure the raspberry pi without WiFi, run:

    ```
    ansible-playbook -i $IP, provision -k
    ```
    **NOTE: the comma is necessary after the IP so that ansible doesn't check for a file**

* To configure WiFi, please execute the `provision` playbook with the optional command line parameters:

    ```
    ansible-playbook -i $IP, provision -k -e ssid='$SSID' -e psk='$PASSWORD'
    ```

* To configure a custom hostname, please execute the `provision` playbook with the optional command line parameter:

    ```
    ansible-playbook -i $IP, provision -k -e hostname='$HOSTNAME'
    ```

* You need to type in the default password for the first time (raspberry)
* Get coffee or tea or a nice beverage of your choice, this is going to take a while

### Upload Repository

* Copy the repo directory onto Raspberry Pi:

    ```
    ansible-playbook -i $IP, upload
    ```
