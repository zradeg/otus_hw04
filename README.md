# Bash, awk, sed, grep � ������

�.�. ���������� � �������� ������� ����������� nginx, ������� ��� �� �������� ���� �� ������ ��������� � ����, �� ������������ ������������ � ���������� �� ���� ���� (access-4560-644067.log). ��� ������������ ����� ������ ������� (logchecker.sh) ���������� ����������� ���������� ����, ����� ��� ������ ������� ��� ��������� ��������, ���������� ������� ����� ��������� ��� �������� ���� � ����������� ������������. ������� ���� ������ ����������� �������� ���������� ����, ��������� ���������� ���������������� ������ �� ������������� ����� � ������� �� � ���, ������� ����� ��������� logchecker. ����� �������, ������ �������� ����������� ���� ��������: ��������� - logchecker.sh � ���������������� - emul_log_writer.sh. ��� ������� ����������� ������, �� �� ������������, � � ��������� ��������� �� �������, ����� � ��������� ������� ���� ����������� ������������� �������� ���������� ���������.

## ���������� � crontab
� crontab ������� ��� �������� ������ ��������:
1. ���������� �������� �����, ������ ���������� ��� � ��� ������. ���������� ��� � ��� ������.
2. ��� ��������� � �������: ������ ���� ���������� � ����� ������ ������� ����. ���������� ���������� ��� � 58 �����.
��� ��������� ������� ������� ������ �����, ����� ������ ����� ���� �������������� � ���������� ������.

## �������� ��������� �������� �������
������� ����������� �������� �������� /vagrant/script � ��� �������:
* logchecker.sh - ����������� ���� �������
* emul_log_writing.sh - ������, ����������� ���� ����
* fixline.log - ������ ����� ��������� ��������� ������ ��� emul_log_writing.sh
* lastline.log - ������ ����� ��������� ��������� ������ ��� logchecker.sh
* lastdate.txt - ������ ��������� ������� ������� ��� logchecker.sh
* last_message.txt - ������ ��������� �����, ������������ logchecker.sh �� �����
* mail_addr - �������� �������� �����, ���� ����� ������������ ������
##### ������������ ���������, ������� ���������� ��������� ������� ����� �������� �������� �������
- ��� ������ ����� �����, �� ������� ����� ������������ ������. ��������� �������� ���:
`MAILADDR=mail@domain.com`
���� mail_addr ��� �������� �������� � ���� �����, ��������� ������ ������ ����� ����� ����� ����� �����.
�� ������ ������� ������� ����� ��� ������ ���� ��������, ������� ������������� ������� ��� �� �������� ���������.

## �������� ��������� �������
#### ����������:
* IP_PATTERN - ������ ���������� ��������� ��� ��������� IP-������
* PIDFILE - ���� � ����� PID.
* LOGFILE - ���� � ����
* MSG - ���� � �����, � ������� ����������� ����� ��� ����������� ��������
* READ_ITER - ������ ������ ����, �������������� �������� � ������ ��������
* LAST_LINE_STORE - ���� � �����, ��� �������� ����� ��������� ������, ��������� � ��������� ��������
* LAST_LINE - ����������, �������� ����� ��������� ������ �������� �� ���������� ��������, �������� � ����� LAST_LINE_STORE
* LASTDATE - ������ ���� ��������� ��������
* TOTAL_LINES - ������ ����� ����� ������������ � ���� � ������� ��������.
* MAILADDR - ������ ����� ����������, ���� ����� ���������� ������. ����� � ����� mail_addr.

#### �������
* check_PID - ��������� ������� PID-����� ��� �������
* put_PID - ������� PID-����
* kill_PID_on_exit
* check_actual_accesslog - ��������� ������� ������ �������� � ������� ������ � ���. � ������ ��������� ���� ��� �������, ���������� ��������������� ��������� �� �����
* tail_from_last_line - �������� ���� ����� ���� �� ��������� ������ ����������� � ���������� ��������, �� ��������� ������.
* save_last_line - �������� ������� ���������� ����� � �������� � ���������� LAST_LINE � ��������� � ���� LAST_LINE_STORE
* most_frequent_client_IP - �������� 10 �������� ������ ip �����������
* most_frequent_URL - �������� ���������� ��������� ������������ URL
* all_errors - �������� ������ 4�� � 5��
* all_responses - �������� ���������� �������
* rotate_date - ��������� ���� �������� ������� ������� � LASTDATE
* make_letter - ���������� ������ ���� ������ ��� ����������� �������� ������ ������� most_frequent_client_IP, most_frequent_URL, all_errors, all_responses, ��������������� ��������� ������ ���� ������������� ������� � ���� MSG
* send_letter - ���������� �������� ������, ��������������� ���� MSG � last_message.txt. ��������� �����, ��������� ���� ��������������� ���, ���������� � ���� ������. ����� ���������� ������� �� ����� mail_addr.

#### ������ ���������� �������
��� ������� ������� ������������� ������� ����������� � ��������� �������:
1. check_PID
2. put_PID
3. make_letter
4. send_letter
5. save_last_line
6. rotate_date