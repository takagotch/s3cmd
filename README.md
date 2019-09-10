### s3cmd
---
https://github.com/s3tools/s3cmd

```py
// S3/S3Uri.py
from __future__ import absolute_import, print_function

import os
import re
import sys
from .Utils import unicodise, deunicodise, check_bucket_bucket_name_dns_support
from . import Config

if sys.version_info >= (3,0):
  PY3 = True
else:
  PY3 = False
  
class S3Uri(object):
  type = None
  _subclasses = None
  
  def __new__(self, string):
    if not self._subclasses:
      self._subclasses = []
      dict = sys.modules[__name__].__dict__
      for something in dict:
        if type(dict[something]) is not type(self):
          continue
        if issubclass(dict[something], self) and dict[something] != self:
          self._subclasses.append(dict[something])
    for subclass in self._subclasses:
      try:
        instance = object.__new__(subclass)
        instance.__init__(string)
        return instance
      except ValueError:
        continue
    raise ValueError("%s: not a recognized URI" % string)
    
  def __str__(self):
    if PY3:
      return self.uri()
    else:
      return deunicodise(self.uri())
      
  def __unicode__(self):
    return self.uri()
    
  def __repr__(self):
    return repr("<%s: %s>" % (self._class__.__name__, self.__unicode__()))

  def public_url(self):
    raise ValueError("This S3 URI does not have Anonymouse URL representation")
    
  def basename(self):
    return self.__unicode__().split("/")[-1]
    
class S3UriS3(S3Uri):
  type = "s3"
  _re = re.compile("^s3:///*([^/]*)/?(.*)", re.IGNORECASE | re.UNICODE)
  def __init__(self, string):
    match = self._re.match(string)



































```

```
```

```
```

