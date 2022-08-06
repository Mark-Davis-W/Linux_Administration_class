#!/bin/env bash

# CSCI 4113 Spring 2022 Lab 1
#   Author: Mark Davis
 
# Space Script
 
# Global Variables

root=$(df -h / | awk 'FNR == 2 {print $5+0}')
boot=$(df -h /boot | awk 'FNR == 2 {print $5+0}')
root_h="Root(/)"
boot_h="(/boot)"

max=80

echo -e "Directory Space Utilization:"
echo -e "(/:root)\t $root%"
echo -e "(/boot)\t\t $boot%\nMonitoring System."

printer () {
	echo -e "ATTENTION: $3 filesystem disk space is at $1% exceeding threshold set at: $2% on account $USER.\n\nPlease attend to this before it becomes a problem on system:\n\n$(hostnamectl)" | mail -s "ADMIN ALERT: $3 directory exceeding threshold: $2%" -r "$USER@localhost" root@localhost
    echo -e "$3 filesystem is exceeding threshold: $2%, Admin has been notified\n"
}


monitor (){
    
    if [ $root -ge $max ]
    then printer $root $max $root_h
    fi

    if [ $boot -ge $max ]
    then printer $boot $max $boot_h
    fi
}

while true
    do monitor
    sleep 60m
done

