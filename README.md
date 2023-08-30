# project
git session

demo
# sub header 

watch the youtube vedio 
#!/bin/bash

# Set your Windows shared folder details
windows_share="//WINDOWS_HOST/SharedFolder"
mount_point="/mnt/shared"

# Set your Windows username and password
windows_username="your_windows_username"
windows_password="your_windows_password"

# Create the mount point if it doesn't exist
if [ ! -d "$mount_point" ]; then
    sudo mkdir -p "$mount_point"
fi

# Mount the Windows shared folder
sudo mount -t cifs -o username="$windows_username",password="$windows_password",vers=3.0 "$windows_share" "$mount_point"

# Check if the mount was successful
if [ $? -eq 0 ]; then
    echo "Windows shared folder mounted successfully at $mount_point"
else
    echo "Failed to mount Windows shared folder"
fi
