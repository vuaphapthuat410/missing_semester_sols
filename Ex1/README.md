1. You need to be using a Unix shell like Bash or ZSH.
2. Create a new directory called missing under /tmp.
```cd /tmp ```
```mkdir missing```
3. Look up the ```touch``` program. The ```man``` program is your friend.
4. Use ```touch``` to create a new file called semester in missing.
```cd missing```
```touch semester```
5. Write the following into that file
```echo "#"'!'/bin/sh > semester```
```echo curl --head --silent https://missing.csail.mit.edu | sudo tee -a semester```
6. Try to execute the file
```./semester```
**REASON**: you don't have excute permission(r-- in my case).
7. Why does ```sh``` work, while ./semester didn’t?
**REASON**: If you use ```sh```, you **read** the **semester** as input of ```sh```, you don't excute it directly.
8. Look up the chmod program (e.g. use man chmod).
9. Make it possible to run the command ./semester
``` chmod 755 semester```
**Notes**: 777 is OK but we often not use 777 because it means that you grant all privileges non-root users.
**Mechanism of Shebang**: ```Shell``` will parse the rest of the file's initial line as an interpreter directive. Read more at Shebang's wiki. 
10. Use | and > to write the “last modified” date output by semester into a file called last-modified.txt in your home directory.
```./semester | grep --ignore-case last-modified | cut -d ' ' -f3,4,5 | tee last-modified.txt```
**Explain**: ```./semester``` use as input of pipeline.
```grep --ignore-case last-modified``` seek for **last-modified** field in input and ignore letter case.
```cut -d ' ' -f3,4,5``` will cut the line contains **last-modified** using ' ' delimiter. In my case, i choose the field (-f) 3,4,5. Read in ```man cut``` for more information.
11. Write a command that reads out your laptop battery’s power level
We can google and ge the answer that **/sys/class/power_supply/BAT0/** directory that store ACPI information about your first battery.
So we do: ```cat /sys/class/power_supply/BAT0/capacity```
_Read more at_ : ```https://ostechnix.com/how-to-check-laptop-battery-status-in-terminal-in-linux/```
And one more thing if you wanna check your CPU temparture, here are the command i found on stackoverflow:
```cat /sys/class/thermal/thermal_zone*/temp``` which you replace * with 1,2,3, .. up to 12 in my case.



