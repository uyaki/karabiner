# karabiner config
- [karabiner config](#karabiner-config)
  - [rules配置说明](#rules配置说明)
    - [配置文件目录](#配置文件目录)
    - [导入rulies配置](#导入rulies配置)
    - [rules配置文件解析](#rules配置文件解析)
  - [68配列键盘配置](#68配列键盘配置)
    - [CapsLock ➡️ Fn](#capslock-️-fn)
    - [Left_shift+esc ➡️ ~](#left_shiftesc-️-)
    - [Double click esc ➡️ double '`'](#double-click-esc-️-double-)
    - [CMD+Esc ➡️ CMD+` use](#cmdesc-️-cmd-use)
    - [Change fn-1 ... 12 ➡️ F1 ... F12](#change-fn-1--12-️-f1--f12)

## rules配置说明
### 配置文件目录
> ~/.config/karabiner/assets/complex_modifications/*.json
### 导入rulies配置
`Karabiner-Elements Preferences` -> `Complex modifications` -> `Rules` -> `Add rule`

![](https://cdn.jsdelivr.net/gh/uyaki/pic-cloud/img/20220402184803.png)

选择需要的rules
![](https://cdn.jsdelivr.net/gh/uyaki/pic-cloud/img/20220402184947.png)

### rules配置文件解析
```json
{
  "title": "this is title",
  "rules": [
    {
      "description": "Change right_option + w/a/s/d' to arrow keys",
      "manipulators": [
        {
          "type": "basic", // 固定是basic
          "from": {
            "key_code": "w", // 按下要映射的键
            "modifiers": {
              "mandatory": [ "right_option" ], // 必须同时按下的修饰符
              "optional": [ "any" ]  // 可选的修饰符，any表示其他任意修饰符按下也能匹配上
            }
          },
          "to": [
            {
              "key_code": "up_arrow" // 映射成方向上键
            }
          ],
          "conditions": [ // 满足条件下才能映射，
            {
              "type": "device_if", // 这里要满足vendor_id和product_id对应设备才能触发
              "identifiers": [
                {
                  "vendor_id": 1452,
                  "product_id": 635,
                  "description": "internal keyboard"
                }
              ]
            }
          ]
        },
        {
          ...
        }
      ]
    }
  ]
}
```

## 68配列键盘配置
1. [68配置](assets/complex_modifications/68.json)

### CapsLock ➡️ Fn
```json
{
    "description": "Change CapsLock to Fn for 68",
    "manipulators": [
        {
            "type": "basic",
            "from": {
                "key_code": "caps_lock"
            },
            "to": [
                {
                    "key_code": "fn"
                }
            ]
        }
    ]
}
```
### Left_shift+esc ➡️ ~
```json
{
    "description": "left_shift+esc to \"~\" for 68",
    "manipulators": [
        {
            "from": {
                "key_code": "escape",
                "modifiers": {
                    "mandatory": [
                        "left_shift"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "grave_accent_and_tilde",
                    "modifiers": "left_shift"
                }
            ],
            "type": "basic"
        }
    ]
}
```
### Double click esc ➡️ double '`'
```json
{
    "description": "Double click esc to double '`' for 68",
    "manipulators": [
        {
            "conditions": [
                {
                    "name": "standalone_escape_pressed",
                    "type": "variable_if",
                    "value": 1
                }
            ],
            "from": {
                "key_code": "escape",
                "modifiers": {
                }
            },
            "to": [
                {
                    "key_code": "grave_accent_and_tilde"
                },
                {
                    "key_code": "grave_accent_and_tilde"
                }
            ],
            "type": "basic"
        },
        {
            "from": {
                "key_code": "escape",
                "modifiers": {
                }
            },
            "to": [
                {
                    "set_variable": {
                        "name": "standalone_escape_pressed",
                        "value": 1
                    }
                }
            ],
            "to_delayed_action": {
                "to_if_canceled": [
                    {
                        "set_variable": {
                            "name": "standalone_escape_pressed",
                            "value": 0
                        }
                    },
                    {
                        "key_code": "escape"
                    }
                ],
                "to_if_invoked": [
                    {
                        "set_variable": {
                            "name": "standalone_escape_pressed",
                            "value": 0
                        }
                    },
                    {
                        "key_code": "escape"
                    }
                ]
            },
            "type": "basic"
        }
    ]
}
```

### CMD+Esc ➡️ CMD+` use
```json
{
    "description": "CMD+Esc to CMD+` use for 68",
    "manipulators": [
        {
            "from": {
                "key_code": "escape",
                "modifiers": {
                    "mandatory": [
                        "left_command"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "grave_accent_and_tilde",
                    "modifiers": "left_command"
                }
            ],
            "type": "basic"
        }
    ]
}
```
### Change fn-1 ... 12 ➡️ F1 ... F12

```json
{
    "description": "Change fn-1...12 to F1...F12 for 68",
    "manipulators": [
        {
            "type": "basic",
            "from": {
                "key_code": "1",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f1"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "2",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f2"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "3",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f3"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "4",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f4"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "5",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f5"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "6",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f6"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "7",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f7"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "8",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f8"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "9",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f9"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "0",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f10"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "hyphen",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f11"
                }
            ]
        },
        {
            "type": "basic",
            "from": {
                "key_code": "equal_sign",
                "modifiers": {
                    "mandatory": [
                        "fn"
                    ]
                }
            },
            "to": [
                {
                    "key_code": "f12"
                }
            ]
        }
    ]
}
```

