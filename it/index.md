Interrogarsi sulla trama della realtà, della società e della natura umana può essere visto come perdersi nello spazio.

Questo blog prende il nome da 3D Pinball: Space Cadet del 1995 e Dead Space di Visceral Games.

Quindi se come essere umano senti il terrore della vastità e dell'ignoto, non preoccuparti, segui il flusso.

Inclina forte il terreno di gioco e calpesta gli zombie spaziali.

![](/images/dead-space.gif)

![](/images/3D_Pinball.png)

Space Cadet è anche il nome di un brano dei Kyuss che avevo in testa quando ho pensato a questo blog.

<video width="100%" height="auto" controls poster="https://img.youtube.com/vi/aW8nFgRwnoA/0.jpg">
  <source src="https://user-images.githubusercontent.com/103458862/221435341-da1ec07e-903d-4ed8-ba8d-e3d7a9163a5d.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> 
<h2 class="post-list-heading">Posts</h2>
<ul class="post-list">
{% for post in site.posts %}
  <li>
      <span class="post-meta">{{ post.date | date: "%d %B %Y" }}</span>
      <h3>
        <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h3>
  </li>
{% endfor %}
<p class="rss-subscribe">iscriviti <a href="/feed.xml">tramite RSS</a></p>
