py_sftp uses sftp to transfer files from remote to local and vice-versa using the [paramiko](http://www.paramiko.org/) package

# Options and usage

py_sftp can be used within a Python script as follows:<br>
`from sftp_py.transfer import RemoteTransfer`<br>
`RemoteTransfer([`*`arguments...`*`])`<br>
<br>

### To download from a remote server:

```
# Establish connection and download files. 
# local_path must be a directory
# remote_path can be a single file or a directory containing files to be transferred

conn = RemoteTransfer(host=host_name, username=user_name, port=22, key=private_key_path)
conn.connect()
conn.list_remote_dir(remote_path)  # inspect directory contents
conn.remote_download(remote_path, local_path, copy_hidden_files=True, copy_symlink_files=True remove=False)

# hidden files (.*) and symlink files are copied by default
# remove=True: Downloaded files are removed immediately after transfer
# remove=False (default): Downloaded files are recorded and can be removed later...

conn.downloaded_files  #list of filenames
conn.remove_downloaded()  #removes downloaded files

# Disconnect once finished

conn.disconnect()
```

### To upload to a server:

```
# Similar code to downloading from a remote server...

conn = RemoteTransfer(host=host_name, username=user_name, port=22, key=private_key_path)
conn.connect()
conn.remote_upload(remote_path, local_path, remove=True)  # upload and remove uploaded files from local_path
conn.disconnect()
```
