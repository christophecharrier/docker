
#### Docker command ####

docker run --name sabnzbd -d -v /colosus/sabnzbd/datadir:/datadir -v /colosus/sabnzbd/media:/media -p 8080:8080 sabnzbd
