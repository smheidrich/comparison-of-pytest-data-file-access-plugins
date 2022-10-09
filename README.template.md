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
{%- for plugin in plugins %}
<tr>
<td>
<a href="{{ plugin.pypi_url }}">{{ plugin.name }}</a>
</td>
<td>
{{ plugin.supports_copying_to_temp }}
</td>
<td>
{{ plugin.supports_access_without_copying }}
</td>
<td>
{{ plugin.provided_as }}
</td>
<td>
{{ plugin.fixture_names|map('tojson')|join(', ')|replace('"', '`') }}
</td>
<td>
{{ plugin.folder_names|map('tojson')|join(', ')|replace('"', '`') }}
</td>
{%- endfor %}
</tr>
</table>
