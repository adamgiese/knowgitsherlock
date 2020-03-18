---
pagination:
  data: collections.challenge
  alias: entries
  reverse: true
  size: 9999 # TODO: real pagination
layout: layouts/home.njk
eleventyNavigation:
  key: Challenges
  order: 3
renderData:
  title: Challenges | Know git, Sherlock
---
<h1>All Challenges</h1>
<ol reversed>
  {%- for entry in entries %}
    <li>
      <a href="{{ entry.url }}">
        {{ entry.data.title}}
      </a>
    </li>
  {%- endfor %}
</ol>
