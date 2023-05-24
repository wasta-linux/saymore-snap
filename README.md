# saymore-snap

Install SayMore (via WINE) on a snap-enabled system.

This needs to be installed with the `--devmode` flag because of how snap's
confinement works, and how SayMore's Welcome Screen and Project Window handle
switching back and forth to each other. Devmode also means that there will
be no automatic updates. All updates have to be done manually, always
remembering to use the `--devmode` flag.

## Installation

Open a terminal, copy/paste this command, then hit [Enter]:
```bash
snap install saymore-unofficial --devmode
```
On many systems the command will pop up a window asking for your user password.
But on some systems you may need to use sudo instead to elevate permissions:
```bash
sudo snap install saymore-unofficial --devmode
```
After installation (which will likely require up to 1 GB of downloading) you
will be able to start SayMore from your normal app menu.

Sometimes the installation of .NET (dotnet462) hangs. See **Troubleshooting** below for tips.

## Updating

```bash
snap refresh saymore-unofficial --devmode
```
or
```bash
sudo snap refresh saymore-unofficial --devmode
```

## Troubleshooting

### Hung installation

See if any processes have hung by using the `watch-procs` subcommand in a terminal:
```bash
saymore-unofficial.watch-procs
```
If none of the processes show higher than, say, 10% CPU usage for more than a couple of minutes,
then it has probably stalled.
- If you started the installer in a terminal you can use Ctrl+C to stop it.
- Regardless, you will probably need to use the terminal command `saymore-unofficial.kill-procs`
to kill the background processes that will likely still be running.
- Then start the app again (from the apps menu or in a terminal) and it will continue installation
where it left off.

### SayMore doesn't start

Maybe the installation got corrupted, especially if it hung during the initial install and you
had to start it again.
- Fully remove the WINE installation with the command `saymore-unofficial.remove-wine-prefix`.
- Open the app again (from the apps menu or in a terminal) and it will reinstall the WINE prefix and SayMore.

### SayMore starts in a random "test" project

This has been added as a workaround. Without an existing project on first run SayMore throws an
error if you try to add a Session or a Person to *any* project. Just choose "open or create"
another project from the menu to get back to the Welcome Screen.