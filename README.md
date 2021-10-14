# Odoo-11 installation on Linux(Ubuntu)

1. Install git on your Linux machine

    `sudo apt-get install git`

2. Clone specefic odoo version from the odoo git repository

    `git clone --depth 1 -b 11.0 -single-branch https://github.com/odoo/odoo.git`

3. Now add deadsnakes ppa repository to change between python versions later

    `sudo add-apt-repository ppa:deadsnakes/ppa`
    
    `sudo apt-get update`
    
4. Install Python 3.7 or later

    `sudo apt-get install python3.7`

5. install postgresql 11  (https://www.postgresql.org/download/linux/ubuntu/)

    - Create the file repository configuration:
    
      `sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'`
    
    - Import the repository signing key:

      `wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -`
     
    - Update the package lists:

      `sudo apt-get update`
    
    - Install the latest version of PostgreSQL.
  
    - If you want a specific version, use 'postgresql-11' or similar instead of 'postgresql':

      `sudo apt-get -y install postgresql-11`
      
6. Create User and alter password

    `sudo -u postgres createuser -s $User_name`
    
    - Enter into postgres console

        `sudo -u postgres psql`
        
    - Alter the default password

        `ALTER USER user_name WITH PASSWORD 'new_password';`
        
7. Now create virtual environment

    - install pip3

      `sudo apt install python3-pip`
      
    - install virtual environment by pip3

      `pip3 install virtualenv`
      
    - finally create your virtual environment

      `python3.7 -m virtualenv $your_environment_name`
 
 8. Install all the dependencies in your virtual environment now

    - Install python3.7 dev first because of the native languages dependencies

        `sudo apt install python3.7-dev`
    
    - Install other dependencies

        `sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev 
    libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev 
    liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev libxcb1-dev libpq-dev`
    
    - Now install all the dependencies listed in requirements.txt file located in odoo directory

        `pip3 install -r $path_to_the_requirements.txt_file`
        
  9. Install wkhtmltopdf
  
    - Go to (https://github.com/odoo/odoo/wiki/Wkhtmltopdf/) and make sure which version should be compatible with which version of odoo
    
    
        `wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.5-1/wkhtmltox_0.12.5-1.focal_amd64.deb`
      
      
        `sudo apt install ./wkhtmltox_0.12.5-1.focal_amd64.deb`
      
  10. Download and install nodejs and npm

      `sudo apt install npm nodejs`
  
  11. Download and install node-less

      `sudo apt install node-less`
      
  12. Install rtlcss

      `sudo apt install rtlcss`
      
  13. Now make a configuration file outside of odoo folder with .conf extension and paste the codes bellow with proper credentials

      `[options]`
      
      `addons_path = $path_to_the_odoo_addons_folder, (add custom addons path here if any)`
      
      `db_host = localhost`
      
      `db_port = 5432`
      
      `db_password = $superuser_pass`
      
      `db_user = $superuser_name`
      
      `server_wide_modules = web`
      
  14. Now execute the odoo-bin python executable with the path of conf file

      `./odoo-bin -c $path_of_the_conf_file`
