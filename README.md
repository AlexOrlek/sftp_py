sftp_py is a Python package for transferring files between remote and local directories using the [paramiko](http://www.paramiko.org/) sftp client<br>

# Installation 

### From pypi:
```bash
pip3 install sftp_py
```
### From GitHub repository:
```bash
git clone https://github.com/AlexOrlek/sftp_py.git
cd sftp_py
pip3 install .
```
<br>

# Options and usage

sftp_py can be used within a Python script as follows:<br>
`from sftp_py.transfer import RemoteTransfer`<br>
`RemoteTransfer([`*`arguments...`*`])`<br>
<br>

### To download from a remote server:

```bash
# Establish connection and download files. 
# local_path must be a directory
# remote_path can be a single file or a directory containing files to be transferred

conn = RemoteTransfer(host=host_name, username=user_name, port=22, key=private_key_path)
conn.connect()
conn.list_remote_dir(remote_path)  # inspect directory contents
conn.remote_download(remote_path, local_path, copy_hidden_files=True, copy_symlink_files=True, remove=False)

# hidden files (.*) and symlink files are copied by default
# remove=True: downloaded files are removed immediately after transfer
# remove=False (default): downloaded files are recorded and can be removed later...

conn.downloaded_files  # conn.downloaded_files records list of downloaded filenames
conn.remove_downloaded()  # remove downloaded files

# Disconnect once finished

conn.disconnect()
```

### To upload to a server:

```bash
# Code for uploading to a remote server is similar to code for downloading from a remote server...

conn = RemoteTransfer(host=host_name, username=user_name, port=22, key=private_key_path)
conn.connect()
conn.remote_upload(remote_path, local_path, remove=True)  # upload and remove uploaded files from local_path
conn.disconnect()
```
<br>

# License

[MIT License](https://en.wikipedia.org/wiki/MIT_License)
