Installing Nav Linux

Verify Available Disks
Sebelum memulai instalasi, pastikan semua disk dan partisi telah terdeteksi dengan benar. Langkah ini membantu menghindari kesalahan saat memilih target instalasi.
Jalankan:
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT

Contoh output:
NAME   SIZE TYPE FSTYPE MOUNTPOINT
loop0    1G loop squashfs
loop1  5.3G loop ext4    /run/rootfsbase

sda   931.5G disk
├─sda1 466G part ntfs
└─sda2 465G part ntfs

sdb   931.5G disk
├─sdb1 207G part ntfs
├─sdb2 59.9G part ext4
├─sdb3 48.8G part ext4
├─sdb4 512M part vfat
├─sdb5 16G  part swap
├─sdb6 133.5G part ntfs
└─sdb7 465.8G part ntfs

sdc   14.5G disk
└─sdc1 14.5G part vfat /run/initramfs/live

Understanding the Output
Dalam contoh di atas:
/dev/sdc adalah USB Live Nav Linux.
/dev/sdb6 akan digunakan sebagai partisi root (/).
/dev/sdb4 adalah EFI System Partition (ESP).
/dev/sdb5 adalah partisi swap yang sudah ada.


Pastikan target instalasi sudah sesuai sebelum melanjutkan ke tahap berikutnya.
Warning
Memilih partisi yang salah dapat menyebabkan kehilangan data. Periksa kembali nama dan ukuran partisi sebelum melakukan format.
