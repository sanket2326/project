@echo off
setlocal enabledelayedexpansion

set "sourceDir1=C:\Path\To\Directory1"
set "sourceDir2=C:\Path\To\Directory2"

:: Create lists of items in both directories
dir /b /s /a-d "%sourceDir1%" > "%temp%\dir1.txt"
dir /b /s /a-d "%sourceDir2%" > "%temp%\dir2.txt"

:: Check for orphaned files or directories in sourceDir1
echo Orphaned items in %sourceDir1%:
for /f %%i in ('findstr /v /g:"%temp%\dir2.txt" "%temp%\dir1.txt"') do (
    echo %%i
)

:: Check for orphaned files or directories in sourceDir2
echo Orphaned items in %sourceDir2%:
for /f %%i in ('findstr /v /g:"%temp%\dir1.txt" "%temp%\dir2.txt"') do (
    echo %%i
)

:: Clean up temporary files
del "%temp%\dir1.txt" "%temp%\dir2.txt"

pause


for /f "delims=" %i in ('dir /ad /b /o-d') do set recent=%i& goto :done
:done
echo Most recent directory: %recent%


git session

demo
# sub header 

watch the youtube vedio 
#!/bin/bash

path="/home/sanket/note/s3"
num_to_keep=2

#file availabe or not available
status=$(find "$path" -maxdepth 1 -type d -printf '%T@ %p\n' | sort -n -r)

# Execute the find, sort, awk, cut, and xargs commands to get the list of directories to delete
dirs_to_delete=$(find "$path" -mindepth 1 -maxdepth 1 -type d -printf '%T@ %p\n' | sort -n -r | awk -v N="$num_to_keep" 'NR > N' | cut -d ' ' -f 2-)


if [ -n "$status" ]; then
        echo "New modified directories are available:"
        echo "$status"
else
        echo "No new directories are available."
fi

# Check if there are directories to delete
if [ -n "$dirs_to_delete" ]; then
    echo "The following directories will be deleted:"
    echo "$dirs_to_delete"
    echo "$dirs_to_delete" | xargs rm -r


else
    echo "No directories to delete."
fi
