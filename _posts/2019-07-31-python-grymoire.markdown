---
layout: post
title:  "Python Grymoire"
date:   2019-07-31 11:25:51 +0000
categories: python grymoire
---

# Python Grymoire

Random tidbits that I need to reference every now and then. Everything is assumed python3

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

## Logging

```
import logging
logger = logging.getLogger()

logger.debug()
logger.info()
logger.warning()
logger.error()
logger.critical()
```
