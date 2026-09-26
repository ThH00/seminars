---
layout: default
title: All Seminars
permalink: /archive/
---

# All Seminars This Semester

<ul class="seminar-list">
{% assign all_seminars = site.seminars | sort: "date" %}
{% for seminar in all_seminars %}
  <li class="seminar-card">
    {% if seminar.flyer %}
      <a href="{{ seminar.url | relative_url }}">
        <img class="thumb" src="{{ seminar.flyer | relative_url }}" alt="Flyer for {{ seminar.title }}">
      </a>
    {% endif %}
    {% if seminar.photo %}
      <a href="{{ seminar.url | relative_url }}">
        <img class="thumb thumb-photo-sm" src="{{ seminar.photo | relative_url }}" alt="Photo of {{ seminar.speaker }}">
      </a>
    {% endif %}
    <div>
      <a href="{{ seminar.url | relative_url }}"><strong>{{ seminar.title }}</strong></a><br>
      {% if seminar.date_tbd %}Date to be announced{% else %}{{ seminar.date | date: "%B %-d, %Y" }}{% endif %} &middot; {{ seminar.speaker }}{% if seminar.affiliation %}, {{ seminar.affiliation }}{% endif %}
    </div>
  </li>
{% endfor %}
</ul>
