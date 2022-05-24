# App Jail
A small script to create the mimimal possible [BastilleBSD](https://bastillebsd.org) jail to run a binary application supervised by daemon.

#### Why no Bastillefile?

Bastillefiles are a great way to provision jails, however Bastille will not apply templates to a stopped jail
and an empty jail cannot be started, so we have to bootstrap it the old fashioned way.

## Usage

Call this script with the full path to your jail and the IP address you want to use.

```
./sh-jail jail_name ip.ad.dr.ess
```

This uses the default `bastille0` shared interface.

You may specify an alternative as the final parameter.

```
./sh-jail jail_name ip.ad.dr.ess bridge0
```

The script will create an empty Bastille jail and set it up with the bare minimum structure and binaries to run a binary supervised by the daemon process.

### Install your app

Copy your app to the jailed /bin folder, you may need copy any supporting files or folders into the jail.

Update the `exec.start` parameter in `jail.conf` to point to your app binary.

### Start the jail

Start the jail and your app will start:

```
bastille start jail_name
```

Check that your app is listening:

```
nc -z ip.ad.dr.ess port
```

If all went well you should see a connection succeeded message, now you need to tell your host or reverse proxy to forward traffic to your jail.


**Note:**
When restarting the jail you may see an error saying the IP is in use, you must remove the jail ip manually:

```
ifconfig bastille0 delete ip.ad.dr.ess
```

For some reason this is not run by `exec.release` in jail.conf.
