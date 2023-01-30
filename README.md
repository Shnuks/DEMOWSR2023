<h1>DEMO2023</h1>

<h1>Образец задания</h1>

<p>Образец задания для демонстрационного экзамена по комплекту оценочной документации.</p>

<h1>Описание задания</h1>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/topology.png?raw=true)

<h1>Таблица 1. Характеристики ВМ</h1>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/VM%20Characteristics.png?raw=true)

<h2>Виртуальные машины и коммутация</h2>

<p>Необходимо выполнить создание и базовую конфигурацию виртуальных машин.</p>

<ol>
    <li>На основе предоставленных ВМ или шаблонов ВМ создайте отсутствующие виртуальные машины в соответствии со схемой</li>
    <ul>
      <li>Характеристики ВМ установите в соответствии с Таблицей 1;</li>
      <li>Коммутацию (если таковая не выполнена) выполните в соответствии со схемой сети.</li>
    </ul>
    <li>Имена хостов в созданных ВМ должны быть установлены в соответствии со схемой.</li>
    <li>Адресация должна быть выполнена в соответствии с Таблицей 1;</li>
    <li>Обеспечьте ВМ дополнительными дисками, если таковое необходимо в соответствии с Таблицей 1;</li>
</ol>
<h3>1. На основе предоставленных ВМ или шаблонов ВМ создайте отсутствующие виртуальные машины в соответствии со схемой</h3>
<p>Убедитесь что все ВМ созданы в соотведствии со схемой</P>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/working_vm.png?raw=true)

<h3>2. Имена хостов в созданных ВМ должны быть установлены в соответствии со схемой.</h3>
<h4>ISP</h4>
<pre>hostnamectl set-hostname ISP</pre>
<h4>RTR-L (Debian)</h4>
<pre>hostnamectl set-hostname RTR-L</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>hostname RTR-L</pre>
<h4>RTR-R (Debian)</h4>
<pre>hostnamectl set-hostname RTR-R</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>hostname RTR-R</pre>
<h4>SRV (Debian)</h4>
<pre>hostnamectl set-hostname SRV</pre>
<h4>SRV (Windows Server)</h4>
<pre>Rename-Computer -NewName SRV<br>Restart-Computer</pre>
<h4>WEB-L</h4>
<pre>hostnamectl set-hostname WEB-L</pre>
<h4>WEB-R</h4>
<pre>hostnamectl set-hostname WEB-R</pre>
<h4>CLI</h4>
<pre>Rename-Computer -NewName CLI<br>Restart-Computer</pre>

<h3>3. Адресация должна быть выполнена в соответствии с Таблицей 1.</h3>
<h4>ISP</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim bind9</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 3.3.3.1/24
dns-search demo.wsr<br>   
auto enp0s8
iface enp0s8 inet static
address 4.4.4.1/24<br>
auto enp0s9
iface enp0s9 inet static
address 5.5.5.1/24   
</pre>
<pre>
systemctl restart networking
</pre>
<h4>RTR-L (Debian)</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 4.4.4.100/24
gateway 4.4.4.1<br>
auto enp0s8
iface enp0s8 inet static
address 192.168.100.254/24
dns-search int.demo.wsr
dns-nameservers 192.168.100.200
</pre>
<pre>
systemctl restart networking
</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>
interface Gi1
ip address 4.4.4.100 255.255.255.0
no shutdown
exit<br>
interface Gi2
ip address 192.168.100.254 255.255.255.0
no shutdown
exit
</pre>
<h4>RTR-R (Debian)</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 5.5.5.100/24
gateway 5.5.5.1<br>
auto enp0s8
iface enp0s8 inet static
address 172.16.100.254/24
dns-search int.demo.wsr
dns-nameservers 192.168.100.200
</pre>
<pre>
systemctl restart networking
</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>
interface Gi1
ip address 5.5.5.100 255.255.255.0
no shutdown
exit<br>
interface Gi2
ip address 172.16.100.254 255.255.255.0
no shutdown
exit
</pre>
<h4>SRV (Debian)</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim bind9</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 192.168.100.200/24
gateway 192.168.100.254
dns-search int.demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>SRV (Windows Server)</h4>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SRV_addressing.png?raw=true)

<h4>WEB-L</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 192.168.100.100/24
gateway 192.168.100.254
dns-nameservers 192.168.100.200
dns-search int.demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>WEB-R</h4>
<p>подключить debian-11.6.0-amd64-BD-1</P>
<pre>apt-cdrom add<br>apt install -y vim</pre>
<pre>
vim /etc/network/interfaces<br>    
auto enp0s3
iface enp0s3 inet static
address 172.16.100.100/24
gateway 172.16.100.254
dns-nameservers 192.168.100.200
dns-search int.demo.wsr
</pre>
<pre>
systemctl restart networking
</pre>
<h4>CLI</h4>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/CLI_addressing.png?raw=true)

