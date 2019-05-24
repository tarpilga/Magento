# Magento

	  ========================================= installation Magenta Avec Docker =========================================

===> etape 1

	__charger les images
		==> docker load -I imageMagento
		==> docker load -I imageMysql
		==>  docker load -I imagePhpmyadmin
	
	__Importer les container
		==> docker import containerMagento
		==> docker import containerMysql
		==> docker import containerPhpmyadmin
	
	__Creer les volume Magenta
		==> docker volume create volumeMagento

===> Etape 2

	__Installer mysql et phpmyadmin avec docker 

		-créer un réseau docker 
			==> docker network create nameNetwork

		-crée le container Mysql
			==> mkdir -p  /opt/mysql (cette commande créer un dossier parent a la racine dans var/lib….)
			==> sudo docker run --name mysql_mag01 --network dockerNet -e MYSQL_ROOT_PASSWORD=password -v /opt/mysql:/var/lib/mysql -p 3306:3306 mysql:5.6.23
		
		-créer le container phpMyadmin
			==> sudo docker run --name admin_mag01 --network dockerNet -e PMA_HOST=ipMysql -p 8080:80 phpmyadmin/phpmyadmin


		en suite aller sur l’url taper le nom de votre adresse plus le port le mot de passe es MYSQL_ROOT_PASSWORD


===> Etape 3 Magento 
	
	__taper la commande suivante 
		==> sudo docker run -ti --name  magentoName --network  dockerNet -v volumeMagento:/var/lib/docker/volumes/volumeMagento -e DB_SERVER=mysql_mag01  -p 3000:80 -d alexcheng/magento2



NB: 
	=> -v volumeMagento:/var/lib/docker/volumes/volumeMagento
                permet d’ajouter un volume a magenta pour que les données reste permanente 
                
    1=> on a créer le volume dans l’étape 1 
    ==> docker volume create volumeMagento  pour trouver le répertoire  
    var/lib/docker/volumes/volumeMagento taper ( docker volume inspect volumeMagento)
