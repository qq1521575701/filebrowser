# filebrowser

# 运行查看密码 更改设置
    docker run --rm \
        -v filebrowser_data:/srv \
        -v filebrowser_database:/database \
        -v filebrowser_config:/config \
        -p 8080:80 \
        filebrowser/filebrowser

# 再次运行持久处理

    docker run --name filebrowser -d \
        -v filebrowser_data:/srv \
        -v filebrowser_database:/database \
        -v filebrowser_config:/config \
        -p 8080:80 \
        filebrowser/filebrowser

# nginx
    server {
       listen 80;
       server_name p6.hk;
    
    set_real_ip_from 173.245.48.0/20;
    set_real_ip_from 103.21.244.0/22;
    set_real_ip_from 103.22.200.0/22;
    set_real_ip_from 103.31.4.0/22;
    set_real_ip_from 141.101.64.0/18;
    set_real_ip_from 108.162.192.0/18;
    set_real_ip_from 190.93.240.0/20;
    set_real_ip_from 188.114.96.0/20;
    set_real_ip_from 197.234.240.0/22;
    set_real_ip_from 198.41.128.0/17;
    set_real_ip_from 162.158.0.0/15;
    set_real_ip_from 104.16.0.0/13;
    set_real_ip_from 104.24.0.0/14;
    set_real_ip_from 172.64.0.0/13;
    set_real_ip_from 131.0.72.0/22;
    
    location / {
        proxy_pass http://127.0.0.1:8080;  # 确保 FileBrowser 在 Docker 容器内监听 8080 端口
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    
        # 增加以下头部设置
        proxy_set_header X-Scheme $scheme;
        proxy_set_header X-Forwarded-Port $server_port;
        client_max_body_size 0;
    }}
