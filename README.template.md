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
  {%- for plugin in plugins %}
  <tr>
    <td>
      <a href="{{ plugin.pypi_url }}">
        {{ plugin.name }}
      </a>
    </td>
    <td>
      {% if plugin.supports_copying_to_temp %}✔{% else %}❌{% endif %}
    </td>
    <td>
      {% if plugin.supports_access_without_copying %}✔{% else %}❌{% endif %}
    </td>
    <td>
      {{ plugin.provided_as }}
    </td>
    <td>
      <ul>
      {%- for fixture_name in plugin.fixture_names %}
        <li><code>{{ fixture_name }}</code></li>
      {%- endfor %}
      </ul>
    </td>
    <td>
      <ul>
      {%- for folder_name in plugin.folder_names %}
        <li><code>{{ folder_name }}</code></li>
      {%- endfor %}
      </ul>
    </td>
  </tr>
  {%- endfor %}
</table>


## Excluded

These plugins have names that might suggest they'd do something similar, but
have slightly different aims than just providing convenient access to packaged
data files:

{% for plugin in excluded_plugins -%}
- [{{ plugin.name }}]({{ plugin.pypi_url }}):
  {{ plugin.reason|wordwrap(77)|indent(2) }}
{% endfor %}

