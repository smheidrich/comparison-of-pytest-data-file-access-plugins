# Comparison of pytest plugins for accessing data files

It is said there are more pytest plugins that aim to provide convenient access
to packaged data files than grains of sand on Earth. Here I compare them all.

## Do I even need a plugin for this?

No.

If you're only interested in files and not directories, in Python 3.7+ you
can use the functions provided by
[`importlib.resources`](https://docs.python.org/3/library/importlib.html#module-importlib.resources).

The "older" method is to use
[`pkg_resources`'s `ResourceManager`
API](https://setuptools.pypa.io/en/latest/pkg_resources.html#resourcemanager-api)
(part of setuptools) which is discouraged but has the advantage that it also
allows you to access entire directories.

The only purpose of these plugins, at least as far as this comparison is
concerned, is to get rid of the boilerplate for you.

## Other things to note

No matter which method or plugin you choose, all of them will have to extract
data files if your package is stored in an archived form (e.g. egg or wheel).
To avoid this, specify `zip_safe=False` in your package configuration.

## Comparison

<table>
  <tr>
    <th>Name / URL</th>
    <th>Supports copying to temp dir</th>
    <th>Supports access without copying</th>
    <th>Paths provided as</th>
    <th>Fixture names</th>
    <th>Folder names</th>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/pytest-datadir/">
        pytest-datadir
      </a>
    </td>
    <td>
      ✔
    </td>
    <td>
      ❌
    </td>
    <td>
      pathlib.Path
    </td>
    <td>
      <ul>
        <li><code>datadir</code></li>
        <li><code>shared_datadir</code></li>
      </ul>
    </td>
    <td>
      <ul>
        <li><code>data</code></li>
        <li><code>test_TEST_NAME</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/pytest-datadir-ng/">
        pytest-datadir-ng
      </a>
    </td>
    <td>
      ✔
    </td>
    <td>
      ✔
    </td>
    <td>
      py.path
    </td>
    <td>
      <ul>
        <li><code>datadir</code></li>
        <li><code>datadir_copy</code></li>
      </ul>
    </td>
    <td>
      <ul>
        <li><code>data</code></li>
        <li><code>data/test_TEST_NAME</code></li>
        <li><code>test_TEST_NAME</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>
      <a href="https://pypi.org/project/pytest-datafixtures/">
        pytest-datafixtures
      </a>
    </td>
    <td>
      ❌
    </td>
    <td>
      ✔
    </td>
    <td>
      pathlib.Path
    </td>
    <td>
      <ul>
        <li><code>datafix</code></li>
        <li><code>datafix_dir</code></li>
        <li><code>datafix_read</code></li>
        <li><code>datafix_readbin</code></li>
      </ul>
    </td>
    <td>
      <ul>
        <li><code>datafixtures</code></li>
        <li><code>**/datafixtures</code></li>
      </ul>
    </td>
  </tr>
</table>


## Excluded

These plugins have names that might suggest they'd do something similar, but
have slightly different aims than just providing convenient access to packaged
data files:

- [pytest-datadir-mgr](https://pypi.org/project/pytest-datadir-mgr/):
  More about downloading, caching etc. than just providing convenient access to
  packaged data files.
- [pytest-data-file](https://pypi.org/project/pytest-data-file/):
  More about loading data from files than just providing raw access.
- [pytest-datafiles](https://pypi.org/project/pytest-datafiles/):
  Doesn't provide much in the way of simplifying access to packaged files. More
  focused on the copy-to-temp aspect.
- [pytest-data-from-files](https://pypi.org/project/pytest-data-from-files/):
  Like pytest-data-file, more about implicitly loading test data from files
  than giving access to those files.
- [pytest-filedata](https://pypi.org/project/pytest-filedata/):
  Also more about parametrizing tests with data from files.

