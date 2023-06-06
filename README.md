# Docker-Commands
Шпаргалка по установке и базовым командам Docker и k8s


======================================Docker==========================================
# Ставить лучше по оф. доке
	Установка движка 
	https://docs.docker.com/engine/install/debian/
	
	Установка DockerDesktop через .deb пакет 
	https://docs.docker.com/desktop/install/ubuntu/
======================================================================================
	
Дальше, чтобы работало, либо через systemctl запускать службу докера, либо просто DockerDesktop
 
## Создание образа
	docker build -t <image_name> . (точка - текущая папка или расположение Dockerfile)
	
## Посмотреть список контейнеров
	docker images
	
## Запуск контейнера
	docker run --name <container_name> -p 8080:8080 -d <image_name>
	
	-p - порт хоста:порт внутри контейнера
	-d - отделить контейнер от текущего терминала в фон

## Список запущенных контейнеров
	docker ps
	docker ps -a - список всех контейнеров, в том числе неактивных
	
## Баш внутри контейнера
	docker exec -it <container_name> bash
	
	-i - держит STDIN открытым, чтоб можно было вводить команды
	-t - выделяет псевдотерминал (без него могут не работать команды)
	
	внутри контейнера +/- обычные линуксовые команды
	
## Стоп контейнера
	docker stop <container_name>
	
## Удаление контейнера
	docker rm <container_name>
	
## Тегирование образа
	docker tag <image_name> <dockerhub_id>/<image_name>
	
	Не изменит текущий тэг, а создаст новый. При docker images покажет, будто их два,
	но на деле - оба тэга ссылаются на один и тот же образ
	
## Войти в dockerhub из терминала
	docker login
	
	Перед этим нужно будет инициализировать gpg-ключ. Оф. дока:
	https://docs.docker.com/desktop/get-started/#credentials-management-for-linux-users
	
## Пуш на dockerhub
	docker push <dockerhub_id>/<image_name>
	
## Запуск образа на другой машине
	docker run -p 8080:8080 -d <dockerhub_id>/<image_name>
	
	Сам проверит локальное наличие образа, если его нет, то сам спуллит, сам запустит
	
===================================Minikube============================================

# Инфа по установке minikube
	https://minikube.sigs.k8s.io/docs/start/
	
# Установка kubectl
	https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/
	
## Запуск ВМ Minikube
	minikube start
	
	выполняется долго - качает образ, стартует кластер. Надо больше 20Гб свободных
	
## Проверка состояния кластера (локального)
	kubectl cluster-info
	
## Проброс портов в миникуб
	kubectl port-forward <pod-name> <pc-port>:<pod-port>

	
