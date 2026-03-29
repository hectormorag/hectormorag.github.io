---
layout: section
title: Traveling
permalink: /traveling/
kicker: Roads
deck: Travel notes, landscapes, routes, weather, and remembered places.
category_key: traveling
empty_message: Travel entries will appear here once posts are filed under the traveling category.
---

Traveling belongs here as movement and observation: trains, coastlines, cities, roadside details, and the texture of being elsewhere.

The photographs below are organized as travel archives by country. They live inside the site repository, so this section can grow into a proper visual map of places over time.

{% assign travel_galleries = "Belgium|England|Finland|France|Germany|India|Italy|Japan|Korea|Luxembourg|Mexico|Neatherlands|Spain|Switzerland" | split: "|" %}

<div class="travel-galleries">
  {% for country in travel_galleries %}
    {% assign country_path = '/photos/' | append: country | append: '/' %}
    {% assign country_photos = site.static_files | where_exp: "file", "file.path contains country_path" | sort: "name" %}
    {% if country_photos.size > 0 %}
      <section class="travel-gallery" id="{{ country | downcase | replace: ' ', '-' }}">
        <div class="travel-gallery-head">
          <p class="travel-gallery-kicker">Travel archive</p>
          <h3>{{ country }}</h3>
          <p class="travel-gallery-count">{{ country_photos.size }} photographs</p>
        </div>

        <div class="travel-photo-grid">
          {% for file in country_photos %}
            <a class="travel-photo-card" href="{{ file.path | relative_url }}">
              <img
                src="{{ file.path | relative_url }}"
                alt="{{ country }} travel photograph {{ forloop.index }}"
                loading="lazy"
              >
            </a>
          {% endfor %}
        </div>
      </section>
    {% endif %}
  {% endfor %}
</div>
