###Установка Python3 на CentOS 7
Первым делом ставим необходимые пакеты
```
yum install -y wget zlib-devel gcc
```
>ВНИМАНИЕ!!! `zlib-devel` ставить обязательно в самом начале, в противном случае при запуске конфига компиляции питона не будет добавлена компиляция zlib и django установить не получится.

С официального сайта Python скачиваем .tar.gz последней версии, например для Python 3.5.1
```
wget https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tgz
tar xf Python-3.5.1.tgz
cd Python-3.5.1
./configure
```
С официального сайта Django качаем .tar.gz последней стабильной версии и распаковываем
```
wget https://www.djangoproject.com/m/releases/1.9/Django-1.9.1.tar.gz
tar xf Django-1.9.1.tar.gz
```
Пока что установить ничего не выйдет, появится ошибка отсутствия setuptools для python3.
Адекватного setuptools для третьего питона нет, зато есть враппер `distributed` который и будем ставить. А еще, добрые люди запаковали его в zip, поэтому надо поставить `unzip`
```
yum install -y unzip
wget https://pypi.python.org/packages/source/d/distribute/distribute-0.7.3.zip
unzip distribute-0.7.3.zip
cd distribute-0.7.3
python3 setup.py install
```
Теперь можем вернуться в директорию с `Django` и установить его
```
cd Django-1.9.1
python3 setup.py install
```
Чтобы проверить, что все прошло успешно, вводим в терминал 
```
python3
import django
print(django.get_version())
```
Если получим в выводе номер версии (в данном случае это была `1.9.1`) значит все установилось успешно.
