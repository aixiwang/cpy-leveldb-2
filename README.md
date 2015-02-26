# cpy-leveldb-2 #
Python bindings for LevelDB using leveldb c api
Based on https://github.com/forhappy/cpy-leveldb project

Author: Fu Haiping (haipingf@gmail.com)
<br>README.md is updated by Aixi Wang <aixi.wang@hotmail.com>


1. How to build
------------------
    $ cd leveldb
    $ make
    $ cp *.a /usr/local/lib
    $ cp lib*so.* /lib
    $ cp lib*so.* /lib/
    $ cd ..
    $ python setup.py build


2. Example Usage
----------------

    >>> import leveldb
    >>> db = leveldb.LevelDB("/tmp/leveldb")
    >>> db.Put("1", "111")
    >>> db.Put("2", "222")
    >>> db.Put("3", "333")
    >>> db.Get("1")
    '111'
    >>> db.Get("3")
    '333'
    >>> db.Get("2")
    '222'
    >>> batch = leveldb.WriteBatch()
    >>> for i in xrange(20):
    ... batch.Put(str(i), "hello world %i" % i)
    ... 
    >>> db.Get("2")
    '222'
    >>> db.Get("5")
    ''
    >>> db.Write(batch)
    >>> db.Get("5")
    'hello world 5'
    >>> db.Get("2")
    'hello world 2'
    >>> iter = leveldb.Iterator(db)
    Iterator_init executed.
    >>> iter.First()
    >>> iter.Key()
    '0'
    >>> iter.Value()
    'hello world 0'
    >>> iter.Last()
    >>> iter.Key()
    '9'
    >>> iter.Value()
    'hello world 9'
    >>> iter.First()
    >>> iter.Next()
    >>> iter.Key()
    '1'
    >>> iter.Next()
    >>> iter.Key()
    '10'
    >>> iter.Next()
    >>> iter.Key()
    '11'
    >>> iter.Value()
    'hello world 11'
    >>> db.Put("1", "111")
    >>> db.Put("2", "222")
    >>> db.Put("3", "333")
    >>> db.Get("1")
    '111'
    >>> snap = leveldb.Snapshot(db)
    Snapshot_init executed.
    >>> db.Delete("1")
    >>> db.Get("1")
    ''
    >>> snap.Set()
    >>> db.Get("1")
    '111'
    >>> snap.Reset()
    >>> db.Get("1")
    ''
    >>> snap.Release()