<h3>4. Обеспечьте ВМ дополнительными дисками, если таковое необходимо в соответствии с Таблицей 1.</h3>
<h4>SRV</h4>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SRV_disks.png?raw=true)

<h2>Сетевая связность</h2>

<p>В рамках данного модуля требуется обеспечить сетевую связность между регионами работы приложения, а также обеспечить выход ВМ в имитируемую сеть “Интернет”.</p>

<ol>
    <li>Сети, подключенные к ISP, считаются внешними: </li>
    <ul><li>Запрещено прямое попадание трафика из внутренних сетей во внешние и наоборот;</li></ul>
    <li>Платформы контроля трафика, установленные на границах регионов, должны выполнять трансляцию трафика, идущего из соответствующих внутренних сетей во внешние сети стенда и в сеть Интернет.</li>
    <ul><li>Трансляция исходящих адресов производится в адрес платформы,расположенный во внешней сети.</li></ul>
    <li>Между платформами должен быть установлен защищенный туннель, позволяющий осуществлять связь между регионами с применением внутренних адресов.</li>
    <ul>
    <li>Трафик, проходящий по данному туннелю, должен быть защищен: </li>
    <ul><li>Платформа ISP не должна иметь возможности просматривать содержимое пакетов, идущих из одной внутренней сети в другую.</li></ul>
    <li>Туннель должен позволять защищенное взаимодействие между платформами управления трафиком по их внутренним адресам </li>
    <ul><li>Взаимодействие по внешним адресам должно происходит без применения туннеля и шифрования</li></ul>
    <li>Трафик, идущий по туннелю между регионами по внутренним адресам, не должен транслироваться.</li>
    </ul>
    <li>Платформа управления трафиком RTR-L выполняет контроль входящего трафика согласно следующим правилам: </li>
    <ul>
    <li>Разрешаются подключения к портам DNS, HTTP и HTTPS для всех клиентов; </li>
    <ul><li>Порты необходимо для работы настраиваемых служб</li></ul>
    <li>Разрешается работа выбранного протокола организации защищенной связи; </li>
    <ul><li>Разрешение портов должно быть выполнено по принципу “необходимо и достаточно”</li></ul>
    <li>Разрешается работа протоколов ICMP;</li>
    <li>Разрешается работа протокола SSH;</li>
    <li>Прочие подключения запрещены;</li>
    <li>Для обращений в платформам со стороны хостов, находящихся внутри регионов, ограничений быть не должно;</li>
    </ul>
    <li>Платформа управления трафиком RTR-R выполняет контроль входящего трафика согласно следующим правилам: </li>
    <ul>
    <li>Разрешаются подключения к портам HTTP и HTTPS для всех клиентов; </li>
    <ul><li>Порты необходимо для работы настраиваемых служб</li></ul>
    <li>Разрешается работа выбранного протокола организации защищенной связи; </li>
    <ul><li>Разрешение портов должно быть выполнено по принципу “необходимо и достаточно”</li></ul>
    <li>Разрешается работа протоколов ICMP;</li>
    <li>Разрешается работа протокола SSH;</li>
    <li>Прочие подключения запрещены;</li>
    <li>Для обращений в платформам со стороны хостов, находящихся внутри регионов, ограничений быть не должно;</li>
    </ul>
    <li>Обеспечьте настройку служб SSH региона Left: </li>
    <ul>
    <li>Подключения со стороны внешних сетей по протоколу к платформе управления трафиком RTR-L на порт 2222 должны быть перенаправлены на ВМ Web-L;</li>
    <li>Подключения со стороны внешних сетей по протоколу к платформе управления трафиком RTR-L на порт 2244 должны быть перенаправлены на ВМ Web-R;</li>
    </ul>
