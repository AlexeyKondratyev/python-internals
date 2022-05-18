# python-internals

## Подготовка к проверке патча

- Скопировать патчи в директорию, например `/tmp/bin`
- Запустить контейнер для проверки
```sh
docker run -ti --rm -v /tmp/bin:/tmp/bin centos:7 /bin/bash
```
- Установить python 2.7
```sh
yum clean all
yum install -y\
    git\
    make\
    gcc-c++\
    vim\
    ssh\
cd /opt
git clone -b 2.7 --single-branch https://github.com/python/cpython.git
cd cpython
```

## Применить патч

- Проверить патч
```sh
git apply --check /tmp/bin/until.patch
```
- применить патч
```sh
git am --signoff < /tmp/bin/until.patch
```
- собрать python
```sh
./configure --with-pydebug --prefix=/tmp/python
make -j2
```
