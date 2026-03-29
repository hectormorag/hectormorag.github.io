---
layout: section
title: Travels
permalink: /travels/
kicker: Country archives
deck: Journeys arranged by place, with each country opening into its own image field.
show_posts: false
wide_body: true
---

Travels is where places get to breathe. Instead of one endless gallery, each country has its own section, its own rhythm, and its own grid of images.

{% assign travel_countries = "Belgium|Finland|France|Germany|Italy|Mexico|Spain|Switzerland" | split: "|" %}

<div class="travel-page" id="travels-top">
  <section class="travel-index">
    {% for country in travel_countries %}
      {% assign country_path = '/photos/' | append: country | append: '/' %}
      {% assign country_photos = site.static_files | where_exp: "file", "file.path contains country_path" | sort: "name" %}
      {% if country_photos.size > 0 %}
        {% assign lead_photo = country_photos | first %}
        <a class="travel-index-card" href="#{{ country | slugify }}">
          <span class="travel-index-thumb">
            <img
              src="{{ lead_photo.path | relative_url }}"
              alt="{{ country }} preview image"
              loading="lazy"
            >
          </span>
          <span class="travel-index-copy">
            <span class="travel-index-country">{{ country }}</span>
            <span class="travel-index-count">{{ country_photos.size }} photos</span>
          </span>
        </a>
      {% endif %}
    {% endfor %}
  </section>

  <div class="country-stack">
    {% for country in travel_countries %}
      {% assign country_path = '/photos/' | append: country | append: '/' %}
      {% assign country_photos = site.static_files | where_exp: "file", "file.path contains country_path" | sort: "name" %}
      {% if country_photos.size > 0 %}
        <section class="country-section" id="{{ country | slugify }}">
          <div class="country-section-head">
            <div>
              <p class="country-kicker">Country archive</p>
              <h2>{{ country }}</h2>
            </div>
            <p class="country-count">{{ country_photos.size }} photographs</p>
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
</div>
