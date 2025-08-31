# nextcloud-pdlib
credits: https://github.com/mrishab/anton-apps/blob/master/nextcloud/Dockerfile \
Nextcloud 29 including pdlib for face recognition app

# Install instructions ubunto
nano nextcloud.pdlib \
copy code from dockerfile, modify nextcloud version number if needed \
sudo docker build -t nextcloud-pdlib -f nextcloud.pdlib . 

# run docker
sudo docker run -d \ \
-p 8089:80 \ \
-v /YourLocalPath:/var/www/html \ \
-e PHP_UPLOAD_LIMIT=4G \ \
-e PHP_MEMORY_LIMIT=1G \ \
--restart unless-stopped --name nextcloud \ \
nextcloud-pdlib

#  install face recognition

Install face recognition via app store
run:
sudo docker exec --user www-data nextcloudtest php occ face:setup -M 1024M
sudo docker exec --user www-data nextcloudtest php occ face:setup -m 1
