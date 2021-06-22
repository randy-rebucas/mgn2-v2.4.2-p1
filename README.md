Setup php cinfugurations and extentions
Create DB

C:\xampp\apache\conf\extra
<VirtualHost *:80>
	AllowEncodedSlashes NoDecode
    DocumentRoot "C:/xampp/htdocs/mgn2/pub"
    ServerName mgn2.com
</VirtualHost>

C:\Windows\System32\drivers\etc
	127.0.0.1       mgn2.com
  
Download Magento via compaser
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .

Magento Setup install  
php bin/magento setup:install --base-url="http://mgn2.com/" --db-host="localhost" --db-name="mgn2" --db-user="root" --db-password="" --admin-firstname="admin" --admin-lastname="admin" --admin-email="user@example.com" --admin-user="admin" --admin-password="admin123" --language="en_US" --currency="USD" --timezone="America/Chicago" --use-rewrites="1" --backend-frontname="admin" --search-engine=elasticsearch7 --elasticsearch-host="http://mgn2.com" --elasticsearch-port=9200 --elasticsearch-enable-auth=1 --elasticsearch-username=elastic --elasticsearch-password=KDTf047fPymf4dLwi7vpOdGh

Update those lines
vendor\magento\framework\Image\Adapter\Gd2.php
if ($url && isset($url['scheme']) && !in_array($url['scheme'], $allowed_schemes) && !file_exists($filename)) {

vendor\magento\framework\View\Element\Template\File\Validator.php
$realPath = str_replace('\\', '/', $this->fileDriver->getRealPath($path));

php bin/magento indexer:reindex
php bin/magento setup:upgrade
php bin/magento setup:static-content:deploy -f
php bin/magento cache:flush

Opional
php bin/magento sampledata:deploy

php bin/magento module:disable Magento_TwoFactorAuth

