# 插件设置

这一页面仅涉及**RPGItems**插件的设置文件

在大多数情况下您不需要去修改这个文件，但是设置文件中的部分全局设置可能会对您有用。

这是一份插件的默认设置文件：

```
language: en_US
version: '1.0'
general:
  enabled_languages:
  - en_US
  - zh_CN
  give_perms: false
  item:
    fs_lock: false
    show_loaded: false
command:
  list:
    item_per_page: 9
    power_per_page: 5
support:
  world_guard:
    enable: false
    force_refresh: false
    disable_in_no_pvp: true
    show_warning: true
gist:
  token: ''
  publish: true
item:
  defaults:
    numeric_bar: false
    force_bar: false
    license: All Right Reserved
    enchant_mode: ALLOW
    allow_anvil_enchant: false
unused:
  locale_inv: false
```
