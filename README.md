# Victron_DummyMeter_NodeRed
With this DummyMeter you can use every Datasource NodeRed support to publish Data to Victron Dbus (Gridmeter)

# Disclaimer
This Script/Project was forked from RalfZim/venus.dbus-fronius-smartmeter.

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