</ol>
<h3>1. Сети, подключенные к ISP, считаются внешними</h3>
<h4>ISP</h4>
<pre>systemctl disable --now apparmor<br>echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf<br>sysctl -p</pre>
<h4>RTR-L (Debian)</h4>
<pre>echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf<br>sysctl -p</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>ip route 0.0.0.0 0.0.0.0 4.4.4.1</pre>
<h4>RTR-R (Debian)</h4>
<pre>echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf<br>sysctl -p</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>ip route 0.0.0.0 0.0.0.0 5.5.5.1</pre>
<h3>2. Платформы контроля трафика, установленные на границах регионов, должны выполнять трансляцию трафика, идущего из соответствующих внутренних сетей во внешние сети стенда и в сеть Интернет.</h3>
<h4>RTR-L (Debian)</h4>
<pre>apt install -y firewalld<br>systemctl disable --now apparmor</pre>
<pre>firewall-cmd --permanent --zone=dmz --add-interface=enp0s3<br>firewall-cmd --permanent --zone=dmz --add-masquerade<br>firewall-cmd --permanent --zone=trusted --add-interface=enp0s8<br>firewall-cmd --reload</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>access-list 1 permit 192.168.100.0 0.0.0.255<br>ip nat inside source list 1 interface Gi1 overload</pre>
<pre>interface Gi1<br>ip nat outside<br>exit<br>interface Gi2<br>ip nat inside<br>exit</pre>
<h4>RTR-R (Debian)</h4>
<pre>apt install -y firewalld<br>systemctl disable --now apparmor</pre>
<pre>firewall-cmd --permanent --zone=dmz --add-interface=enp0s3<br>firewall-cmd --permanent --zone=dmz --add-masquerade<br>firewall-cmd --permanent --zone=trusted --add-interface=enp0s8<br>firewall-cmd --reload</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>access-list 1 permit 172.16.100.0 0.0.0.255<br>ip nat inside source list 1 interface Gi1 overload</pre>
<pre>interface Gi1<br>ip nat outside<br>exit<br>interface Gi2<br>ip nat inside<br>exit</pre>
<h3>3. Между платформами должен быть установлен защищенный туннель, позволяющий осуществлять связь между регионами с применением внутренних адресов.</h3>
<h4>RTR-L (Debian)</h4>
<pre>apt install -y wireguard</pre>
<pre>mkdir /etc/wireguard/keys<br>cd /etc/wireguard/keys<br>wg genkey | tee srv-sec.key | wg pubkey > srv-pub.key<br>wg genkey | tee cli-sec.key | wg pubkey > cli-pub.key</pre>
<pre>cat srv-sec.key cli-pub.key >> /etc/wireguard/wg0.conf<br>vim /etc/wireguard/wg0.conf<br>
[Interface]
Address = 10.20.30.1/30
ListenPort = 12345
PrivateKey = "id_srv-sec.key"<br>
[Peer]
PublicKey = "id_cli-pub.key"
AllowedIPs = 10.20.30.0/30, 172.16.100.0/24
</pre>
<pre>systemctl enable --now wg-quick@wg0</pre>
<pre>vim /etc/ssh/sshd_config<br>...<br>PermitRootLogin yes<br>...</pre>
<pre>systemctl restart sshd</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>
interface Tunnel1
ip address 10.20.30.1 255.255.255.252
tunnel mode gre ip
tunnel source 4.4.4.100
tunnel destination 5.5.5.100
</pre>
<pre>
router bgp 65001
neighbor 10.20.30.2 remote-as 65002
network 10.20.30.0 mask 255.255.255.252
network 192.168.100.0 mask 255.255.255.0
</pre>
<pre>
crypto isakmp policy 1
encryption aes
authentication pre-share
hash sha256
group14
exit<br>
crypto isakmp key P@ssw0rd address 5.5.5.100
crypto isakmp nat keepalive 5<br>
crypto ipsec transform-set TSET  esp-aes 256 esp-sha256-hmac
mode tunnel
exit<br>
crypto ipsec profile VTI
set transform-set TSET
exit
</pre>
<pre>
interface Tunnel1
tunnel mode ipsec ipv4
tunnel protection ipsec profile VTI
</pre>
<h4>RTR-R (Debian)</h4>
<pre>apt install -y wireguard</pre>
<pre>
mkdir /etc/wireguard/keys
cd /etc/wireguard/keys
scp root@4.4.4.100:/etc/wireguard/cli-sec.key ./
scp root@4.4.4.100:/etc/wireguard/srv-pub.key ./
</pre>
<pre>
cat cli-sec.key srv-pub.key >> /etc/wireguard/wg0.conf
vim /etc/wireguard/wg0.conf<br>
[Interface]
Address = 10.20.30.2/30
PrivateKey = "id_cli-sec.key"<br>
[Peer]
PublicKey = "id_srv-pub.key"
Endpoint = 4.4.4.100:12345
AllowedIPs = 10.20.30.0/30, 192.168.100.0/24
PersistentKeepalive = 10
</pre>
<pre>systemctl enable --now wg-quick@wg0</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>
interface Tunnel1
ip address 10.20.30.2 255.255.255.252
tunnel mode gre ip
tunnel source 5.5.5.100
tunnel destination 4.4.4.100
</pre>
<pre>
router bgp 65002
neighbor 10.20.30.1 remote-as 65001
network 10.20.30.0 mask 255.255.255.252
network 172.16.100.0 mask 255.255.255.0
</pre>
<pre>
crypto isakmp policy 1
encryption aes
authentication pre-share
hash sha256
group14
exit<br>
crypto isakmp key P@ssw0rd address 4.4.4.100
crypto isakmp nat keepalive 5<br>
crypto ipsec transform-set TSET  esp-aes 256 esp-sha256-hmac
mode tunnel
exit<br>
crypto ipsec profile VTI
set transform-set TSET
exit
</pre>
<pre>
interface Tunnel1
tunnel mode ipsec ipv4
tunnel protection ipsec profile VTI
</pre>
<h3>4. Платформа управления трафиком RTR-L выполняет контроль входящего трафика согласно следующим правилам:</h3>
<h4>RTR-L (Debian)</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-service={http,https,dns,ssh,ntp}
firewall-cmd --permanent --zone=dmz --add-port={53,123}/{tcp,udp}
firewall-cmd --permanent --zone=dmz --add-port=12345/{tcp,udp}
firewall-cmd --permanent --zone=trusted --add-service=ntp
firewall-cmd --permanent --zone=internal --add-interface=wg0
firewall-cmd --permanent --zone=internal --add-port={443,53,123}/tcp
firewall-cmd --permanent --zone=internal --add-port={53,123}/udp
firewall-cmd --permanent --zone=internal --add-service={mdns,ssh,ntp,samba-client}
firewall-cmd --reload
</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>
ip access-list extended LEFT<br>
permit tcp any any established
permit udp host 4.4.4.100 eq 53 any
permit udp host 5.5.5.1 eq 123 any
permit tcp any host 4.4.4.100 eq 80 
permit tcp any host 4.4.4.100 eq 443 
permit tcp any host 4.4.4.100 eq 2222
permit udp host 5.5.5.100 host 4.4.4.100 eq 500
permit esp any any
permit icmp any any
</pre>
<pre>
interface Gi1 
ip access-group LEFT in
</pre>
<h3>5. Платформа управления трафиком RTR-R выполняет контроль входящего трафика согласно следующим правилам:</h3>
<h4>RTR-R (Debian)</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-service={dns,http,https,ntp,ssh}
firewall-cmd --permanent --zone=dmz --add-port={53,123}/{tcp,udp}
firewall-cmd --permanent --zone=trusted --add-service=ntp
firewall-cmd --permanent --zone=internal --add-interface=wg0
firewall-cmd --permanent --zone=internal --add-port={443,53,123}/tcp
firewall-cmd --permanent --zone=internal --add-port={53,123}/udp
firewall-cmd --permanent --zone=internal --add-service={mdns,ssh,ntp,samba-client}
firewall-cmd --reload
</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>
ip access-list extended RIGHT<br>
permit tcp any any established
permit tcp any host 5.5.5.100 eq 80 
permit tcp any host 5.5.5.100 eq 443 
permit tcp any host 5.5.5.100 eq 2244 
permit udp host 4.4.4.100 host 5.5.5.100 eq 500
permit esp any any
permit icmp any any
</pre>
<pre>
interface Gi1 
ip access-group RIGHT in
</pre>
<h3>6. Обеспечьте настройку служб SSH региона Left:</h3>
<h4>RTR-L (Debian)</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=2222:proto=tcp:toport=22:toaddr=192.168.100.100
firewall-cmd --reload
</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>ip nat inside source static tcp 192.168.100.100 22 4.4.4.100 2222</pre>
<h4>RTR-R (Debian)</h4>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=2244:proto=tcp:toport=22:toaddr=172.16.100.100
firewall-cmd --reload
</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>ip nat inside source static tcp 172.16.100.100 22 5.5.5.100 2244</pre>
<h4>WEB-L</h4>
<pre>
vim /etc/ssh/sshd_config
...
PermitRootLogin yes
...
</pre>
<pre>systemctl restart sshd</pre>
<h4>WEB-R</h4>
<pre>
vim /etc/ssh/sshd_config
...
PermitRootLogin yes
...
</pre>
<pre>systemctl restart sshd</pre>

