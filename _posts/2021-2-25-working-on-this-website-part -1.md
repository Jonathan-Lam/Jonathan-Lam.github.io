---
layout: post
author: Jonathan Lam
featured_img: /assets/img/template.png
tags: website jekyll bootstrap
---
I've spent some time learning/working on this website using Jekyll and Bootstrap 4. Through a mixture of documentation, trial and error, and perseverance, I at least have a basic layout of what details I want to display on this site. However, I did get caught up on one details; how to highlight the navbar link depending on the current page. I figured I would show how I did to impart this knowledge to fellow front end web developer learners. I assume the reader has some experience with Jekyll already.

The website is organized as follows:  
* _layouts
  * default.html
  * post.html
  * project.html
* _includes
  * footer.html
  * header.html
  * navbar.html
* _data
  * navbar.yml
  * projects.yml
* index.html
* ...other files

Layouts hold default.html, which uses the header, navbar, and fotoer in _includes. Here is a code snippet from navbar.html. The Liquid syntax has the % removed:

```
 <div class="collapse navbar-collapse" id="navbarResponsive">
    <ul class="navbar-nav ml-auto">
	{ for item in site.data.navbar }
		{ if page.url == item.link }
		<li class="nav-item active">
			<a class="nav-link" href="{{ item.link }}"><u>{{ item.name }}</u></a>
		</li>
		{ else }
		<li class="nav-item">
			<a class="nav-link" href="{{ item.link }}">{{ item.name }}</a>
		</li>
		{ endif }
	{ endfor }
    </ul>
 </div>
 ```
 
 The site.data.navbar references a YAML file shown below:
 
 ```
 - name: Home
  link: /
- name: Projects
  link: /projects.html
- name: About
  link: /about.html
```

I use the navbar.yml file to store the name and links to the other pages. If the current URL matches the navbar link, we use the "nav_item active" classes to illuminate the link in the navbar, as well as underline it. Otherwise, the link is made without the active class. One downside of course is that we need to update the navbar.yml file if we want to add more links to the navbar. Perhaps there is a way to automatically iterate through a directory and insert the page title and link. If there is, please let me know!
 