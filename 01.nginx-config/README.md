Nginx Config
---

Explain
```
01.nginx-config
│
└───dist                 // gitignored, the output directory
│
└───group_vars
│   │
│   └───webservers       // variables definitions for hosts "webservers"
│
└───roles
│   │
│   └───web
│       │
│       └───tasks
│       │   │
│       │   └───main.yml // use "template" module to create the config file
│       │
│       └───templates
│           │
│           └───conf.j2  // the Jinja2 template
│
└───hosts                // hosts definition, points "webservers" to localhost
│
└───nginx.yml            // this is the playbook
```

Exexute the plays:

```bash
cd 01.nginx-config
ansible-playbook -i hosts nginx.yml
```

Output `dist/web.config`
```
# Ansible managed


location ^~ / {
    proxy_pass          http://localhost:8080;
    proxy_http_version  1.1;
    proxy_set_header    Connection "";
    add_header Cache-Control no-cache;
}

location ^~ /users {
    proxy_pass          http://localhost:8080;
    proxy_http_version  1.1;
    proxy_set_header    Connection "";
    add_header Cache-Control no-cache;
}

location ^~ /posts {
    proxy_pass          http://localhost:8080;
    proxy_http_version  1.1;
    proxy_set_header    Connection "";
    add_header Cache-Control no-cache;
}
```