<h2>Инфраструктурные службы</h2>

<p>В рамках данного модуля необходимо настроить основные инфраструктурные службы и настроить представленные ВМ на применение этих служб для всех основных функций.</p>

<ol>
    <li>Выполните настройку первого уровня DNS-системы стенда: </li>
    <ul>
        <li>Используется ВМ ISP;</li>
        <li>Обслуживается зона demo.wsr</li>
        <ul><li>Наполнение зоны должно быть реализовано в соответствии с Таблицей 2;</li></ul>
        <li>Сервер делегирует зону int.demo.wsr на SRV; </li>
        <ul>
            <li>Поскольку SRV находится во внутренней сети западного региона, делегирование происходит на внешний адрес маршрутизатора данного региона.</li>
            <li>Маршрутизатор региона должен транслировать соответствующие порты DNS-службы в порты сервера SRV</li>
        </ul>
        <li>Внешний клиент CLI должен использовать DNS-службу, развернутую на ISP, по умолчанию;</li>
    </ul>
    <li>Выполните настройку второго уровня DNS-системы стенда; </li>
    <ul>
    <li>Используется ВМ SRV;</li>
    <li>Обслуживается зона int.demo.wsr; </li>
    <ul><li>Наполнение зоны должно быть реализовано в соответствии с Таблицей 2;</li></ul>
    <li>Обслуживаются обратные зоны для внутренних адресов регионов</li>
    <ul><li>Имена для разрешения обратных записей следует брать из Таблицы 2;</li></ul>
    <li>Сервер принимает рекурсивные запросы, исходящие от адресов внутренних регионов; </li>
    <ul><li>Обслуживание клиентов(внешних и внутренних), обращающихся к к зоне int.demo.wsr, должно производится без каких либо ограничений по адресу источника;</li></ul>
    <li>Внутренние хосты регионов (равно как и платформы управления трафиком) должны использовать данную DNS-службу для разрешения всех запросов имен;</li>
    </ul>
    <li>Выполните настройку первого уровня системы синхронизации времени:</li>
    <ul>
    <li>Используется сервер ISP.</li>
    <li>Сервер считает собственный источник времени верным, stratum=4;</li>
    <li>Сервер допускает подключение только через внешний адрес соответствующей платформы управления трафиком; </li>
    <ul><li>Подразумевается обращение SRV для синхронизации времени;</li></ul>
    <li>Клиент CLI должен использовать службу времени ISP;</li>
    </ul>
    <li>Выполните конфигурацию службы второго уровня времени на SRV </li>
    <ul>
    <li>Сервер синхронизирует время с хостом ISP; </li>
    <ul><li>Синхронизация с другими источникам запрещена;</li></ul>
    <li>Сервер должен допускать обращения внутренних хостов регионов, в том числе и платформ управления трафиком, для синхронизации времени;</li>
    <li>Все внутренние хосты(в том числе и платформы управления трафиком) должны синхронизировать свое время с SRV;</li>
    </ul>
    <li>Реализуйте файловый SMB-сервер на базе SRV</li>
    <ul>
    <li>Сервер должен предоставлять доступ для обмена файлами серверам WEB-L и WEB-R;</li>
    <li>Сервер, в зависимости от ОС, использует следующие каталоги для хранения файлов:</li>
    <ul>
        <li>/mnt/storage для система на базе Linux;</li>
        <li>Диск R:\ для систем на базе Windows;</li>
    </ul>
    <li>Хранение файлов осуществляется на диске (смонтированном по указанным выше адресам), реализованном по технологии RAID типа “Зеркало”;</li>
    </ul>
    <li>Сервера WEB-L и WEB-R должны использовать службу, настроенную на SRV, для обмена файлами между собой:</li>
    <ul>
    <li>Служба файлового обмена должна позволять монтирование в виде стандартного каталога Linux</li>
    <ul><li>Разделяемый каталог должен быть смонтирован по адресу /opt/share;</li></ul>
    <li>Каталог должен позволять удалять и создавать файлы в нем для всех пользователей;</li>
    </ul>
    <li>Выполните настройку центра сертификации на базе SRV: </li>
    <ul>
    <li>В случае применения решения на базе Linux используется центр сертификации типа OpenSSL и располагается по адресу /var/ca</li>
    <li>Выдаваемые сертификаты должны иметь срок жизни не менее 500 дней;</li>
    <li>Параметры выдаваемых сертификатов: </li>
    <ul>
        <li>Страна RU;</li>
        <li>Организация DEMO.WSR;</li>
        <li>Прочие поля (за исключением CN) должны быть пусты;</li>
    </u>
    </ul>
