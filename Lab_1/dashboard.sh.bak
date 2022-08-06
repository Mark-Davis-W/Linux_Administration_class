#!/bin/env bash

# CSCI 4113 Spring 2022 Lab 1
#   Author: Mark Davis

# Dashboard Script

# Global Variables

dom=google.com
internet="NO"
#lo=awk -v OFS='\t' '/lo:/ {print $2,$10} /Receive/ {print $2,$4}' /proc/net/dev
lo_rec=$(awk '/lo:/ {print $2;}' /proc/net/dev)
lo_trans=$(awk '/lo:/ {print $10;}' /proc/net/dev)
enp0s3_rec=$(awk '/enp0s3:/ {print $2;}' /proc/net/dev)
enp0s3_trans=$(awk '/enp0s3:/ {print $10;}' /proc/net/dev)
shells=$(cat /etc/shells | wc -l)
ttl_users=$(cat /etc/passwd | wc -l)
active_users=$(who | awk '{print $1}' | sort -u | wc -l)
bashes=$(awk -F ':' '{print$7}' /etc/passwd | grep -c /bin/bash)
noLogins=$(awk -F ':' '{print$7}' /etc/passwd | grep -c /sbin/nologin)
falses=$(awk -F ':' '{print$7}' /etc/passwd | grep -c /bin/false)
files_ttl=$(find / -type f 2> /dev/null | wc -l)
directories=$(find / -type d 2> /dev/null | wc -l)

# original way but second I think is better
# uptime | cut -d "," -f 3,4,5 | cut -d ":" -f 2
CPU=$(uptime | awk 'BEGIN{FS="load average: "} {print $2}')
RAM=$(free --mega | awk '/Mem:/ {print $4}')


function connected
{
   ping $dom -c 4 > /dev/null

   if [ $? -eq 0 ]
    then
      internet="YES!"
   fi
}
connected

# -----Dashboard Print OUT------- #

echo -e " CPU AND MEMORY RESOURCES ------------------------------------------\n"
echo -e " CPU Load Average: $CPU\t Free RAM: $RAM MB\n\n"

echo -e " NETWORK CONNECTIONS -----------------------------------------------\n"
echo -e " lo:\t Bytes Received: $lo_rec\t\t Bytes Transmitted: $lo_trans\n"
echo -e " enp0s3: Bytes Received: $enp0s3_rec\t Bytes Transmitted: $enp0s3_trans\n"
echo -e " Internet Connectivity:\t $internet\n\n"

echo -e " ACCOUNT INFORMATION -----------------------------------------------\n"
echo -e " Total Users:\t $ttl_users\t Number Active: $active_users\n"
echo -e " Shells:\t $shells\n"
echo -e " /sbin/nologin:\t $noLogins\n"
echo -e " /bin/bash:\t $bashes\n"
echo -e " /bin/false:\t $falses\n\n"

echo -e " FILESYSTEM INFORMATION --------------------------------------------\n"
echo -e " Total Number of Files:\t\t $files_ttl\n"
echo -e " Total Number of Directories:\t $directories\n"

