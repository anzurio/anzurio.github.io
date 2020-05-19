---
layout: default
title: Resume
permalink: /resume/
---

## Profile
{{ site.data.resume.professional-profile }}

## Experience
{% for experience in site.data.resume.experience %}
**{{ experience.title }}; {{ experience.company }}**
_{{ experience.location }} – {{ experience.date }}_
{% for item in experience.items %} 
- {{ item }} {% endfor %}
{% endfor %}

## Education	
{% for education in site.data.resume.education %}
**{{ education.institution }} – {{education.degree }}, {{ education.class }}**
_{{ education.location }}_
{% for item in education.items %} 
- {{ item }} {% endfor %}
{% endfor %}

{% for other in site.data.resume.others %}
## {{ other.title }}
{{ other.body }}
{% endfor %}
