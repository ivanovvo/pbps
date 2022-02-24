all: PICOFoxweb

clean:
	@rm -rf *.o
	@rm -rf PICOFoxweb

install: PICOFoxweb
	useradd -c "PICOFoxweb user" -r -s /sbin/nologin -d /var/www/foxweb foxweb
	install -o root -g root -m 0755 PICOFoxweb /usr/local/sbin/
	install -o root -g root -m 0644 foxweb.service /etc/systemd/system/
	systemctl daemon-reload
	systemctl restart foxweb.service
	mkdir -p /var/www/foxweb
	cp -r webroot -t /var/www/foxweb/
	chown -R foxweb:foxweb /var/www/foxweb

uninstall:
	systemctl stop foxweb
	rm -rf /var/www/foxweb
	rm -f /usr/local/sbin/PICOFoxweb
	rm -f /etc/systemd/system/foxweb.service
	systemctl daemon-reload
	userdel -f foxweb

PICOFoxweb: main.o httpd.o
	gcc -o PICOFoxweb $^

main.o: main.c httpd.h
	gcc -c -o main.o main.c

httpd.o: httpd.c httpd.h
	gcc -c -o httpd.o httpd.c
