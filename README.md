# `vk-bot`

`vk-bot` is a Python 2/3 VK bot builder built with
[`vk-client`](https://github.com/Suenweek/vk-client).


## Install

```bash
pip install vk-bot
```


## Usage

#### Create bot
```python
import vk_bot

bot = vk_bot.VkBot('YOUR_ACCESS_TOKEN')
```

#### Register event handlers
```python
from vk_client import GroupEventType

@bot.on([GroupEventType.GROUP_JOIN])
def group_join_handler(obj):
    bot.vk.Message.send(
        peer=obj.user,
        message=f'Welcome, {obj.user.first_name}!'
    )
```

#### Create event handler for commands
```python
from vk_bot.ext import CmdHandler

command = CmdHandler(bot)
```

#### Register commands
```python
import operator

OPS = {
    'add': operator.add,
    'sub': operator.sub,
    'mul': operator.mul,
    'div': operator.truediv
}

@command(args={
    'op': {'choices': list(OPS)},
    'a': {'type': int},
    'b': {'type': int}
})
def calc(op, a, b):
    """Simple calculator."""
    try:
        return f'Result: {OPS[op](a, b)}'
    except ArithmeticError as e:
        return f'Error: {e}'
```

#### Run bot
```python
bot.run()
```
