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

    http {
        # 网盘
        server {
            listen 80;
            server_name file.19981026.xyz;
    
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
            }
        }
    }