</ol>

<h1>Таблица 2. DNS-записи зон</h1>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/table_dns.png?raw=true)

<h3>1. Выполните настройку первого уровня DNS-системы стенда:</h3>
<h4>ISP</h4>
<pre>
mkdir /opt/dns
cp /etc/bind/db.local /opt/dns/demo.db
chown -R bind:bind /opt/dns
</pre>
<pre>
vim /etc/bind/named.conf.options
options {
            directory "/var/cache/bind";
            dnssec-validation no;
            allow-query { any; };
            listen-on-v6 { any; };
        };
</pre>
<pre>
vim /etc/bind/named.conf.default-zones
zone "demo.wsr" {
            type master;
            allow-transfer { any; };
            file "/opt/dns/demo.db";
        };
</pre>
<pre>
vim /opt/dns/demo.db
</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/demo.db.png?raw=true)

<pre>systemctl restatr bind9</pre>

<ul><ul><li>Маршрутизатор региона должен транслировать соответствующие порты DNS-службы в порты сервера SRV.</li></ul></ul>
<h4>RTR-L (Debian)</h4>
<pre>firewall-cmd --permanent --zone=dmz --add-forward-port=port=53:proto={tcp,udp}:toport=53:toaddr=192.168.100.200<br>firewall-cmd --reload</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>ip nat inside source static tcp 192.168.100.200 53 4.4.4.100 53<br>ip nat inside source static udp 192.168.100.200 53 4.4.4.100 53</pre>
<h3>2. Выполните настройку второго уровня DNS-системы стенда;</h3>
<h4>SRV (Debian)</h4>
<pre>systemctl disable --now apparmor</pre>
<pre>
mkdir /opt/dns
cp /etc/bind/db.local /opt/dns/int.demo.db
cp /etc/bind/db.127 /opt/dns/100.168.192.in-addr.arpa.db
cp /etc/bind/db.127 /opt/dns/100.16.172.in-addr.arpa.db
chown -R bind:bind /opt/dns
</pre>
<pre>
vim /etc/bind/named.conf.options<br>
options {
            directory "/var/cache/bind";
            dnssec-validation no;
            allow-query { any; };
            listen-on-v6 { any; };
        };
