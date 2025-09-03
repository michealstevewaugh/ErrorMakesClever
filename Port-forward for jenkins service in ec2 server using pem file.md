If your Azure VM was created with a .pem private key file, then you should not use ~/.ssh/id_rsa.
Instead, you must use that .pem file to connect.

✅ How to SSH with .pem file

If your private key file is named something like mykey.pem, run:
```
ssh -i /path/to/mykey.pem azureuser@74.162.41.187
```
✅ How to port-forward Jenkins using .pem
```
ssh -i /path/to/mykey.pem -L 8080:localhost:8080 azureuser@74.162.41.187
```
✅ If you don’t want to keep a terminal open, run it with -N -f:
```
ssh -i volt-tools-key.pem -L 8080:localhost:8080 azureuser@74.162.41.187 -N -f
```

Then open in your browser:
```
http://localhost:8080
```

✅ Ways to stop it

If you are still in that terminal → just type:
```
exit
```
(or press Ctrl + D)
This closes the SSH session → port forwarding stops.

If you put it in the background, find the process:
```
ps aux | grep "ssh -L"
```
Then kill it:
```
kill <PID>
```
