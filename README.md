
# Template for a static website  
To create a static website (without database), the following rules must be used.  
  
## I. Rules  
### Only files and folders in /src need to be modified.  
### Do not add an internal link in a href  
```  
#BAD:  
<a href="/contact">Contact</a>  
  
#GOOD  
<a href="{% link contact.html %}">Contact</a>  
```  
`{% link %}` will retrieve the variable `permalink: /contact` from the Front Matter of the contact page.  
If the link is changed on this page, it is changed throughout the site.  
### Google's first position is only reachable if we develop a quality website.
- [W3C Validator](https://validator.w3.org/): it is very rigorous (maybe too much), but it helps us to fix a lot of errors in project.
- Use [Google Lighthouse](https://developers.google.com/web/tools/lighthouse) to check quality and fix errors. 90% is the minimum to reach.
- Check on [GTMetrix](https://gtmetrix.com/): A is the minimum to get.
- Use [Tinypng](https://tinypng.com/) if you need to optimise images.

### Process
1. Project managers assign your work in Asana. Your work is a project with steps displayed as checkboxes.
2. Clone the Repository locally
3. Each time you finish a task, **check the box in Asana**. It's really important because project manager and salers must be able to tell the customer at what stage of creation we are.
4. The **Continuous Deployment** is enabled for all projects. That means all of your changes will online in about 5 minutes without others actions than push to the master branch of the repository.
### Recommended process to make a site (each step must be a separate commit)
1. Create all the empty pages of the site
2. Modify the src/assets/css/scss/_variables.scss file to set the default theme (font, color, rounding,
etc.).
3. Make the header
4. Make the footer
5. Make the pages one by one

### Recommended/mandatory softwares
- Code: **Visual Studio Code** with plugins ***Prettier*** and ***Project Manager***
- Git: **Git Kraken** or **SourceTree** (**you cannot use command line** because we cannot verify our own code with the command line).
- **Slack** (mandatory): communication
- **Asana** (mandatory): projects and tasks management
- **TimeDoctor** (mandatory): improve productivity
- **ManaTime** (mandatory): manage paid leaves
  
<br>  
  
## II. How to work with Jekyll  
### A) Install Ruby  
[Details here](https://www.ruby-lang.org/en/documentation/installation/)
### B) Install Jekyll  
```sh  
gem install bundler jekyll;  
bundle update --bundler;  
```  
  
### C) Run locally  
```sh  
bundle exec jekyll serve --livereload;  
```  
Don't forget **--livereload**! It will reload page in browser each time you change something in code.
  
### D) Build PROD  
```sh  
JEKYLL_ENV="production" bundle exec jekyll build;  
```  
  
### E) Test code  
```sh  
JEKYLL_ENV="production" bundle exec jekyll build;  
bundle exec htmlproofer _site;  
```  
  
<br>

## III. Input of forms
*Mandatory fields*
- name: if there is firstName and lastName, you have to named lastName as name
- email: string in email format
*Mandatory hidden fields*
- type: estimate|contact
- redirectUrl: where redirect after the form is processed
- lang: fr|en
- website: integer

<br>

## IV. Explanation
### A) Folders and files  
#### Root  
- **_site/** contains the generated website  
- **src/** the source code  
- the other files contain the general configuration of Jekyll  
  
#### ./src  
- **_data/**: company.yml contains the website variables (email, phone, address, etc.) and pictures.yml contains the  
default configuration of the images integrated on the site (this file should generally not be modified).  
- **_layouts** contains the basic architecture of a page.  It includes files found in **_includes**.  
and of course it's used in all pages.  
- **_includes**: Files that can be included from other pages can be found here.  
- **assets**: contains the scss files that will be compiled into css, the js files and the images that will be  
resized according to the configuration of **_data/pucture.yml**.  
- Finally each others files are the pages of the website.  
- 404.html is a special page that is called if no page is found.  
  
### B) The images  
Creating styles dans ./src/_data/picture.yml  
```  
markup_presets:  
  default:  
    ...  
  custom-theme:  
    widths: [30]  
    formats: [webp, original]  
    attributes:  
      source: class="img-fluid" width="30" height="30"  
      img: class="img-fluid" width="30" height="30"  
```  
  
Then apply them to the site:  
```  
{% picture custom-theme assets/img/image.png %}  
```  
  
If needed, the complete documentation is here: [Jekyll Picture Tag](https://rbuchberger.github.io/jekyll_picture_tag/)