</pre>
<pre>
vim /etc/bind/named.conf.default-zones<br>
zone "int.demo.wsr" {
    type master;
    allow-transfer { any; };
    file "/opt/dns/int.demo.db";
};<br>
zone "100.168.192.in-addr.arpa" {
    type master;
    allow-transfer { any; };
    file "/opt/dns/100.168.192.in-addr.arpa.db";
};<br>
zone "100.16.172.in-addr.arpa" {
    type master;
    allow-transfer { any; };
    file "/opt/dns/100.16.172.in-addr.arpa.db";
};
</pre>
<pre>vim /opt/dns/int.demo.db</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/int_demo_db.png?raw=true)

<pre>vim /opt/dns/100.168.192.in-addr.arpa.db</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/arpa_1.png?raw=true)

<pre>vim /opt/dns/100.16.172.in-addr.arpa.db</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/arpa_2.png?raw=true)

<pre>systemctl restatr bind9</pre>
<h4>SRV (Windows Server)</h4>
<pre>Install-WindowsFeature -Name DNS -IncludeManagementTools</pre>
<pre>Add-DnsServerPrimaryZone -Name "int.demo.wsr" -ZoneFile "int.demo.wsr.dns"</pre>
<pre>
Add-DnsServerPrimaryZone -NetworkId 192.168.100.0/24 -ZoneFile "int.demo.wsr.dns"
Add-DnsServerPrimaryZone -NetworkId 172.16.100.0/24 -ZoneFile "int.demo.wsr.dns"
</pre>
<pre>
Add-DnsServerResourceRecordA -Name "web-l" -ZoneName "int.demo.wsr" -AllowUpdateAny -IPv4Address "192.168.100.100" -CreatePtr 
Add-DnsServerResourceRecordA -Name "web-r" -ZoneName "int.demo.wsr" -AllowUpdateAny -IPv4Address "172.16.100.100" -CreatePtr 
Add-DnsServerResourceRecordA -Name "srv" -ZoneName "int.demo.wsr" -AllowUpdateAny -IPv4Address "192.168.100.200" -CreatePtr 
Add-DnsServerResourceRecordA -Name "rtr-l" -ZoneName "int.demo.wsr" -AllowUpdateAny -IPv4Address "192.168.100.254" -CreatePtr 
Add-DnsServerResourceRecordA -Name "rtr-r" -ZoneName "int.demo.wsr" -AllowUpdateAny -IPv4Address "172.16.100.254" -CreatePtr
</pre>
<pre>
Add-DnsServerResourceRecordCName -Name "ntp" -HostNameAlias "srv.int.demo.wsr" -ZoneName "int.demo.wsr"
Add-DnsServerResourceRecordCName -Name "dns" -HostNameAlias "srv.int.demo.wsr" -ZoneName "int.demo.wsr"
</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/int.demo.wsr.db.png?raw=true)

