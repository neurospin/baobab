---
layout: page_select
title:
permalink: /people/
---

{% assign people_sorted = site.people | sort: 'joined' | reverse %}
{% assign people_array = "pi|engineer|postdoc|gradstudent|alumni" | split: "|" %}


{% assign people_valid = '' | split: '' %}
{% for item in people_array %}
    {% assign listpeople = '' | split: '' %}
    {% for profile in people_sorted %}
        {% if profile.position contains item %}
            {% assign listpeople = listpeople | push: profile %}
        {% endif %}
    {% endfor %}
    {% assign people_valid = people_valid | push: listpeople %}
{% endfor %}
 
 
<div>
{% assign i = 0 %}
{% for item in people_array %}
    {% assign listpeople = people_valid[i] %}
    {% assign i = i | plus: 1 %}
    {% if listpeople.size > 0 %}
        <div class="pos_header">
        {% if item == 'postdoc' %}
            <h3>Postdoctoral Fellows</h3>
        {% elsif item == 'pi' %}
            <h3>Principal Investigators</h3>
        {% elsif item == 'gradstudent' %}
            <h3>PhD Students</h3>
        {% elsif item == 'engineer' %}
            <h3>Research Engineers</h3>
        {% elsif item == 'visiting' %}
            <h3>Visiting Scholars</h3>
        {% elsif item == 'alumni' %}
            <h3>Alumni</h3>
        {% endif %}
        </div>
        <div class="content list people">
          {% for profile in listpeople %}
            <div class="list-item-people {{profile.cat|replace: ' ', '-'}} {{profile.subcat|replace: ' ', '-'}}">
              <p style="text-align: left; padding-left: 5em; margin: 0;">
                  &#x2022;
                  {% if profile.site %}
                    <a class="name" href="{{profile.site}}" target="_blank">
                  {% endif %}
                  {{profile.name}}
                  {% if profile.desc %}
                  - {{profile.desc}}
                  {% endif %}
                  {% if profile.site %}
                    </a>
                  {% endif %}
              </p>
            </div>
          {% endfor %}
        </div>
        <br />
    {% endif %}
{% endfor %}
</div>
