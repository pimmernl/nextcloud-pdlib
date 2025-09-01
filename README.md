# nextcloud-pdlib
Nextcloud 29 including pdlib for face recognition app. \
This docker can be used for existing or new installation. \
If you are new to nextcloud, follow the installation instructions on the nextcloud site. \
If you allready have nextcloud docker running, please assure you have identical version numbers to prevent issues. \

**Install instructions ubunto** \
nano nextcloud.pdlib \
copy code from https://github.com/pimmernl/nextcloud-pdlib/blob/main/Dockerfile, modify nextcloud version number if needed \
sudo docker build -t nextcloud-pdlib -f nextcloud.pdlib . \
It can take a while, you should not get errors, warnings can be ignored.

**Run docker** \
Change: \
  YourLocalPath to your local direcory for storing Nextcloud data, see nextcloud instructions for permissions. If you have existing nextcloud instance, no data will be erased. \
  Port number 8089 to you preference \
  
sudo docker run -d \ \
-p 8089:80 \ \
-v /YourLocalPath:/var/www/html \ \
-e PHP_UPLOAD_LIMIT=4G \ \
-e PHP_MEMORY_LIMIT=1G \ \
--restart unless-stopped --name nextcloud \ \
nextcloud-pdlib

**install face recognition (quick guide)** \
For full manual and settings instructions see: https://github.com/matiasdelellis/facerecognition \
Install face recognition via app store \
run: \
  sudo docker exec --user www-data nextcloudtest php occ face:setup -M 1024M \
  sudo docker exec --user www-data nextcloudtest php occ face:setup -m 1 \
Check in the administrator section of Nextcloud, the Face Recognition, on the bottom the status schould be green. \
run to test: \
  sudo docker exec --user www-data nextcloudtest php occ face:background_job -u UserNextcloud -t 900 \
If all ok, add the background cron job, example to run task each hour for 30 minutes: \
  sudo crontab -e \
  0 * * * * sudo docker exec --user www-data nextcloud php occ face:background_job -u UserNextcloud -t 1800 \

**Credits** \
https://github.com/matiasdelellis/facerecognition \
https://github.com/mrishab/anton-apps/blob/master/nextcloud/Dockerfile \