<ul><ul><li>Внутренние хосты регионов (равно как и платформы управления трафиком) должны использовать данную DNS-службу для разрешения всех запросов имен;</li></ul></ul>
<h4>RTR-L (Cisco CSR)</h4>
<pre>
ip name-server 192.168.100.200
ip domain name int.demo.wsr
</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>
ip name-server 192.168.100.200
ip domain name int.demo.wsr
</pre>
<h3>3. Выполните настройку первого уровня системы синхронизации времени:</h3>
<h4>ISP</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server 127.0.0.1 iburst prefer
hwtimestamp *
local stratum 4
allow 4.4.4.0/24
allow 3.3.3.0/24
</pre>
<pre>systemctl restart chronyd</pre>
<ul><ul><li>Клиент CLI должен использовать службу времени ISP;</li></ul></ul>
<h4>CLI</h4>
<pre>New-NetFirewallRule -DisplayName "NTP" -Direction Inbound -LocalPort 123 -Protocol UDP -Action Allow</pre>
<pre>
Start-Service W32Time
w32tm /config /manualpeerlist:3.3.3.1 /syncfromflags:manual /reliable:yes /update
Restart-Service W32Time
</pre>
<pre>Set-Service -Name W32Time -StartupType Automatic</pre>
<h3>4. Выполните конфигурацию службы второго уровня времени на SRV:</h3>
<h4>SRV (Debian)</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server 4.4.4.1 iburst prefer
allow 192.168.100.0/24
allow 172.16.100.0/24
allow 10.20.30.0/30
</pre>
<pre>systemctl restart chronyd</pre>
<h4>SRV (Windows Server)</h4>
<pre>New-NetFirewallRule -DisplayName "NTP" -Direction Inbound -LocalPort 123 -Protocol UDP -Action Allow</pre>
<pre>
w32tm /query /status
Start-Service W32Time
w32tm /config /manualpeerlist:4.4.4.1 /syncfromflags:manual /reliable:yes /update
Restart-Service W32Time
</pre>
<ul><ul><li>Все внутренние хосты(в том числе и платформы управления трафиком) должны синхронизировать свое время с SRV;</li></ul></ul>
<h4>RTR-L (Debian)</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server ntp.int.demo.wsr iburst prefer
allow 192.168.100.0/24
</pre>
<pre>systemctl restart chronyd</pre>
<h4>RTR-L (Cisco CSR)</h4>
<pre>ntp server ntp.int.demo.wsr</pre>
<h4>RTR-R (Debian)</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server ntp.int.demo.wsr iburst prefer
allow 172.16.100.0/24
</pre>
<pre>systemctl restart chronyd</pre>
<h4>RTR-R (Cisco CSR)</h4>
<pre>ntp server ntp.int.demo.wsr</pre>
<h4>WEB-L</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server ntp.int.demo.wsr iburst prefer
allow 192.168.100.0/24
</pre>
<pre>systemctl restart chronyd</pre>
<h4>WEB-R</h4>
<pre>apt install -y chrony</pre>
<pre>
vim /etc/chrony/chrony.conf<br>
#pool 2.debian.pool.ntp.org iburst
server ntp.int.demo.wsr iburst prefer
allow 172.16.100.0/24
</pre>
<pre>systemctl restart chronyd</pre>
<h3>5. Реализуйте файловый SMB-сервер на базе SRV</h3>
<h4>SRV (Debian)</h4>
<pre>apt install -y mdadm</pre>
<pre>
mdadm --zero-superblock --force /dev/sd{b,c}
wipefs --all --force /dev/sd{b,c}
mdadm --create --verbose /dev/md1 -l 1 -n 2 /dev/sd{b,c}
mkfs.ext4 /dev/md1
</pre>
<pre>
mkdir /mnt/storage
chmod 777 /mnt/storage
echo /dev/md1 /mnt/storage ext4 defaults 1 2 >> /etc/fstab
mount -a
</pre>
<pre>apt install -y samba</pre>
<pre>vim /etc/samba/smb.conf</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/smb.conf.png?raw=true)

<pre>systemctl restart smbd</pre>
<h4>SRV (Windows Server)</h4>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/RAID1_1.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/RAID1_2.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/RAID1_3.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/RAID1_4.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_1.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_2.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_3.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_4.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_5.png?raw=true)

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/SMB_6.png?raw=true)

<h3>6. Сервера WEB-L и WEB-R должны использовать службу, настроенную на SRV, для обмена файлами между собой:</h3>
<h4>WEB-L</h3>
<pre>apt install -y cifs-utils</pre>
<pre>
mkdir /opt/share
chmod 777 /opt/share
echo //srv.int.demo.wsr/share /opt/share cifs guest 0 0 >> /etc/fstab
mount -a
</pre>
<h4>WEB-R</h3>
<pre>apt install -y cifs-utils</pre>
<pre>
mkdir /opt/share
chmod 777 /opt/share
echo //srv.int.demo.wsr/share /opt/share cifs guest 0 0 >> /etc/fstab
mount -a
</pre>
<h3>7. Выполните настройку центра сертификации на базе SRV:</h3>
<h4>SRV (Debian)</h4>
<pre>
mkdir /var/ca
cd /var/ca
</pre>
<pre>openssl req -newkey rsa:4096 -keyform PEM -keyout ca.key -x509 -days 3650 -outform PEM -out ca.cer</pre>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/Root_CA.png?raw=true)

<h4>SRV (Windows Server)</h4>
<pre>
Install-WindowsFeature -Name AD-Certificate, ADCS-Web-Enrollment -IncludeManagementTools<br>
Install-AdcsCertificationAuthority -CAType StandaloneRootCa -CACommonName "Demo.wsr" -force<br>
Install-AdcsWebEnrollment -Confirm -force<br>
New-SelfSignedCertificate -subject "localhost"<br> 
Get-ChildItem cert:\LocalMachine\My<br>
Move-item Cert:\LocalMachine\My\XFX2DX02779XFD1F6F4X8435A5X26ED2X8DEFX95 -destination Cert:\LocalMachine\Webhosting\<br>
New-IISSiteBinding -Name 'Default Web Site' -BindingInformation "*:443:" -Protocol htts -CertificateThumbPrint XFX2DX02779XFD1F6F4X8435A5X26ED2X8DEFX95 <br>
Start-WebSite -Name "Default Web Site"<br>
Get-CACrlDistributionPoint | Remove-CACrlDistributionPoint -force<br>
Get-CAAuthorityInformationAccess |Remove-CAAuthorityInformationAccess -force<br>
Get-CAAuthorityInformationAccess |Remove-CAAuthorityInformationAccess -force<br>
Restart-Service CertSrv
</pre>

