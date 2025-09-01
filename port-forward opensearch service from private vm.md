Everyone can't ssh the private machine. So use under the same cidr/subnet range public machine for ssh and create a tunnel.
```
ssh -i mykey.pem -L 9200:<private-vm-ip>:9200 user@<bastion-public-ip>
```

For opensearch:
```
ssh -i volt_bastion.pem -L 9200:10.20.13.4:9200 azureuser@40.120.107.194
```
For opensearch-dashboard:
```
ssh -i volt_bastion.pem -L 5601:10.20.13.4:5601 azureuser@40.120.107.194
```
