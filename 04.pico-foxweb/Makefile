all: PICOFoxweb

clean:
	@rm -rf *.o
	@rm -rf PICOFoxweb

PICOFoxweb: main.o httpd.o
	gcc -o PICOFoxweb $^

main.o: main.c httpd.h
	gcc -c -o main.o main.c

httpd.o: httpd.c httpd.h
	gcc -c -o httpd.o httpd.c

install: PICOFoxweb
	useradd -c "PICOFoxweb user" -r -s /sbin/nologin -d /var/www/webroot lab1User
	install -o root -g root -m 0755 PICOFoxweb /usr/local/sbin/
	install -o root -g root -m 0644 httpLab1.service /etc/systemd/system/
	systemctl daemon-reload
	systemctl restart httpLab1.service
	mkdir -p /var/www
	mkdir -p /var/log/myLogs
	touch /var/log/myLogs/myLog.log
	cp -r webroot -t /var/www/
	chown -R lab1User:lab1User /var/www/webroot
	chown -R lab1User:lab1User /var/log/myLogs

uninstall:
	systemctl stop httpLab1
	rm -rf /var/www/webroot
	#rm -rf /var/log/myLogs
	rm -f /usr/local/sbin/PICOFoxweb
	rm -f /etc/systemd/system/httpLab1.service
	systemctl daemon-reload
	userdel -f lab1User

