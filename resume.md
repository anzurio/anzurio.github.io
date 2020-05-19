---
layout: default
title: Resume
permalink: /resume/
---

## Profile
Software architect with 12 years of professional experience developing a wide range of projects including object-oriented frameworks, libraries, web services, and applications in .NET, C++, and Javascript; over 8 years taking the software engineering manager, technical and team leader roles. I thrive on exploring computer programming at its core; getting my hands dirty with manual memory management, language theory and mathematical complexities.

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
