# Victron_DummyMeter_NodeRed
With this DummyMeter you can use every Datasource NodeRed support to publish Data to Victron Dbus (Gridmeter)


# Disclaimer
This Script/Project was forked from RalfZim/venus.dbus-fronius-smartmeter.

![scriptRuns](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/522c7a27-6fe1-40e9-aa71-33005e92a3e4)
![NodeRed](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/12588376-c111-4766-9c85-5725431ff136)
![Cerbo2](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/885eb751-36b4-4003-90c0-a0e6a6f5d7bc)
![Cerbo](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/f834f423-5ec7-4327-b8e6-5f7040843406)

# Installation

    Copy the files to the /data folder on your venus:
        /data/DummyGridMeter/DummyGridMeter.py
        /data/DummyGridMeter/kill_me.sh
        /data/DummyGridMeter/service/run

    Set permissions for files:

    chmod 755 /data/DummyGridMeter/service/run

    chmod 744 /data/DummyGridMeter/kill_me.sh

    Get two files from the velib_python and install them on your venus:
        /data/DummyGridMeter/vedbus.py
        /data/DummyGridMeter/ve_utils.py

    Add a symlink to the file /data/rc.local:

    ln -s /data/DummyGridMeter/service /service/DummyGridMeter


    Am besten dann in crontab den Befehl  ln -s /data/DummyGridMeter/service /service/DummyGridMeter nach reboot ausführen lassen!
    @reboot ln -s "/data/DummyGridMeter/service" "/service/DummyGridMeter"



    You should now be able to see the DummyMeter with the values 0 in the Cerbo.

    Then switch to the NodeRed of the Cerbo: https://venusip:1881.

    Fill the individual data points there with the Node Custom Control. 



# Debugging

You can check the status of the service with svstat:

svstat /service/DummyGridMeter

It will show something like this:

/service/DummyGridMeter: up (pid 10078) 325 seconds

If the number of seconds is always 0 or 1 or any other small number, it means that the service crashes and gets restarted all the time.

When you think that the script crashes, start it directly from the command line:

python /data/DummyGridMeter/DummyGridMeter.py
and see if it throws any error messages.

If the script stops with the message

dbus.exceptions.NameExistsException: Bus name already exists: com.victronenergy.grid"

it means that the service is still running or another service is using that bus name.
Restart the script

If you want to restart the script, for example after changing it, just run the following command:

/data/DummyGridMeter/kill_me.sh

The daemon-tools will restart the scriptwithin a few seconds.

You can use a Hitchi SML Reader or something like that. So need for a EM24 etc anymore.

![20210819_144334](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/5b91f310-6cf5-4709-b5c5-ada52defcfeb)
![20210819_013136](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/ec720004-67e4-43fc-bdb8-916b0cfe3d30)
![Tasmotaview](https://github.com/Marv2190/Victron_DummyMeter_NodeRed/assets/24812585/4fbb9959-a11c-4014-a073-3a488548d9dc)
