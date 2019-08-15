---
layout: post
title:  "Python Grymoire"
date:   2019-07-31 11:25:51 +0000
categories: python grymoire
---

# Python Grymoire

Random tidbits that I need to reference every now and then. Everything is assumed python3

## Logging

```
import logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger()

logger.debug()
logger.info()
logger.warning()
logger.error()
logger.critical()
```

For alternative methods of setting logger levels, look at the following. However, it appears that this is overwritten by logging.basicConfig

```
logger.setLevel(logging.DEBUG)
logger.getEffectiveLevel()
```

## Regex

Don't use re.match is anchored at the start of string. Use re.search

```
import re

match = re.search('meow', 'meow woof meow')
# only returns the first match
# match.group() to see thae matching object
# 'meow woof meow'[match.start(), match.end()] == 'meow'
# match is not None


match = re.search('meow', 'woof')
# match == None

match = re.findall('meow', 'meow woof meow')
# match == ['meow', 'meow']
```

## Typing

```
from typing import Dict, List, Sequence, Tuple, Any
def example(
   first: str,
   second: str=None,
   third: Dict[str, str],
   fourth: Tuple[int, int],
   fifth: Any,
) -> str:
```


## Unit Testing

Patching is difficult, and difficult to get right.
```
from unittest.mock import MagicMock, patch
patcher = patch(THE.REAL.STUFF, spec=True)
mock_the_real_stuff = patcher.start()
patcher.stop()


# or maybe
patcher.stopall()
```

patch vs patch.object

The former is a string path, and patch.object is an actual reference

