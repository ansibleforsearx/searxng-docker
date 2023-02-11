SearXNG_docker
==============
Install and configure [SearXNG](https://github.com/searxng/searxng) as a docker image.

Verified working Linux distros
------------------------------
- Arch Linux
- Debian bullseye
- openSUSE Tumbleweed
- Fedora 37 <br/><br/> [![CI](https://github.com/ansibleforsearx/searxng-docker/actions/workflows/CI.yml/badge.svg)](https://github.com/ansibleforsearx/searxng-docker/actions/workflows/CI.yml)

This role will probabbly work on the majority of Systemd distros but I can't test them all.

Role Variables
--------------
Here are the variables and their defaults, none of which are manditory. For more information refer to the [project documentation](https://docs.searxng.org/).
```yaml
searxng_docker_repo: 'https://github.com/searxng/searxng-docker.git'
  # If you're maintaing an on premisis fork of the searxng-docker repo
  # you should put it here that way multiple hosts don't need to go all
  # the way out to github for it.
searxng_docker_sha1: 'd4f06df911e91803d6af48b8f0e060f08429b767'
  # The sha1 hash of the searxng docker repo used during testings. If
  # you overwrite this default I can't garentee sucess.
searxng_docker_path: '/usr/local/searxng-docker'
  # Where searxng will be installed
searxng_docker_service_name: 'searxng-docker.service'
  # The name of the Systemd service
searxng_docker_hostname: '# SEARXNG_HOSTNAME=<host>'
searxng_docker_letsencrypt: '# LETSENCRYPT_EMAIL=<email>'
  # If you're going to change the above two variables provide the full
  # uncommented line. For example:
  # searxng_docker_hostname: 'SEARXNG_HOSTNAME=MyWonderfulHost'
searxng_docker_default_settings: 'true'
searxng_docker_debug: 'false'
searxng_docker_instance_name: 'SearXNG'
searxng_docker_privacypolicy_url: 'false'
searxng_docker_donation_url: 'https://docs.searxng.org/donate.html'
searxng_docker_contact_url: 'false'
searxng_docker_enable_metrics: 'true'
searxng_docker_safe_search: '0'
searxng_docker_autocomplete: ''
  # This is where SearXNG gets it's autocomplete data. options include:
  #   'dbpedia'
  #   'duckduckgo'
  #   'google'
  #   'startpage'
  #   'swisscows'
  #   'qwant'
  #   'wikipedia'
searxng_docker_default_lang: ''
  # leave blank to detect from browser information or use codes from
  # git://searx/languages.py.
searxng_docker_ban_time_on_fail: '5'
searxng_docker_max_ban_time_on_fail: '120'
searxng_docker_formats: 'html,'
  # use a comma seperated list of formats here. example 'html, csv, json, rss' 
searxng_docker_base_url: 'false'
searxng_docker_port: '8888'
searxng_docker_bind_address: '127.0.0.1'
searxng_docker_limiter: 'false'
searxng_docker_image_proxy: 'false'
searxng_docker_static_use_hash: 'false'
searxng_docker_default_locale: ''
searxng_docker_query_in_title: 'false'
searxng_docker_infinite_scroll: 'false'
searxng_docker_center_alignment: 'false'
searxng_docker_cache_url: 'https://web.archive.org/web/'
searxng_docker_default_theme: 'simple'
searxng_docker_simple_style: 'auto'
  # The SearXNG UI theme, options include 'auto' 'light' 'dark'
searxng_docker_redis_url: 'redis://redis:6379/0'
searxng_docker_request_timeout: '2.0'
searxng_docker_max_request_timeout: '10.0'
searxng_docker_useragent_suffix: ''
searxng_docker_pool_connections: '100'
searxng_docker_pool_maxsize: '10'
searxng_docker_enable_http2: 'true'
searxng_docker_path_to_docker_compose: '/usr/bin'
searxng_docker_path_to_systemd_units: '/etc/systemd/system'
```

Example Playbook
----------------
Here's what the author uses to configure his laptop. 
```yaml
- hosts: all
  become: true
  roles:
  - role: ansibleforsearx.searxng_docker
      vars:
        searxng_docker_enable_metrics: 'false'
        searxng_docker_instance_name: 'MySearXNG'
        searxng_docker_autocomplete: 'duckduckgo'
        searxng_docker_simple_style: 'dark'
        searxng_docker_infinite_scroll: 'true'
```
My browser's homepage is http://localhost as is it's default search engine. I clear cookies on exit with an exception for localhost. The individual search engine settings are stored in the browser cookie. I use https everwhere with an exception for localhost.

License
-------
[GPL 3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)

Author Information
------------------
I'm a consumer of this amazing product. This is my contribution.<br/>
*This is an auto generated file do not edit it directly.*<br/>
*Refer to [SearXNG_docker.org](./SearXNG_docker.org) for more details.*<br/><br/>
