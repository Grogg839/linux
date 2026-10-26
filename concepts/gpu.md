# NVIDIA GT 730

The goal here is to set my gpu to its highest power state (0f). Right now it's locked in a low power state which is harming my desktop performance.

The pstate file is located in `/sys/kernel/debug/dri/1` and I can read the 3 entries by hand. I want to be able to select 0f and make this stick when I boot.  

From what I've read online, it seems that writing the state you want straight to that file will change it, so for a manual change I can run the following code:

```bash
echo 0f | sudo tee /sys/kernel/debug/dri/1/pstate
```

To check if it worked:

```bash
sudo cat /sys/kernel/debug/dri/1/pstate
```

Now I should try to make this run when I boot my pc, so I know now I need to add to my configuration.nix file, I know I will need a systemd service and I know it will need to be a 'oneshot' type of service.

```nix
systemd.services.gpu-0f = {
  description = "Set the GT 730 to power state 0f";
  wantedBy = [ "multi-user.target" ];
  serviceConfig.Type = "oneshot";
  script = ''
    sleep 10
	echo 0f > /sys/kernel/debug/dri/1/pstate
  '';
};
```

The `wantedBy` line just means 'run every time this computer boots'
