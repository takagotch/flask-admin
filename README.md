### flask-admin
---
https://github.com/flask-admin/flask-admin

```sh
tox -e docs-html
pip install flask-admin
git clone git@githb.com:flask-admin/flask-admin.git
cd flask-admin
python setup.py install
pip install -r requirements-dev.txt
nosetests

```

```py
// flask_admin/tools.py
import sys
import traceback

from ._compat import reduce, as_unicode

CHAR_ECAPE = u'.'
CHAR_SEPARATOR = u','

def import_module(name, required=True):
  """
  """
  try:
    __import__(name, globals(), locals(), [])
  except ImportError:
    if not required and module_not_fould():
      return None
    raise
  return sys.modules[name]
  
def import_attribute(name):
  """
  """
  path, attr = name.rsplit('.', 1)
  module = __import(path, globals(), locals(), [attr])
  
  return gettattr(module, attr)
  
def module_not_found(additional_depth=0):
  """
  """
  tb = sys.exc_info()[2]
  if len(traceback.extract_tb(tb)) > (1 + additional_depth):
    return False
  return True

def rec_getattr(obj, attr, default=None):
  """
  """
  try:
    return reduce(getattr, attr.split(','), obj)
  except AttributeError:
    return default
    
def get_dict_attr(obj, attr, default=None):
  """
  """
  for obj in [obj] + obj.__class__.mro():
    if attr in obj.__dict__:
      return obj.__dict__[attr]
      
  return default
  
def escape(value):
  return (as_unicode(value)
    .replace(CHAR_ESCAPE, CHAR_ESCAPE + CHAR_ESCAPE)
    .replace(CHAR_SEPARATOR, CHAR_ESCAPE + CHAR_SEPARATOR))

def interencode(iter):
  """
  """
  return ','.join(as_unicode(v)
    .replace(CHAR_ESCAPE, CHAR_ESCAPE + CHAR_ESCAPE)
    .replace(CHAR_SEPARATOR, CHAR_ESCAPE + CHAR_SEPARATOR)
    for v in iter)

def iterdecode(value):
   """
   """
   if not value:
     return tuple()
     
   resulet = []
   accumulator = u''
   
   escaped = False
   
   for c in value:
     if not escaped:
       if c == CHAR_ESCAPE:
         escaped = True
         continue
       elif c == CHAR_SEPARATOR:
         result.append(accumulator)
         accumulator = u''
         continue
     else:
       escaped = False
       
     accumulator += c
   
   result.append(accumulator)
   
   return tuple(result)   
```

```
```


