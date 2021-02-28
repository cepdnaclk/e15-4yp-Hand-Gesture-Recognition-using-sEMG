# eYY-4yp-project-template

This is a sample repository you can use for your Final Year Research project.

### Enable Github Pages

You can put the things to be shown in GitHub pages into the _docs/_ folder. Both html and md file formats are supported. You need to go to settings and enable GitHub pages and select _main_ branch and _docs_ folder from the dropdowns, as shown in the below image.

![image](https://user-images.githubusercontent.com/11540782/98789936-028d3600-2429-11eb-84be-aaba665fdc75.png)

### Special Configurations

These projects will be automatically added into [https://projects.ce.pdn.ac.lk](). If you like to show more details about your project on this site, you can fill the parameters in the file, _/docs/index.json_

```
{
   "title":"This is the title of the project",
   "team":[
      {
         "name":"Team Member Name 1",
         "email":"email@eng.pdn.ac.lk",
         "eNumber":"E/yy/xxx",
         "github_profile":"#",
         "linkedin_profile":"#",
         "researchgate_profile":"#"
      },
      {
         "name":"Team Member Name 2",
         "email":"email@eng.pdn.ac.lk",
         "eNumber":"E/yy/xxx",
         "github_profile":"#",
         "linkedin_profile":"#",
         "researchgate_profile":"#"
      },
      {
         "name":"Team Member Name 3",
         "email":"email@eng.pdn.ac.lk",
         "eNumber":"E/yy/xxx",
         "github_profile":"#",
         "linkedin_profile":"#",
         "researchgate_profile":"#"
      }
   ],
   "supervisors":[
      {
         "name":"Dr. Supervisor 1",
         "email":"email@eng.pdn.ac.lk",
         "linkedin_profile":"",
         "researchgate_profile":""
      },
      {
         "name":"Supervisor 2",
         "email":"email@eng.pdn.ac.lk",
         "linkedin_profile":"",
         "researchgate_profile":""
      }
   ],
   "description":"This is a brief introduction of the project. You need to use plain text without any specific characters here",
   "publications":[
      {
         "title":"Paper Title",
         "journal":"Journal or Conference Name",
         "description":"Sample Description",
         "url":"#"
      }
   ],
   "media":[
      {
         "type":"youtube",
         "url":"#"
      }
   ],
   "tags":[
      "Final Year Projects"
   ]
}
```

*linkedin_profile*,, *researchgate_profile*, *publications*, *media* parameters are optional and keep the default values, unless fill them.

Allowed media types: youtube

### Page Theme

A custom theme integrated with this GitHub Page, which is based on [github.com/cepdnaclk/eYY-project-theme](https://github.com/cepdnaclk/eYY-project-theme). If you like to remove this default theme, you can remove the file, _docs/\_config.yml_
