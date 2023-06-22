# Introduction
The container images are locked from NGC Registry
We need API key to access them

## Please follow this guide:
https://docs.nvidia.com/ngc/gpu-cloud/ngc-user-guide/index.html#generating-api-key

## Install NGC CLI
https://ngc.nvidia.com/setup/installers/cli
(We are using AMD64 Linux.)
```ruby
wget --content-disposition https://ngc.nvidia.com/downloads/ngccli_linux.zip && unzip ngccli_linux.zip && chmod u+x ngc-cli/ngc
```
```ruby
find ngc-cli/ -type f -exec md5sum {} + | LC_ALL=C sort | md5sum -c ngc-cli.md5
```
```ruby
echo "export PATH=\"\$PATH:$(pwd)/ngc-cli\"" >> ~/.bash_profile && source ~/.bash_profile
```
```ruby
ln -s $(pwd)/ngc-cli/ngc [destination_path]/ngc
```
```ruby
ngc config set
```

```ruby
docker login nvcr.io
```
### Username
```
$oauthtoken  //Enter exactly the $oauthtoken
```
### Password
#### Get the password (API) here.
https://ngc.nvidia.com/setup/api-key
```
<Your API>
```
Login succeeded


## More about NGC
https://docs.nvidia.com/dgx/ngc-registry-for-dgx-user-guide/index.html
