# Linux Services, Sockets, and Logs

## 1. Checking Service Status

Use `systemctl` to inspect systemd-managed services.

```bash
systemctl status ssh
systemctl status ssh.socket
```

- `ssh.service` runs the SSH server.
- `ssh.socket` can listen for incoming SSH connections and activate the service when needed.

A service can be inactive while its associated socket is active.

## 2. Inspecting Network Sockets

```bash
ss -tuln
sudo ss -tulpn
```

- `-t`: TCP sockets
- `-u`: UDP sockets
- `-l`: Listening sockets
- `-n`: Numeric addresses and ports
- `-p`: Associated process information, when available

Common ports:

- TCP 22: SSH
- UDP/TCP 53: DNS

A listening port does not automatically mean the service is reachable from the internet.

## 3. Viewing System Logs

```bash
sudo journalctl -n 20 --no-pager
sudo journalctl -u ssh --no-pager
sudo journalctl -u ssh.socket --no-pager
```

- `journalctl` displays systemd journal logs.
- `-u` filters logs by unit.
- `-n 20` displays the latest 20 matching entries.
- `--no-pager` prints output directly in the terminal.

A query returning `-- No entries --` means no matching entries were available for that query. It does not necessarily mean the logging system is broken.

## 4. Troubleshooting Principles

1. Check the service status.
2. Inspect the relevant network sockets.
3. Examine available logs.
4. Form a hypothesis based on the evidence.
5. Test the hypothesis before changing configuration.
6. Verify the result.

## 5. Lessons From the Lab

- Ubuntu uses systemd to manage many services.
- Socket activation allows systemd to listen for connections and activate a service when appropriate.
- Logs help explain system events.
- An authentication failure should be investigated in context rather than automatically treated as an attack.
