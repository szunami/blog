Welcome to my blog.

I am Sam Szuflita, and on the internet I go by `szunami`.

There isn't much to see here yet, but this is what we got:

<ul>
  {% for post in site.posts %}
    <li>
      <a href="/blog{{ post.url }}">{{ post.title }}</a>
      <br>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>
