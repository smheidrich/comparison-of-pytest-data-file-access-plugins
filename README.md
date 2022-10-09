# Comparison of pytest plugins for accessing data files

It is said there are more pytest plugins that aim to provide convenient access
to packaged data files than grains of sand on Earth. Here I compare them all.

## Comparison

<table>
<th>
<td>Name / URL</td>
<td>Supports copying to temp dir</td>
<td>Supports accessing without copying</td>
<td>Paths provided as</td>
<td>Fixture names</td>
<td>Folder names</td>
</th>
<tr>
<td>
<a href="https://pypi.org/project/pytest-datadir/">pytest-datadir</a>
</td>
<td>
True
</td>
<td>
False
</td>
<td>
pathlib.Path
</td>
<td>
`datadir`, `shared_datadir`
</td>
<td>
`data`, `test_TEST_NAME`
</td>
<tr>
<td>
<a href="https://pypi.org/project/pytest-datadir-ng/">pytest-datadir-ng</a>
</td>
<td>
True
</td>
<td>
True
</td>
<td>
py.path
</td>
<td>
`datadir`, `datadir_copy`
</td>
<td>
`data`, `data/test_TEST_NAME`, `test_TEST_NAME`
</td>
<tr>
<td>
<a href="https://pypi.org/project/pytest-datafixtures/">pytest-datafixtures</a>
</td>
<td>
False
</td>
<td>
True
</td>
<td>
pathlib.Path
</td>
<td>
`datafix`, `datafix_dir`, `datafix_read`, `datafix_readbin`
</td>
<td>
`datafixtures`, `**/datafixtures`
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

