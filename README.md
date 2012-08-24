# Install Magento @ AWS #

1. Create the application environment
  1. ./start-application.py -a **greetbraadslee**
  1. Repeat until not more errors occur ;)
  1. Mark all relevant login info
1. Add to .ssh/config
  1. Host .hypernode.com
    1. Port 2222
    1. ServerAliveInterval 3
1. Create MySQL database (and clean)
  1. echo "drop database appdb; create database appdb" | mysql -u **lygia** --host=**db-1-**greetbraadslee**.lkjslfd3pnslif1.eu-west-1.rds.amazonaws.com** --password=**fgdgfgfdgfdlkjolijqfeijhpliojasfijh** appdb 
  1. mysql -u **lygia** --host=**db-1-**greetbraadslee**.lkjslfd3pnslif1.eu-west-1.rds.amazonaws.com** --password=**fgdgfgfdgfdlkjolijqfeijhpliojasfijh** appdb < magento_sample_data_for_1.6.1.0.sql
1. Drop all files on remote host
  1. rsync --delete -av magento/ root@**greetbraadslee**.hypernode.com:/home/user/docroot/
  1. rsync --delete -av magento-sample-data/media/ root@**greetbraadslee**.hypernode.com:/home/user/docroot/media/
  1. ssh root@**greetbraadslee**.hypernode.com 'chown -R user:user /home/user/docroot/'
1. Install Magento
  1. ssh root@**greetbraadslee**.hypernode.com
  1. su - user
  1. php install.php --license_agreement_accepted true --locale en_US --default_currency euro --db_host **db-1-**greetbraadslee**.lkjslfd3pnslif1.eu-west-1.rds.amazonaws.com** --db_name appdb --db_user **lygia** --url http://**greetbraadslee**.hypernode.com/ --use_rewrites true --use_secure false --use_secure_admin false --admin_username admin --admin_password **hermaniseenvrolijkevent**  --admin_lastname Admin --admin_firstname Magento --admin_email **my@myemail.com** --timezone "Europe/Berlin" --secure_base_url http://**greetbraadslee**.hypernode.com/ --db_pass **fgdgfgfdgfdlkjolijqfeijhpliojasfijh**
