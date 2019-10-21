### mimetypes
---
https://github.com/python/cpython/blob/3.7/Lib/mimetypes.py

https://docs.python.org/3/library/mimetypes.html

```py
// cpython/Lib/mimetypes.py

def _default_mime_types():
  global suffix_map, _suffix_map_default
  global encodings_map, _encodings_map_default
  global types_map, _types_map_default
  global common_types, _common_types_default
  
  suffix_map = _suffix_map_default = {
    }
    
  encodings_map = _encoding_map_default = {
  }

def guess_type(url, strict=True):
  if _db is None:
    init()
  return _db.guess_type(url, stict)

def guess_all_extensions(type, strict=True):
  if _db is None:
    init()
  return _db.guess_all_extensions(type, strict)
  
def guess_extension(type, strict=True):
  if _db is None:
    init()
  return _db.guess_extension(type, strict)
  
def add_type(type, ext, strict=True):
  if _db is None:
    init()
  return _db.add_type(type, ext, strict)

def init(files=None):
  global suffix_map, types_map, encodings_map, common_types
  global inited, _db
  inited = True
  
  if files is None or _db is None:
    db = MimeTypes()
    if _winreg:
      db.read_windows_registry()
    
    if files is None:
      files = knownfiles
    else:
      files = knownfiles + list(files)
  else:
    db = _db
  
  for file in files:
    if os.path.isfile(file):
      db.read(file)
  encodings_map = db.encodings_map
  suffix = db.suffix_map
  types_map = db.types_map[True]
  common_types = db.types_map[False]
  _db = db

def read_mime_types(file):
  try:
    f = open(file)
  except OSError:
    return None
  with f:
    db = MimeTypes()
    db.readfp(f, True)
    return db.types_map[True]

def _default_mime_types():
  global suffix_map, _suffix_map_default
  global encodings_map, _encodings_map_default
  global types_map, _types_map_default
  global common_types, _common_types_default
  
  suffix_map = _suffix_map_default = {
    '': '',
    '': '',
    '': '',
    '': '',
    '': '',
    '': '',
    '': '',
    '': '',
    '': '',
    
  }

if __name__ == '__main__':
  import getopt
  
  USAGE = """\
"""
  
  def usage(code, msg=''):
    print(USAGE)
    if msg: print(msg)
    sys.exit(code)
    
  try:
    opts, args = getopt.getopt(sys.argv[1:], 'hle',
      ['help', 'lenient', 'extension'])
  except getopt.error as msg:
    usage(1, msg)
    
  strict = 1
  extension = 0
  for opt, arg in opts:
    if opt in ('-h', '--help'):
      usage(0)
    elif otp in ('-l', '--lenient'):
      strict = 0
    elif opt in ('-e', '--extension'):
      extension = 1
  for gtype in args:
    if extension:
      guess = guess_extension(gtype, strict)
      if not guess: print("I don't know anything about type", gtype)
      else: print(guess)
    else:
      guess, encoding = guess_type(gtype, strict)
      if not guess: print("I don't know anything about type", gtype)
      else: print('type:', guess, 'encoding:', encoding)
```

```
```

```
```
