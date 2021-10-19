Tài liệu

Hướng dẫn xây dựng hệ thống mail zimbra - mô hình single mail






MỤC LỤC

1. Lên kế hoạch triển khai hệ thống
   1. Cài đặt hệ điều hành máy chủ
   1. Thiết lập cấu hình kết nối mạng
   1. Chuẩn bị phần mềm cài đặt máy chủ mail zimbra
   1. Cài đặt phần mềm máy chủ mail zimbr
1. Cài đặt hệ điều hành máy chủ
1. Thiết lập cấu hình kết nối mạng
   1. Cài đặt hostname
   1. Disable SELINUX
   1. Reboot máy để nhận hostname
   1. Kiểm tra kết quả sau khi thay đổi cấu hình
   1. Cấu hình card mạng “eth0”
   1. Khởi động lại dịch vụ mạng
   1. Kiểm tra thông tin card mạng
   1. Kiểm tra kết nối mạng
   1. Cài đặt một số công cụ hỗ trợ
   1. Update hệ điều hành
   1. reboot

\4.	Chuẩn bị cài đặt Zimbra

`	`4.1.	Cài đặt DNS

`	`4.2.	Sửa file named.conf

`	`4.3.	Tạo bản ghi phân giải

`	`4.4.	Start và enable dịch vụ

`	`4.5	Tạo rule cho firewall cho phép sử dụng DNS

`	`4.6	Kiểm tra các file DNS

`	`4.7.	Kiểm tra phân giải tên miền

`	`4.8.	Thêm # ở dòng Defaults requiretty trong Sudoers để tránh lỗi LDAP

4.9.	Disable một số dịch vụ xung đột với Zimbra

\5.	Cấu hình và cài đặt Zimbra

5.1	Download Zimbra CS NE 8 (8.6) về máy client

5.2 	Cài đặt zimbra

5.3	Kiểm tra trạng thái của service của Mail Zimbra

1. **Lên kế hoạch triển khai**
   1. ***Cài đặt hệ điều hành máy chủ***

Cài đặt hệ điều hành máy chủ CentOS 7 cho hệ thống Mail Zimbra

2. ***Thiết lập cấu hình kết nối mạng***

Thiết lập cấu hình kết nối mạng trên máy mail Zimbra, gồm:

\+ Địa chỉ IP, Subnetmask

\+ Gateway

\+ DNS

\+ hostname

3. ***Chuẩn bị phần mềm cài đặt máy chủ mail zimbra***

Một số bước cần chuẩn bị trước khi cài đặt phần mềm máy chủ thư Zimbra:

\+ Thay đổi timezone, thời gian hệ thống

Cài đặt date      

**Kiểm tra date:**

**[root@mail /]# date**

`	`**Cài đặt lại date:**

**[root@mail /]# date -s "Sat Sep 31 17:37:59 ICT 2016"**

\+ Thêm các kho phần mềm cần thiết

\+ Cập nhật HĐH máy chủ

\+ Cài đặt 1 số công cụ, tiện ích (cơ bản)

\+ Cài đặt 1 số công cụ, tiện ích (nâng cao)

\+ Thiết lập hệ thống DNS cục bộ

\+ Disable SELinux

**[root@mail /]# vi /etc/sysconfig/selinux**

` `**Thay đổi dòng “SELINUX=enforcing” thành “SELINUX=disabled”**

**SELINUX=disabled**


