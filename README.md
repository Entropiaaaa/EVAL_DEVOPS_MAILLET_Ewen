# EVAL_DEVOPS_MAILLET_Ewen

Playbook Ansible:

- name: Installation docker sur Debian
  hosts: all
  become: true

  tasks:
    - name: Installer certificate
      apt:
        name: ca-certificates
        state: present
    - name: Installer curl
      apt:
        name: curl
        state: present
    - name: Installer gnupg
      apt:
        name: gnupg
        state: present



Docker Compose :

services:
  db:
    image: mariadb
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MARIADB_ROOT_PASSWORD: mariadb

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  wordpress:
    image: wordpress:latest
    volumes:
      - wp_data:/var/www/html
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=mariadb
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
  wp_data:

