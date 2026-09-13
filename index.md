---
layout: default
title: Home
permalink: /
---

# {{ site.title }}

{{ site.description }}

<p><a href="{{ '/calendar/' | relative_url }}">📅 View the full calendar</a></p>

## Upcoming Seminars

{% assign today = site.time | date: "%s" %}
{% assign sorted_seminars = site.seminars | sort: "date" %}
{% assign upcoming_count = 0 %}
<ul class="seminar-list">
{% for seminar in sorted_seminars %}
  {% assign seminar_epoch = seminar.date | date: "%s" %}
  {% if seminar_epoch >= today %}
    {% assign upcoming_count = upcoming_count | plus: 1 %}
    <li class="seminar-card">
      {% if seminar.photo or seminar.flyer %}
        <a href="{{ seminar.url | relative_url }}">
          <img class="thumb {% if seminar.photo %}thumb-photo{% endif %}" src="{{ seminar.photo | default: seminar.flyer | relative_url }}" alt="{% if seminar.photo %}Photo of {{ seminar.speaker }}{% else %}Flyer for {{ seminar.title }}{% endif %}">
        </a>
      {% endif %}
      <div>
        <a href="{{ seminar.url | relative_url }}"><strong>{{ seminar.title }}</strong></a><br>
        {{ seminar.date | date: "%B %-d, %Y" }} &middot; {{ seminar.speaker }}
      </div>
    </li>
  {% endif %}
{% endfor %}
{% if upcoming_count == 0 %}
  <li>No upcoming seminars scheduled yet — check back soon.</li>
{% endif %}
</ul>

## Past Seminars

{% assign past_count = 0 %}
<ul class="seminar-list">
{% for seminar in sorted_seminars reversed %}
  {% assign seminar_epoch = seminar.date | date: "%s" %}
  {% if seminar_epoch < today %}
    {% assign past_count = past_count | plus: 1 %}
    <li class="seminar-card past">
      {% if seminar.photo %}
        <a href="{{ seminar.url | relative_url }}">
          <img class="thumb thumb-photo" src="{{ seminar.photo | relative_url }}" alt="Photo of {{ seminar.speaker }}">
        </a>
      {% endif %}
      <div>
        <a href="{{ seminar.url | relative_url }}">{{ seminar.title }}</a><br>
        {{ seminar.date | date: "%B %-d, %Y" }} &middot; {{ seminar.speaker }}
      </div>
    </li>
  {% endif %}
{% endfor %}
{% if past_count == 0 %}
  <li>No past seminars yet.</li>
{% endif %}
</ul>
