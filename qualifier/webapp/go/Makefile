run:
	go build -o app
	rsync -av ../public/ /opt/isucon/public/
	sudo cp nginx-isucon3 /etc/nginx/sites-enabled/isucon3
	sudo systemctl restart nginx
	./app

bench:
	sudo mv /var/log/nginx/access-kataribe.log /var/log/nginx/access-kataribe-`date +%Y%m%d-%H%H%S`.log
	sudo systemctl restart nginx
	GODEBUG=cgocheck=0 ../../qualifier_bench/qualifier_bench benchmark

kataribe:
	cat /var/log/nginx/access-kataribe.log | ~/go/bin/kataribe

profile:
	go tool pprof -http=":5001" app cpu.pprof

check-css:
	curl -i http://localhost/css/bootstrap.min.css

http-dump:
	sudo tcpdump -i lo -A dst port 80

