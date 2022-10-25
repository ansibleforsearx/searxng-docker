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
Here are the variables and their defaults for more information refer to the [project documentation](https://docs.searxng.org/).
```yaml
searxng_repo: 'https://github.com/searxng/searxng-docker.git'
  # If you're maintaing an on premisis fork of the searxng-docker repo
  # you should put it here that way multiple hosts don't need to go all
  # the way out to github for it.
searxng_sha1: 'd4f06df911e91803d6af48b8f0e060f08429b767'
  # The sha1 hash of the searxng docker repo used during testings. If
  # you overwrite this default I can't garentee sucess.
searxng_path: '/usr/local/searxng-docker'
  # Where searxng will be installed
searxng_service_name: 'searxng-docker.service'
  # The name of the Systemd service
searxng_hostname: '# SEARXNG_HOSTNAME=<host>'
searxng_letsencrypt: '# LETSENCRYPT_EMAIL=<email>'
  # If you're going to change the above two variables provide the full
  # uncommented line. For example:
  # searxng_hostname: 'SEARXNG_HOSTNAME=MyWonderfulHost'
searxng_default_settings: 'true'
searxng_debug: 'false'
searxng_instance_name: 'SearXNG'
searxng_privacypolicy_url: 'false'
searxng_donation_url: 'https://docs.searxng.org/donate.html'
searxng_contact_url: 'false'
searxng_enable_metrics: 'true'
searxng_safe_search: '0'
searxng_autocomplete: ''
  # This is where SearXNG gets it's autocomplete data. options include:
  #   'dbpedia'
  #   'duckduckgo'
  #   'google'
  #   'startpage'
  #   'swisscows'
  #   'qwant'
  #   'wikipedia'
searxng_default_lang: ''
  # leave blank to detect from browser information or use codes from
  # git://searx/languages.py.
searxng_ban_time_on_fail: '5'
searxng_max_ban_time_on_fail: '120'
searxng_formats: 'html,'
  # use a comma seperated list of formats here. example 'html, csv, json, rss' 
searxng_base_url: 'false'
searxng_port: '8888'
searxng_bind_address: '127.0.0.1'
searxng_limiter: 'false'
searxng_image_proxy: 'false'
searxng_static_use_hash: 'false'
searxng_default_locale: ''
searxng_query_in_title: 'false'
searxng_infinite_scroll: 'false'
searxng_center_alignment: 'false'
searxng_cache_url: 'https://web.archive.org/web/'
searxng_default_theme: 'simple'
searxng_simple_style: 'auto'
  # The SearXNG UI theme, options include 'auto' 'light' 'dark'
searxng_redis_url: 'redis://redis:6379/0'
searxng_request_timeout: '2.0'
searxng_max_request_timeout: '10.0'
searxng_useragent_suffix: ''
searxng_pool_connections: '100'
searxng_pool_maxsize: '10'
searxng_enable_http2: 'true'
searxng_path_to_docker_compose: '/usr/bin'
# See REHL OS family hosts below for more detail.
searxng_path_to_systemd_units: '/etc/systemd/system'
```

Example Playbook
----------------
Here's what the author uses to configure his laptop. 
```yaml
- hosts: all
  become: true
- role: ansibleforsearx.searxng_docker
    vars:
      searxng_enable_metrics: 'false'
      searxng_instance_name: 'MySearXNG'
      searxng_autocomplete: 'duckduckgo'
      searxng_simple_style: 'dark'
      searxng_infinite_scroll: 'true'
```
My browser's homepage is http://localhost as is it's default search engine. I clear cookies on exit with an exception for localhost. The individual search engine settings are stored in the browser cookie. I use https everwhere with an exception for localhost.

REHL OS family hosts
--------------------
This role uses the geerlingguy.docker role to install the docker dependencies on REHL OS family hosts. As such the path to docker compose is known and the searxng_path_to_docker_compose variable is ignored on those hosts. The geerlingguy.docker role dependency should install itself when you install this role.

License
-------
[GPL 3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)

Author Information
------------------
I'm a consumer of this amazing product. This is my contribution.<br/>
*This is an auto generated file do not edit it directly.*<br/>
*Refer to [SearXNG_docker.org](./SearXNG_docker.org) for more details.*<br/><br/>
