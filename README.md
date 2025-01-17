# Мануал по работе с QEMU NBD (Network Block Device)

## 1. Подключение модуля ядра `nbd`
```bash
sudo modprobe nbd
```
**Описание**:  
Загружает модуль ядра `nbd`, необходимый для работы с сетевыми блочными устройствами. Это позволяет использовать команды для монтирования образов дисков.

---

## 2. Подключение образа `.qcow2` к устройству `/dev/nbd0`
```bash
sudo qemu-nbd --connect=/dev/nbd0 /var/lib/libvirt/images/work.qcow2
```
**Описание**:  
Команда подключает образ диска `work.qcow2` к блочному устройству `/dev/nbd0`. Это позволяет работать с образом как с обычным диском.

---

## 3. Проверка структуры разделов подключенного устройства
```bash
sudo fdisk -l /dev/nbd0
```
**Описание**:  
Сканирует и выводит таблицу разделов подключенного устройства `/dev/nbd0`. Позволяет определить, какие разделы доступны для монтирования.

---

## 4. Подключение клонированного образа
```bash
sudo qemu-nbd --connect=/dev/nbd0 /var/lib/libvirt/images/work-clone.qcow2
```
**Описание**:  
Команда подключает копию образа `work-clone.qcow2` к тому же устройству `/dev/nbd0`. Это полезно для работы с резервными копиями.

---

## 5. Монтирование раздела из образа
```bash
sudo mount /dev/nbd0p1 /home/user/share
```
**Описание**:  
Монтирует первый раздел (`/dev/nbd0p1`) из подключенного образа в директорию `/home/user/share`. Теперь файлы из образа доступны в этой папке.

---

## 6. Размонтирование раздела
```bash
sudo umount /mnt
```
**Описание**:  
Отключает монтированный раздел, освобождая точку монтирования `/mnt` или другую указанную директорию.

---

## 7. Отключение образа от устройства
```bash
sudo qemu-nbd --disconnect /dev/nbd0
```
**Описание**:  
Отключает устройство `/dev/nbd0` и освобождает его. Это завершает работу с образом диска.

---
