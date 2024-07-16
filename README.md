# free_up_space


Certainly! Below is a shell script that incorporates all the mentioned actions to help free up space on a Mac. Please review the script carefully before running it, as it performs operations that delete files and directories.

Create a Shell Script
Open the Terminal.
Create a new shell script file:
sh
نسخ الكود
nano free_up_space.sh
Copy and paste the following script into the file:
sh
نسخ الكود
#!/bin/bash

# Find and list large files (larger than 100MB) in the home directory
echo "Finding large files (larger than 100MB) in the home directory..."
``find ~ -type f -size +100M -exec ls -lh {} \; | awk '{ print $NF ": " $5 }'``

# Check disk usage of directories in the home directory
echo "Checking disk usage of directories in the home directory..."
```du -sh ~/*```

# Clear system logs
echo "Clearing system logs..."
sudo rm -rf /private/var/log/*

# Clear user cache
echo "Clearing user cache..."
rm -rf ~/Library/Caches/*

# Clear system cache
echo "Clearing system cache..."
sudo rm -rf /Library/Caches/*

# Remove old iOS backups
echo "Removing old iOS backups..."
rm -rf ~/Library/Application\ Support/MobileSync/Backup/*

# Remove unnecessary applications (commented out for safety)
# Uncomment and replace [Application Name] with the actual application name to use
# echo "Removing unnecessary applications..."
# rm -rf /Applications/[Application Name].app

# Empty Trash
echo "Emptying Trash..."
rm -rf ~/.Trash/*

# Remove duplicate files (requires fdupes)
if command -v fdupes &> /dev/null
then
    echo "Removing duplicate files..."
    fdupes -rdN ~
else
    echo "fdupes is not installed. Skipping duplicate file removal..."
fi

# Clean up Homebrew caches (requires Homebrew)
if command -v brew &> /dev/null
then
    echo "Cleaning up Homebrew caches..."
    brew cleanup
else
    echo "Homebrew is not installed. Skipping Homebrew cleanup..."
fi

# Delete old Mail attachments
echo "Deleting old Mail attachments..."
rm -rf ~/Library/Mail/V*/MailData/Attachments/*

# Delete temporary files
echo "Deleting temporary files..."
sudo rm -rf /private/var/tmp/*
sudo rm -rf /tmp/*

echo "Space cleanup completed."
Save and exit the file (in nano, press CTRL+X, then Y, and then ENTER).
Make the Script Executable
Make the script executable by running:
sh
نسخ الكود
chmod +x free_up_space.sh
Run the Script
Run the script with:
sh
نسخ الكود
./free_up_space.sh
Important Considerations
Review and Customize: Make sure to review the script and customize it according to your needs. For example, the application removal section is commented out to prevent accidental deletion of applications.
Permissions: Some commands require sudo and will ask for your password.
Backup Important Data: Always ensure you have backups of important data before running cleanup scripts.
