## Set up keybindings for vim users on macOS

Hello! I recently set up keybindings for my MacBook that were useful to me as a vim user. I'm going to share how I set up the following keybindings:
- `caps lock` as both `esc` and `control` 
- `control + H,J,K,L` as arrow key alternatives
- Shortcuts to certain applications

All the Karabiner configurations are on my [GitHub repository](https://github.com/genakag/myconfig/blob/main/karabiner.json).

I usually just bind the `caps lock` key to the `esc` key. But this time, in my attempt to pursue the best programming experience I decided to bind the `caps lock` key to both the `esc` key and the `control` key. `control` key when combined with another key, and `esc` when the key is released without pressing any other keys. I am hoping that this will make both the `esc` key and `control` key easier to press. I took note of what I did in case I need to do it again on another computer.

## Install Karabiner
Karabiner lets you customize how your keyboard behaves. I downloaded the installer at the [Karabiner website](https://karabiner-elements.pqrs.org/) and installed it by following the instructions. Just note that you need admin permission to install Karabiner.

## Binding the `caps lock` key to the `control` key
This is pretty straightforward. 
1. Open Karabiner-Elements app 
2. Go to the `Simple modifications` tab
3. Add item
4. Set `From key` to `caps_lock` and `To key` to `left_control`

Now holding the `caps lock` key should behave like the `control` key. I'll add a screenshot just in case.

![Screen Shot 2021-08-09 at 3.13.09.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628446621567/KzrOw62QA.png)

## Binding the `caps lock` to the `esc` key
I wanted the `caps lock` key to behave like the `esc` key when it is pressed and released without pressing any other keys. This was a little more complicated.

1. Open the Karabiner configuration file at `~/.config/karabiner/karabiner.json`
2. Add the JSON object below to the JSON key at
```javascript
// location to add code
profiles[<your profile>].complex_modifications.rules
```

```javascript
// code to add
{
    "description": "Bind CONTROL to ESCAPE",
    "manipulators": [
        {
            "from": {
                "key_code": "left_control",
                "modifiers": {}
            },
            "to": [
                {
                    "key_code": "left_control"
                }
            ],
            "to_if_alone": [
                {
                    "key_code": "escape"
                }
            ],
            "type": "basic"
        }
    ]
}
```

After you save the JSON file, Karabiner automatically reads the file. You should see a new rule under `Complex modifications`. You can understand what this JSON is doing by reading up on the [Karabiner documentation](https://karabiner-elements.pqrs.org/docs/json/typical-complex-modifications-examples/). 

![Screen Shot 2021-08-09 at 11.47.08.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1628477241778/hlGv846_P.png)

## Binding `control + H,J,K,L` as arrow key alternatives
I find the arrow keys sometimes too far, especially whenever I need to select an item when searching. Once this is set up, you can use this keybinding anywhere! I'll just paste the configuration JSON for this. Similar to the previous section, you just need to add the JSON to the `profiles[<your profile>].complex_modifications.rules`
```javascript
{
    "description": "Arrow keys with CONTROL + H,J,K,L",
    "manipulators": [
        {
            "from": {
                "key_code": "h",
                "modifiers": {
                    "mandatory": ["control"]
                }
            },
            "to": [
                {
                    "key_code": "left_arrow"
                }
            ],
            "type": "basic"
        },
        {
            "from": {
                "key_code": "j",
                "modifiers": {
                    "mandatory": ["control"]
                }
            },
            "to": [
                {
                    "key_code": "down_arrow"
                }
            ],
            "type": "basic"
        },
        {
            "from": {
                "key_code": "k",
                "modifiers": {
                    "mandatory": ["control"]
                }
            },
            "to": [
                {
                    "key_code": "up_arrow"
                }
            ],
            "type": "basic"
        },
        {
            "from": {
                "key_code": "l",
                "modifiers": {
                    "mandatory": ["control"]
                }
            },
            "to": [
                {
                    "key_code": "right_arrow"
                }
            ],
            "type": "basic"
        }
    ]
}
```

## Shortcuts to certain applications
I always find myself pressing `command + tab` a whole bunch to toggle through all the opened apps just to get to the browser. Having these shortcuts allow me to focus on the browser directly. 
```javascript
{
    "description": "Focus on browser",
    "manipulators": [
        {
            "type": "basic",
            "from": {
                "key_code": "b",
                "modifiers": 
                {
                    "mandatory": ["control", "command"]
                }
            },
            "to": [
                {
                    "shell_command": "osascript -e 'tell application \"Brave Browser\" to activate'"
                }
            ]
        }
    ]
}
```

This is calling an AppleScript code to focus on the specified application.

## Thanks
Thanks for reading till the end! I hope you find this helpful!

Let me know your thoughts! 