<h2>Инфраструктура веб-приложения.</h2>

<p>Данный блок подразумевает установку и настройку доступа к веб-приложению, выполненному в формате контейнера Docker</p>

<ol>
<li>Образ Docker (содержащий веб-приложение) расположен на ISO-образе дополнительных материалов; <li>
<ul><li>Выполните установку приложения AppDocker0; </li></ul>
<li>Пакеты для установки Docker расположены на дополнительном ISO-образе;</li>
<li>Инструкция по работе с приложением расположена на дополнительном ISO-образе;</li>
<li>Необходимо реализовать следующую инфраструктуру приложения. </li>
<ul>
<li>Клиентом приложения является CLI (браузер Edge);</li>
<li>Хостинг приложения осуществляется на ВМ WEB-L и WEB-R;</li>
<li>Доступ к приложению осуществляется по DNS-имени www.demo.wsr; </li>
    <ul>
        <li>Имя должно разрешаться во “внешние” адреса ВМ управления трафиком в обоих регионах;</li>
        <li>При необходимости, для доступа к к приложению допускается реализовать реверс-прокси или трансляцию портов;</li>
    </ul>
<li>Доступ к приложению должен быть защищен с применением технологии TLS; </li>
<ul><li>Необходимо обеспечить корректное доверие сертификату сайта, без применения “исключений” и подобных механизмов;</li></ul>
<li>Незащищенное соединение должно переводится на защищенный канал автоматически;</li>
</ul>
<li>Необходимо обеспечить отказоустойчивость приложения; </li>
<ul>
<li>Сайт должен продолжать обслуживание (с задержкой не более 25 секунд) в следующих сценариях: </li>
    <ul>
        <li>Отказ одной из ВМ Web</li>
        <li>Отказ одной из ВМ управления трафиком.</li>
    </ul>
</ul>
</ol>
<h3>1. Образ Docker (содержащий веб-приложение) расположен на ISO-образе дополнительных материалов;</h3>
<p>подключить docker-new.iso</p>

![Image alt](https://github.com/NewErr0r/DEMO39WSI/blob/main/images/docker_cdrom.png?raw=true)

<h4>WEB-L</h4>
<pre>apt-cdrom add</pre>
<h4>WEB-R</h4>
<pre>apt-cdrom add</pre>
<h3>2. Пакеты для установки Docker расположены на дополнительном ISO-образе;</h3>
<h4>WEB-L</h4>
<pre>
apt install -y docker-ce
systemctl enable --now docker
</pre>
<pre>
mkdir /mnt/app
mount /dev/sr1 /mnt/app
docker load < /mnt/app/app.tar
</pre>
<pre>
docker images
docker run --name app  -p 8080:80 -d app
docker ps
</pre>
<h4>WEB-R</h4>
<pre>
apt install -y docker-ce
systemctl enable --now docker
</pre>
<pre>
mkdir /mnt/app
mount /dev/sr1 /mnt/app
docker load < /mnt/app/app.tar
</pre>
<pre>
docker images
docker run --name app  -p 8080:80 -d app
docker ps
</pre>
<h3>RTR-L (Debian)</h3>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=80:proto=tcp:toport=80:toaddr=192.168.100.100
firewall-cmd --permanent --zone=dmz --add-forward-port=port=443:proto=tcp:toport=443:toaddr=192.168.100.100
firewall-cmd --reload
</pre>
<h3>RTR-L (Cisco CSR)</h3>
<pre>no ip http secure-server<br>
ip nat inside source static tcp 192.168.100.100 80 4.4.4.100 80 
ip nat inside source static tcp 192.168.100.100 443 4.4.4.100 443 
</pre>
<h3>RTR-R (Debian)</h3>
<pre>
firewall-cmd --permanent --zone=dmz --add-forward-port=port=80:proto=tcp:toport=80:toaddr=172.16.100.100
firewall-cmd --permanent --zone=dmz --add-forward-port=port=443:proto=tcp:toport=443:toaddr=172.16.100.100
firewall-cmd --reload
</pre>
<h3>RTR-R (Cisco CSR)</h3>
<pre>no ip http secure-server<br>
ip nat inside source static tcp 172.16.100.100 80 5.5.5.100 80 
ip nat inside source static tcp 172.16.100.100 443 5.5.5.100 443 
</pre>
<h3>4. Необходимо реализовать следующую инфраструктуру приложения</h3>
