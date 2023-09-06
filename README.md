@echo off

setlocal enabledelayedexpansion

:: Specify the search string
set search_string=apple

:: Get the current date in a specific format (YYYYMMDD)
for /f "tokens=2-4 delims=/ " %%a in ('date /t') do (
    set "current_date=%%c%%b%%a"
)

:: Define the directory name based on the current date
set directory_name=!current_date!_GA

:: Specify the path to the directory where the files are located
set base_directory=C:\path\to\base\directory

:: Combine the base directory path and the constructed directory name
set directory_path=!base_directory!\!directory_name!

:: Define the file name you want to search within
set file_name=yourfile.txt

:: Combine the directory path and file name
set file_path=!directory_path!\!file_name!

:: Use the `find` command to search for the string in the file
find /i "%search_string%" "!file_path!" | find /c /v ""

:: Check the %errorlevel% to determine if the string was found
if %errorlevel%==0 (
    :: Count the number of lines containing the search string
    for /f %%A in ('findstr /i /c:"%search_string%" /c:"%search_string%"^<"!file_path!" ^| find /c /v ""') do (
        set count=%%A
    )
    
    echo String "%search_string%" found in %count% line(s) in the file !file_name! in directory !directory_name!.
) else (
    echo String "%search_string%" not found in the file !file_name! in directory !directory_name!.
)

endlocal

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