![https://lh4.googleusercontent.com/\_VZZf-N5MEs4auVq1pxEknbx\_wvuzG4oxKPlUmyVDp1Mj-YBTj2PHOsa0z6TbmZUQC0mFGlI7383wB1bK4YZQuA-Jqt4FFHE98lxhV0pwVwDTYwp0G9dcYSvxcpajz2zote1N6nu](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.001.png)

\+ Mở Port trên Firewall

\+ Disable 1 số dịch vụ xung đột với Zimbra

4. ***Cài đặt phần mềm máy chủ mail zimbra***

Cài đặt  và cấu hình phần mềm máy chủ thư ZCS 8.6, phiên bản NE

2. **Cài đặt hệ điều hành máy chủ**

Phần mềm máy chủ thư Zimbra được cài đặt trên HĐH máy chủ Linux: CentOS-7 (64-bit). Các bước cài đặt HĐH CentOS-7 được triển khai bình thường.

3. **Thiết lập cấu hình kết nối mạng**
   1. ***Cài đặt hostname***

**[root@mail:~] # vi /etc/hostname**

![https://lh3.googleusercontent.com/awAroQnPLqJ\_RNZZ3KPKr5FP8dVt-jVctNh8lWtpfqUxmFVOMY2bBbWFOJJwWX5jpc5K0JsmfZJoIjQu5wrXQTNueb94WUAzm865CVJyvgSd\_P1eMOYi5n7F5Rc1MPeXnqvgzino](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.002.png)

2. ***Reboot máy để nhận hostname***

**[root@mail:~] # reboot**

3. ***Kiểm tra kết quả sau khi thay đổi cấu hình***

**[root@mail:~] # hostname**

![https://lh3.googleusercontent.com/ljHnLkxLoazN6qprTBu9WUnM\_YkePLStGcMVcq7sFXrEN3ANQWR5wdJjCKw2b992HcsuJQgpf51cJSqiH8ETasKPVJAWOTu6-4-mC4uB3G6DNCPoaZtMAyIPkFudJVLGpGfH0iWz](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.002.png)

4. ***Cấu hình card mạng “eno16777736”***

**[root@mail:~] # vi /etc/sysconfig/network-script/ifcfg-eno16777736**

![](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.003.png)

5. ***Khởi động lại dịch vụ mạng***

**[root@mail:~] # systemctl restart network**

6. ***Kiểm tra thông tin card mạng***

**[root@mail:~] # ip addr**

![https://lh6.googleusercontent.com/g45rof5adQgFGg5gKM1-mO-P3Qg8ok6BxayfTNiXYxGjUBZ99aV7pshxFrKw4gGDh64W2PPMaO\_XBPqcl11G9gDv34oO4FNSBxVVS5DHOGdRgB74t5ogPM0vubvplquxiiJv73Rn](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.004.png)

7. ***Kiểm tra kết nối mạng***

**[root@mail:~] # ping google.com**

![https://lh4.googleusercontent.com/nJibM0-0Sc9TOBp8iaWJNkYOA8z5P-VZ0WQN0IFjtunyVgmEkrhMmIUDfI8OE9J0W8PovJU13vbbeAXsK2XHkGmzoW-Ge4uB1WF5ac5EV0XWylHDcNikS6gyfRYGEDj21-kuFTW1](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.005.png)

8. ***Cài đặt một số công cụ hỗ trợ***

**[root@mail~] # rpm -Uvh [http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm**](http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm)**

**[root@mail~] # rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-5.rpm**

**[root@mail~] #yum install wget screen lsof rsync nmap net-tools unzip sudo sysstat perl-core -y**

**[root@mail /]# yum install vim-enhanced telnetyum -y**

9. ***Update hệ điều hành - optional***

**[root@mail~] #yum update -y**

10. ***reboot***

**[root@mail:~] #c**

4. **Chuẩn bị cài đặt Zimbra**

`	`***4.1.	Cài đặt webmin và DNS:***

***[root@mail /]# vim /etc/yum.repos.d/webmin.repo***

***[Webmin]***

***name=Webmin Distribution Neutral***

***#baseurl=http://download.webmin.com/download/yum***

***mirrorlist=http://download.webmin.com/download/yum/mirrorlist***

***enabled=1***

***[root@mail /]# rpm --import http://www.webmin.com/jcameron-key.asc***

***[root@mail /]# yum install webmin perl-Net-SSLeay -y***

***[root@mail /]# service webmin start***

***[root@mail /]# lsof -i :10000***

***[root@mail /]# chkconfig webmin on***

**[root@mail~] # yum install bind bind-utils bind-chroot –y**

**truy cập địa chỉ: [https://ip_máy:10000**](https://ip_máy:10000)**

**khởi tạo create master zone và các bản ghi:**

**hanu.vn A ip\_máy** 

**zimbra.hanu.vn A ip\_máy**

**hanu.vn MX zimbra.hanu.vn**

**Truy cập trình duyệt web (eg: coccoc)**

**-Go https://9.9.9.9:100000**

**-Login vào hệ thống**

**>username: root**

**>password: 123456a@**

**-Ở sidebar: vào “un-used modules”**

`		  `**Chọn> “BIND DNS server”**

**-Trong phần “Existing DNS Zones”: chọn> “create master zone”**

`				`![](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.006.jpeg)

**-Trong Edit master zone**

`	`**>Chon Address: add 2 Address**

![](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.007.jpeg)

`	`**>Mail server: add mail server**


![](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.008.jpeg)

**6.Sửa file:**



`	`***4.2.	Sửa file named.conf***

**[root@mail:~] # vi /etc/named.conf**

![https://lh4.googleusercontent.com/pmJwRPMiDLzumygRTiW1vZA95aN8SMMt2xGRsS47m2U4X6IaS5aAiW8pRMCKL0g\_h4R5xe7LCyyE57KSzJv\_o0k6q62MyAFQU8eD\_LKjhqsc2TpQ5gI6OQNkjpwxPvTwluZW1gF7](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.009.png)

***listen-on port 53 { any; }***

***allow-query        {localhost; dải\_ip\_máy/24; }***

`	`***4.4.	Start và enable dịch vụ***

**[root@mail:~] #systemctl enable named**

**[root@mail:~] #systemctl start named**

`	`***4.5	Tạo rule cho firewall cho phép sử dụng DNS - optional***

***Tắt hẵn firewall:***

**[root@mail:~] #systemctl stop firewalld**

**[root@mail:~] #systemctl disable firewalld**

***OR***

**[root@mail:~] #systemctl enable firewalld**

**[root@mail:~] #systemctl start firewalld**

**firewall-cmd --permanent --zone=public --add-port=443/tcp** 

**firewall-cmd --permanent --zone=public --add-port=3930/tcp**

**firewall-cmd --permanent --zone=public --add-port=110/tcp**

**firewall-cmd --permanent --zone=public --add-port=25/tcp** 

**firewall-cmd --permanent --zone=public --add-port=143/tcp**         

**firewall-cmd --permanent --zone=public --add-port=993/tcp** 	

**firewall-cmd --permanent --zone=public --add-port=389/tcp** 	

**firewall-cmd --permanent --zone=public --add-port=995/tcp** 

**firewall-cmd --permanent --zone=public --add-port=7025/tcp**

**firewall-cmd --permanent --zone=public --add-port=5800/tcp**

**firewall-cmd --permanent --zone=public --add-port=5900/tcp**

**firewall-cmd --permanent --zone=public --add-port=7071/tcp** 	

**firewall-cmd --permanent --zone=public --add-port=3894/tcp**

**firewall-cmd --permanent --zone=public --add-port=3895/tcp**

**firewall-cmd --permanent --zone=public --add-port=80/tcp** 

**firewall-cmd --reload**

***Reload lại rule firewall***

**[root@mail ~] # firewall-cmd --list-all**

***Xem lai cac rule vua dat***

\*	**[root@mail:~] # vi /etc/resolv.conf**

![https://lh3.googleusercontent.com/JuMndwQJAhJ92t-mbaqdmJvO5x4ttewa3q4vWrDw7SNAw\_q52vyacFRAu9\_b4L11DkLuP0ue-H9SqbvNwoR2FRMSG-PBL5S1LPxv\_XpBHVrQeMtkiUZmZ5MGLpwAZu9TJG1G2qwU](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.010.png)

**[root@mail~] #vi /etc/hosts**

**Đoạn này ghi hostname của máy vào.** 

![https://lh6.googleusercontent.com/d\_vjRNDE4bcQrjJE2bAHOM0ThDZMUgwrqZGT7BkAJWVVoieIJazpaYYFvlZUOTKWnPbPFlYlszT3rcqRSTh9dsZLgcFImb6fj1bE1lQWZjA5NQQGnZi7aL7PxLOv7atCvRXqX8nc](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.011.png)

`	`***4.7.	Kiểm tra phân giải tên miền***

***Đoạn mx hỏi hanu.vn do cài đặt trên mail server tên là hanu.vn***

![https://lh4.googleusercontent.com/0Kvi5SoJ\_Ad3S5NW0JBv2PVDNbT8gPyiyf\_Pu7lPdLfuw3otCiLnKnG74ymDbqyqnh3gRBBp2vYVhHn2PbUcDqd5zhSYHVm7tV-gThr30b2JmFOLEqSrXyzN5Pc9k\_NrsA1\_LDbB](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.012.png)

`	`***4.8. disable service***
\*
`	`**[root@mail ~] # systemctl stop postfix**

**[root@mail ~] # systemctl disable postfix**

***		

5. **Cấu hình và cài đặt Mail Zimbra**

***5.1	Download Zimbra CS NE 8 (8.6) về máy client***

**[root@mail~] #cd /**

**[root@mail/] #wget[` `*https://files.zimbra.com/downloads/8.6.0_GA/zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz***](https://files.zimbra.com/downloads/8.6.0_GA/zcs-8.6.0_GA_1153.RHEL7_64.20141215151110.tgz)**

***Ta tiến hành giải nén Zimbra đã tải về trong thư mục setupzimbra***

**[root@mail ~] # cd /**

**[root@mail /] #tar -vxzf zcs-8.6.0\_GA\_1153.RHEL7\_64.20141215151110.tgz**

***5.2 	Cài đặt zimbra***

**[root@mail/] #cd /zcs-8.6.0\_GA\_1153.RHEL7\_64.20141215151110**

**[root@mail tar xzf zcs-8.6.0\_GA\_1153.RHEL7\_64.20141215151110]#./install.sh --platform-override**

***Do you agree the the term of the software license agreement ?***

***=> Ta chọn Y***

***Tiếp tục là yêu cầu lựa chọn các gói để cài đặt. Ta cấu hình như sau :***

***gói zimbra-dnscache chọn N***

![](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.013.png)

***Tiếp tục , ta chọn 6 để vào zimbra-store:***

![https://lh5.googleusercontent.com/AQkKOT6HKT6E9B0HiGL7U3g-19Rty57qbaJd4Bb00c\_4RigtSyiq3cQZM0IkBemUgH129AJBKtwIZkfjZjm-3TerzwxSqKwnPD0vBFDRV-1R5WvdPfrvRGzydHDnsxCs0aoY0OHC](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.014.png)

***Chọn 4 để cài đặt password : 123456a@***

![https://lh6.googleusercontent.com/s8jM8AQV4dsnKhUL\_D9nUfomcOWXnz4PECu4rS6l4rKG\_iu\_3ZbdE4zHWOW3D65WXlTL4-LBeZ6-crJFRMZqBp89aaiqhg\_H1A-Y4u\_JsDtCThb6vRTzRkm1Jm4PujEIAoFAp8-L](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.015.png)

***Làm theo các bước trong hình***

![https://lh4.googleusercontent.com/8WmplCQ1n2LA-4\_mAXtwclqjZX9msVcJ40e8sj-MmVq4H1VlUeWso06nyRTfBTzcIVqLnVHGkxA67u9FfxnXX3g6YlEqfu466eI7ftWLHBO5TpWBhyJx5-vmwHPMM0alK8F33pN9](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.016.png)

***change domain name: N***

***5.3	Kiểm tra trạng thái của service của Mail Zimbra***

***[root@mail~] #su - zimbra***

***[zimbra@mail ~]$ zmcontrol status***

![https://lh3.googleusercontent.com/7N6MAIFXib1B7L2B\_R8iANd6nMZO-m3S1hQwFflG4CuQzK-UOUTfGDyw8yFVkG3j-uv5mNd9B8RvkOHmVL7uXNqhyxUPd0z0v9yF7viRm6GUEZ68n86BVTIJ4HEpS6zF0\_Rpi70J](Aspose.Words.2f762e3f-0d99-4447-8966-231983568cc7.017.png)

***truy cập https:// ip\_máy:7071 - giao diện quản trị zimbra server của admin***

***truy cập https://ip\_máy - giao diện webmail của người dùng. sau khi cài đặt xong, test gửi- nhận mail, nếu gửi nhận thành công là đạt.***

