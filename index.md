Welcome to my blog.

I am Sam Szuflita, and I often go by `szunami`.

There isn't much to see here yet, but this is what we got:

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>